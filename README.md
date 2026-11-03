

1. Vấn đề là gì?
Nam không truy cập được trang quản trị do nhập sai tên miền. DNS không tìm thấy địa chỉ IP tương ứng nên trình duyệt báo lỗi DNS_PROBE_FINISHED_NXDOMAIN.
Cần xác định lỗi xảy ra ở máy người dùng (Client) hay máy chủ (Server).
Nam sửa đúng tên miền nhưng vẫn nhận lỗi 404 Not Found.

2. Yêu cầu là gì?
- **Chức năng 1 (Phân tích mạng):** Giải thích chi tiết tiến trình DNS Lookup từ khi Nam gõ tên miền đến khi trình duyệt tìm thấy địa chỉ IP máy chủ.

- **Chức năng 2 (Chẩn đoán lỗi):** Phân biệt bản chất giữa lỗi DNS và lỗi 500 Internal Server Error để xác định lỗi này nằm ở phía Client hay Server.

3. Cách làm:

p1
- Input: Tên miền (phong-dieu-phoi.grenlog.vn).
- Output: Địa chỉ IP của máy chủ.
- Luồng DNS:
  + Bước 1: Nam nhập tên miền vào trình duyệt.
  + Bước 2: Trình duyệt kiểm tra bộ nhớ DNS Cache.
  + Bước 3: Nếu chưa có, máy tính gửi yêu cầu đến DNS Resolver.
  + Bước 4: DNS Resolver tra cứu các máy chủ DNS để tìm địa chỉ IP.
  + Bước 5: Nếu tìm thấy, IP được trả về trình duyệt để kết nối máy chủ.

Do Nam nhập sai grenlog.vn thay vì greenlog.vn nên DNS không tìm thấy tên miền. Có thể hiểu DNS giống như cuốn danh bạ Internet, chỉ cần sai một ký tự thì có thể không tìm được địa chỉ cần thiết.

p2
- DNS_PROBE_FINISHED_NXDOMAIN: DNS không tìm thấy tên miền, yêu cầu chưa thể kết nối đến máy chủ.
- HTTP 500 Internal Server Error: Yêu cầu đã đến máy chủ nhưng máy chủ gặp lỗi khi xử lý.

Có thể dùng F12 → Network → tải lại trang → kiểm tra cột Status để xem mã trạng thái HTTP.

p3
Lỗi 404 xảy ra khi máy chủ đã nhận được yêu cầu nhưng không tìm thấy trang hoặc tài nguyên tương ứng. Nguyên nhân có thể do đường dẫn sai, trang đã bị xóa hoặc địa chỉ trang không tồn tại.

