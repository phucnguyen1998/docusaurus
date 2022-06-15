---
layout: default
title: 3.5 Truyền sự kiện khi muốn lấy vị trí
parent: 3. Tích hợp client
grand_parent: home
sidebar_position: 5
---

# Thông tin chung

- Một số sự kiện trên trên nền tảng web không xử lý được, cần được xử lý từ phía
  Mobile app để đảm bảo trải nghiệm người dùng. Trong trường hợp này web của đối
  tác có nhu cầu lấy vị trí trên app MBBank. Do đó web của Đối tác sẽ bắn ra
  một sự kiện để Mobile App cung cấp danh bạ cho web của Đối tác

## Phương thức kết nối

- Ứng dụng WEB của Đối tác thực hiện gọi hàm `Javascript` để truyền dữ liệu giao dịch
  cho MB App.

- Cú pháp:

```js
window["ReactNativeWebView"].postMessage({
  type: "GET_LOCATION",
});
```

## Dữ liệu truyền lên

- Dữ liệu nhận vào của hàm truyền dữ liệu ở định dạng JSON như sau:

| Tham số | Mô tả                                                                                 |
| ------- | ------------------------------------------------------------------------------------- |
| `type`  | **Bắt buộc** Kiểu String, tối đa 30 ký tự. Loại action mặc định truyền `GET_LOCATION` |

## Dữ liệu trả về

- Dữ liệu trả về sẽ có định dạng JSON như sau:

| Tham số     | Mô tả                                       |
| ----------- | ------------------------------------------- |
| `accuracy`  | Kiểu number, tối đa 100 ký tự. Độ chính xác |
| `latitude`  | Kiểu number, tối đa 100 ký tự. Vĩ độ        |
| `longitude` | Kiểu number, tối đa 100 ký tự. Kinh độ      |
