# All In One Pro Max Ultimate

Cấu hình Shadowrocket gộp các rule và script cho YouTube, Spotify, SoundCloud, Locket cùng một số ứng dụng khác.

## Nội dung

- `10in1`: file cấu hình chính lấy từ [Gaucuto/ver2promax](https://raw.githubusercontent.com/Gaucuto/ver2promax/refs/heads/main/10in1).
- `dependencies/`: các JavaScript được tham chiếu bởi `script-path` trong cấu hình.
- `dependencies/manifest.txt`: danh sách 16 URL phụ thuộc duy nhất.
- `dependencies/SHA256SUMS`: checksum SHA-256 để kiểm tra file tải xuống.

## Cài đặt

1. Mở `10in1` và nhập vào Shadowrocket hoặc trình quản lý cấu hình tương thích.
2. Bật MITM trong ứng dụng nếu muốn sử dụng các rule cần sửa request/response.
3. Đảm bảo các URL `script-path` có thể truy cập Internet. Các script vẫn được tham chiếu từ URL gốc; bản sao trong `dependencies/` dùng để lưu trữ và kiểm tra.

## Cập nhật phụ thuộc

Tải lại từng URL trong `dependencies/manifest.txt`, thay thế file cùng tên trong `dependencies/`, rồi tạo lại checksum:

```sh
while IFS= read -r url; do
  curl -L --fail --silent --show-error "$url" \
    -o "dependencies/${url##*/}"
done < dependencies/manifest.txt

sha256sum 10in1 dependencies/*.js > dependencies/SHA256SUMS
```

## Kiểm tra

```sh
sha256sum -c dependencies/SHA256SUMS
```

Lệnh trên phải báo `OK` cho `10in1` và toàn bộ script.

## Lưu ý

- Đây là cấu hình bên thứ ba; hãy kiểm tra rule và script trước khi sử dụng.
- Tính năng thực tế phụ thuộc vào phiên bản ứng dụng, máy chủ và khả năng tương thích của Shadowrocket.
- Không chia sẻ thông tin tài khoản, token hoặc dữ liệu riêng tư trong quá trình kiểm tra.
