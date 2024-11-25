---
title: "Implementasi Autentikasi Passkey di Aplikasi Laravel Kamu"
datePublished: Mon Nov 25 2024 23:32:01 GMT+0000 (Coordinated Universal Time)
cuid: cm3xnx78c000z08ic6gpva24w
slug: implementasi-autentikasi-passkey-di-aplikasi-laravel-kamu
tags: laravel, php

---

Passkey adalah masa depan dari autentikasi. Dengan teknologi ini, Kamu bisa mengizinkan pengguna membuat akun dan login hanya dengan perangkat mereka, tanpa perlu memasukkan kata sandi.

### Apa Itu Passkey?

Passkey memungkinkan pengguna untuk login menggunakan perangkat mereka (seperti ponsel atau komputer) dan biometrik seperti sidik jari atau pengenalan wajah. Kunci publik dan pribadi akan dibuat dan dipertukarkan antara perangkat dan server, memastikan keamanan autentikasi.

## Apa yang Akan Kita Bangun

Di artikel ini, kita akan membangun demo autentikasi passkey di Laravel menggunakan **WebAuthn API**. Kita akan menggunakan SimpleWebAuthn untuk sisi klien dan Webauthn Framework dari Spomky Labs di sisi server.

### Langkah Instalasi

1. **Instal dependency yang diperlukan**:
    
    ```bash
    yarn add @simplewebauthn/browser
    composer require web-auth/webauthn-lib
    ```
    
2. **Tambahkan Alpine.js**: Kita akan menggunakan Alpine.js dari CDN untuk interaktivitas di sisi klien.
    

## Alur Autentikasi

Berikut adalah alur dasar autentikasi passkey yang akan kita implementasikan:

1. Pengguna memasukkan username.
    
2. Perangkat mereka akan diminta untuk membuat passkey.
    
3. Kunci publik akan dikirim ke server dan disimpan di database.
    
4. Pada login berikutnya, perangkat akan memverifikasi pengguna melalui biometrik, tanpa memerlukan password.
    

## Struktur Database

### Tabel Users

Tabel ini menyimpan data pengguna tanpa kata sandi:

```php
Schema::create('users', function (Blueprint $table) {
    $table->id();
    $table->string('username')->unique();
    $table->rememberToken();
    $table->timestamps();
});
```

### Tabel Authenticators

Setiap pengguna bisa memiliki beberapa perangkat untuk autentikasi. Data perangkat ini disimpan di tabel **authenticators**:

```php
Schema::create('authenticators', function (Blueprint $table) {
    $table->id();
    $table->foreignId('user_id')->constrained()->onDelete('cascade');
    $table->text('credential_id');
    $table->text('public_key');
    $table->timestamps();
});
```

Modelnya akan mengenkripsi `credential_id` dan `public_key` untuk keamanan:

```php
class Authenticator extends Model {
    use HasFactory;

    protected $fillable = ['credential_id', 'public_key'];

    protected $casts = [
        'credential_id' => 'encrypted',
        'public_key'    => 'encrypted:json',
    ];

    public function user() {
        return $this->belongsTo(User::class);
    }

    public function credentialId(): Attribute {
        return new Attribute(
            get: fn($value) => base64_decode($value),
            set: fn($value) => base64_encode($value)
        );
    }
}
```

## JavaScript untuk Autentikasi

Berikut kode JavaScript untuk mengatur proses autentikasi menggunakan SimpleWebAuthn di sisi klien:

