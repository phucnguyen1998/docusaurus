---
layout: default
title: 3.3 Truyền sự kiện khi muốn đóng webview
parent: 3. Tích hợp client
grand_parent: home
sidebar_position: 3
---

# Thông tin chung

- Một số sự kiện trên trên nền tảng web không xử lý được, cần được xử lý từ phía
  Mobile app để đảm bảo trải nghiệm người dùng. Trong trường hợp này web của đối
  tác có nhu cầu đóng lại chính webview của Đối tác. Do đó web của Đối tác sẽ bắn ra
  một sự kiện để Mobile App có đóng chính webview hiện tại của đối tác.

## Phương thức kết nối

- Ứng dụng WEB của Đối tác thực hiện gọi hàm `Javascript` để truyền dữ liệu giao dịch
  cho MB App.

- Cú pháp:

```js
window["ReactNativeWebView"].postMessage({
  type: "GO_BACK",
});
```

## Dữ liệu truyền lên

- Dữ liệu nhận vào của hàm truyền dữ liệu ở định dạng JSON như sau:

| Tham số | Mô tả                                                                            |
| ------- | -------------------------------------------------------------------------------- |
| `type`  | **Bắt buộc** Kiểu String, tối đa 30 ký tự. Loại action mặc định truyền `GO_BACK` |
