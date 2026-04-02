# DNS Setup

## Hiện trạng hiện tại

- `sacxemaydien.vn` đang trỏ về `157.10.44.162`
- `www.sacxemaydien.vn` đang trỏ về `157.10.44.162`
- `app.sacxemaydien.vn` chưa có bản ghi DNS

Để public website landing bằng GitHub Pages và tách phần app vận hành riêng, cần đổi DNS theo cấu hình dưới đây.

## Mục tiêu

- `https://sacxemaydien.vn` -> GitHub Pages
- `https://www.sacxemaydien.vn` -> GitHub Pages
- `https://app.sacxemaydien.vn` -> app vận hành riêng

## Bản ghi DNS cần cấu hình

### Domain gốc `sacxemaydien.vn`

Tạo hoặc sửa 4 bản ghi `A`:

- Host: `@`
  Type: `A`
  Value: `185.199.108.153`
- Host: `@`
  Type: `A`
  Value: `185.199.109.153`
- Host: `@`
  Type: `A`
  Value: `185.199.110.153`
- Host: `@`
  Type: `A`
  Value: `185.199.111.153`

### Subdomain `www.sacxemaydien.vn`

Tạo hoặc sửa 1 bản ghi `CNAME`:

- Host: `www`
  Type: `CNAME`
  Value: `caobach369.github.io`

### Subdomain `app.sacxemaydien.vn`

Nếu app vẫn chạy ở VPS hiện tại thì tạm thời dùng:

- Host: `app`
  Type: `A`
  Value: `157.10.44.162`

Nếu sau này app chuyển sang máy khác, chỉ cần đổi bản ghi `app` sang IP hoặc CNAME mới mà không ảnh hưởng website public.

## GitHub Pages

Trong repo GitHub:

1. Vào `Settings`
2. Vào `Pages`
3. Chọn `Deploy from a branch`
4. Chọn branch `main`
5. Chọn folder `/ (root)`
6. Lưu lại
7. Điền custom domain là `sacxemaydien.vn`
8. Khi DNS đúng, bật `Enforce HTTPS`

## Lưu ý Cloudflare

Nếu domain đang dùng Cloudflare:

- Với `@` và `www`, nên để `DNS only` trong giai đoạn đầu
- Sau khi GitHub Pages hoạt động ổn định mới cân nhắc bật proxy
- Với `app`, nếu app dùng SSL/reverse proxy riêng thì kiểm tra kỹ trước khi bật proxy

## Kiểm tra sau khi trỏ DNS

Kiểm tra các địa chỉ sau:

- `https://sacxemaydien.vn`
- `https://www.sacxemaydien.vn`
- `https://app.sacxemaydien.vn`

Nếu `sacxemaydien.vn` chưa lên ngay thì chờ propagation DNS từ 5 phút đến vài giờ.