```javascript
import {
    startAuthentication,
    startRegistration,
    browserSupportsWebAuthn,
} from '@simplewebauthn/browser';
import './bootstrap';

document.addEventListener('alpine:init', () => {
    Alpine.data('authForm', () => ({
        mode: 'login',
        username: '',
        browserSupported: browserSupportsWebAuthn(),
        error: null,
        submit() {
            this.error = null;
            return this.mode === 'login' ? this.submitLogin() : this.submitRegister();
        },
        submitRegister() {
            window.axios
                .post('/registration/options', { username: this.username })
                .then((response) => startRegistration(response.data))
                .then((attResp) => axios.post('/registration/verify', attResp))
                .then((verificationResponse) => {
                    if (verificationResponse.data?.verified) {
                        return window.location.reload();
                    }
                    this.error = 'Error saat verifikasi registrasi.';
                })
                .catch((error) => {
                    this.error = error?.response?.data?.message || error;
                });
        },
        submitLogin() {
            window.axios
                .post('/authentication/options', { username: this.username })
                .then((response) => startAuthentication(response.data))
                .then((attResp) => axios.post('/authentication/verify', attResp))
                .then((verificationResponse) => {
                    if (verificationResponse.data?.verified) {
                        return window.location.reload();
                    }
                    this.error = 'Error saat verifikasi autentikasi.';
                })
                .catch((error) => {
                    const errorMessage = error?.response?.data?.message || error;
                    if (errorMessage === 'User not found') {
                        this.mode = 'confirmRegistration';
                        return;
                    }
                    this.error = errorMessage;
                });
        },
    }));
});
```

## Authentication Controller

### Membuat Opsi Autentikasi

Ketika pengguna memasukkan username, server akan mengirimkan opsi autentikasi:

```php
class AuthenticationController extends Controller {
    const CREDENTIAL_REQUEST_OPTIONS_SESSION_KEY = 'publicKeyCredentialRequestOptions';

    public function generateOptions(Request $request) {
        $user = User::where('username', $request->input('username'))->firstOrFail();
        $userEntity = PublicKeyCredentialUserEntity::create(
            $user->username,
            (string) $user->id,
            $user->username,
            null
        );

        // Dapatkan daftar authenticator yang terdaftar
        $pkSourceRepo = new CredentialSourceRepository();
        $registeredAuthenticators = $pkSourceRepo->findAllForUserEntity($userEntity);

        // Buat opsi autentikasi
        $allowedCredentials = collect($registeredAuthenticators)
            ->pluck('public_key')
            ->map(fn($publicKey) => PublicKeyCredentialSource::createFromArray($publicKey))
            ->map(fn($credential) => $credential->getPublicKeyCredentialDescriptor())
            ->toArray();

        $pkRequestOptions = PublicKeyCredentialRequestOptions::create(random_bytes(32))
            ->allowCredentials(...$allowedCredentials);

        $serializedOptions = $pkRequestOptions->jsonSerialize();
        $request->session()->put(self::CREDENTIAL_REQUEST_OPTIONS_SESSION_KEY, $serializedOptions);

        return $serializedOptions;
    }
}
```

### Verifikasi Autentikasi

Setelah perangkat pengguna mengirimkan data autentikasi, server akan memverifikasi:

```php
class AuthenticationController extends Controller {
    public function verify(Request $request, ServerRequestInterface $serverRequest) {
        // Validasi respons autentikasi
        $responseValidator = AuthenticatorAssertionResponseValidator::create(
            new CredentialSourceRepository(),
            IgnoreTokenBindingHandler::create(),
            ExtensionOutputCheckerHandler::create(),
            Manager::create()->add(ES256::create(), RS256::create())
        );

        $publicKeyCredential = PublicKeyCredentialLoader::create()->load(json_encode($request->all()));
        $authenticatorAssertionResponse = $publicKeyCredential->getResponse();

        $publicKeyCredentialSource = $responseValidator->check(
            $publicKeyCredential->getRawId(),
            $authenticatorAssertionResponse,
            PublicKeyCredentialRequestOptions::createFromArray(session(self::CREDENTIAL_REQUEST_OPTIONS_SESSION_KEY)),
            $serverRequest,
            $authenticatorAssertionResponse->getUserHandle()
        );

        // Autentikasi berhasil
        $user = User::where('username', $publicKeyCredentialSource->getUserHandle())->firstOrFail();
        Auth::login($user);

        return ['verified' => true];
    }
}
```

Dengan mengikuti langkah-langkah di atas, Kamu sudah bisa mengimplementasikan autentikasi passkey di aplikasi Laravel Kamu!