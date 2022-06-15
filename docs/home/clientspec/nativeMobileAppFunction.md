---
layout: default
title: 3.2 Tích hợp các native mobile app function
parent: 3. Tích hợp client
grand_parent: home
sidebar_position: 2
---

# Thông tin chung

- Một số sự kiện trên trên nền tảng web không xử lý được, cần được xử lý từ phía
  Mobile app để đảm bảo trải nghiệm người dùng. Trong trường hợp này web của đối
  tác có nhu cầu muốn mở một trang web khác. Do đó web của Đối tác sẽ bắn ra một sự
  kiện để Mobile App có thể put một webview khác đó đè lên webview hiện tại

## Phương thức kết nối

- Ứng dụng WEB của Đối tác thực hiện gọi hàm `Javascript` để truyền dữ liệu giao dịch
  cho MB App.
- Cú pháp:

```js
window["ReactNativeWebView"].postMessage({
  type: "OPEN_NEW_WEBVIEW",
  name: "Bảo hiểm tai nạn",
  link: "https://www.mbageas.life/",
});
```

## Dữ liệu truyền lên

| Tham số | Mô tả                                                                                     |
| ------- | ----------------------------------------------------------------------------------------- |
| `type`  | **Bắt buộc** Kiểu String, tối đa 30 ký tự. Loại action mặc định truyền `OPEN_NEW_WEBVIEW` |
| `name`  | **Bắt buộc** Kiểu String, tối đa 100 ký tự. Tên hiển thị trên header của Webview          |
| `link`  | **Bắt buộc** Kiểu String, tối đa 1000 ký tự. Link của webview                             |
