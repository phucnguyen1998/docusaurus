---
sidebar_position: 2
---

# 2. Luồng thanh toán

## Thông tin chung

### Mục đích

- Trong mục này của tài liệu sẽ mô tả phương thức tích hợp backend và client cho
  trường hợp Merchant muốn thực hiện yêu cầu mời khách hàng thanh toán cho một
  dịch vụ của Merchant.

<!-- ![alt text](../../assets/images/thread-pay.png) -->

{% include flow.html %}

- **Bước 1**: Khách hàng mở webview của đối tác trên MB App và thực hiện thanh toán
  cho dịch vụ của đối tác
- **Bước 2**: Máy chủ backend của Đối tác thực hiện yêu cầu hệ thống MB Payment Hub
  khởi tạo giao dịch thanh toán
- **Bước 3**: Hệ thống MB Payment Hub trả lại thông tin giao dịch cho máy chủ backend
  của Đối tác
- **Bước 4**: Máy chủ backend của Đối tác gửi message chứa thông tin giao dịch sang
  MB App
- **Bước 5**: Ứng dụng MB App gửi thông tin giao dịch được truyền vào từ Đối tác lên
  MB App Backend để xác nhận thông tin giao dịch
- **Bước 6**: MB App Backend gửi thông tin giao dịch sang MB Payment Hub để xác
  nhận thông tin giao dịch
- **Bước 7**: Hệ thống MB Payment Hub kiểm tra thông tin giao dịch và trả về kết quả
  cho MB App Backend
- **Bước 8**: Hệ thống MB App Backend trả về kết quả cho phép khách hàng thực hiện
  thanh toán trên MB App
- **Bước 9**: Khách hàng thực hiện thanh toán trên MB App
- **Bước 10**: Sau khi khách hàng thanh toán thành công, hệ thống MB App Backend
  thực hiện thông báo kết quả giao dịch đến hệ thống MB Payment Hub
- **Bước 11**: Hệ thống MB Payment Hub cập nhật kết quả giao dịch và thực hiện thông
  báo kết quả cho hệ thống backend của Đối tác
