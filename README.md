# BaseOS Connect

Developer documentation for the shared integration protocol.

Production API: `https://baseos.net/api/v1/connect`

Canonical receiver on a customer website: `https://example.com/baseos`

BaseOS calls `POST {receiver}/commands` and `GET {receiver}/health`.

## Install

Laravel:

```bash
composer require baseos/connect-laravel
php artisan vendor:publish --tag=baseos-connect-config
php artisan migrate
php artisan baseos:pair <PAIRING_CODE>
```

Node.js. The npm organization is `baseos`, so the package scope is `@baseos`.

```bash
npm install @baseos/connect-node
npx baseos-connect pair <PAIRING_CODE> \
  --site=https://example.com \
  --receiver=https://example.com/baseos
```

## Commands

| Command | Laravel | CLI |
|---|---|---|
| Pair | `php artisan baseos:pair CODE` | `npx baseos-connect pair CODE --site= --receiver=` |
| Status | `php artisan baseos:status` | `npx baseos-connect status` |
| Sync schema | `php artisan baseos:sync` | `npx baseos-connect sync` |
| Diagnose | `php artisan baseos:doctor` | `npx baseos-connect doctor` |
| Disconnect | `php artisan baseos:disconnect CONNECTION_ID` | `npx baseos-connect disconnect CONNECTION_ID` |

Disconnect removes the credential on the website. Also revoke that connection in BaseOS.

## Concepts

Pairing uses a one-time code. The response `secret` is the HMAC key. The same signature, site identity, tenant id, and command list apply to every connector. The protocol source is the `connect-spec` repository.
