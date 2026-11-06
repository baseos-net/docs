# BaseOS Connect

Connect a website so BaseOS can publish articles to it.
Kết nối website để BaseOS đăng bài lên đó.

## 1. Create a pairing code · Tạo mã ghép

In BaseOS, open the project, then **Website connection**, and create a code. It works once and expires after 15 minutes.
Trong BaseOS, mở dự án → **Kết nối website** → tạo mã. Mã dùng một lần và hết hạn sau 15 phút.

## 2. Install on the website · Cài trên website

Laravel. PHP 8.1+, Laravel 10–13.

```bash
composer require baseos/connect-laravel
php artisan vendor:publish --tag=baseos-connect-config
php artisan migrate
```

Set `APP_URL` to the public HTTPS address, and `BASEOS_REPOSITORY` to the class that stores posts. The class is described in the Laravel repository.
Đặt `APP_URL` là địa chỉ HTTPS công khai, và `BASEOS_REPOSITORY` là class lưu bài. Cách viết class nằm trong repository Laravel.

Node.js 18+.

```bash
npm install @baseos/connect-node
```

Mount the handler at `https://your-domain/baseos`. The Node repository shows Express, Fastify, and Next.js.
Gắn handler tại `https://tên-miền/baseos`. Repository Node có ví dụ Express, Fastify và Next.js.

## 3. Pair · Ghép

```bash
php artisan baseos:pair CODE
```

```bash
npx baseos-connect pair CODE \
  --site=https://example.com \
  --receiver=https://example.com/baseos
```

When the command finishes, the website shows as connected in BaseOS. Open **Publishing setup** there to map categories.
Lệnh xong, website hiện là đã kết nối trong BaseOS. Mở **Cấu hình đăng bài** ở đó để gắn chuyên mục.

## After pairing · Sau khi ghép

| You want | Laravel | Node.js |
|---|---|---|
| Check the connection · Xem kết nối | `php artisan baseos:status` | `npx baseos-connect status` |
| Send the site structure again · Gửi lại cấu trúc site | `php artisan baseos:sync` | `npx baseos-connect sync` |
| Find a setup problem · Tìm lỗi cài đặt | `php artisan baseos:doctor` | `npx baseos-connect doctor` |
| Remove the connection on this website · Gỡ kết nối trên website | `php artisan baseos:disconnect ID` | `npx baseos-connect disconnect ID` |

After disconnect, revoke the same connection in BaseOS.
Sau khi gỡ trên website, thu hồi kết nối đó trong BaseOS.

Several websites on one codebase: pair each one with `--tenant=your-site-id`.
Nhiều website trên một mã nguồn: ghép từng website với `--tenant=mã-website`.
