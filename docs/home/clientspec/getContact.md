---
layout: default
title: 3.4 Truyền sự kiện khi muốn lấy danh bạ
parent: 3. Tích hợp client
grand_parent: home
sidebar_position: 4
---

# Thông tin chung

- Một số sự kiện trên trên nền tảng web không xử lý được, cần được xử lý từ phía
  Mobile app để đảm bảo trải nghiệm người dùng. Trong trường hợp này web của đối
  tác có nhu cầu lấy danh bạ trên app MBBank. Do đó web của Đối tác sẽ bắn ra
  một sự kiện để Mobile App cung cấp danh bạ cho web của Đối tác

## Phương thức kết nối

- Ứng dụng WEB của Đối tác thực hiện gọi hàm `Javascript` để truyền dữ liệu giao dịch
  cho MB App.

- Cú pháp:

```js
window["ReactNativeWebView"].postMessage({
  type: "GET_CONTACT",
});
```

## Dữ liệu truyền lên

- Dữ liệu nhận vào của hàm truyền dữ liệu ở định dạng JSON như sau:

| Tham số | Mô tả                                                                                |
| ------- | ------------------------------------------------------------------------------------ |
| `type`  | **Bắt buộc** Kiểu String, tối đa 30 ký tự. Loại action mặc định truyền `GET_CONTACT` |

## Dữ liệu trả về

- Dữ liệu trả về sẽ là 1 list JSON như sau:

| Tham số | Mô tả                                                              |
| ------- | ------------------------------------------------------------------ |
| `name`  | Kiểu String, tối đa 100 ký tự. Tên được lưu trong danh bạ          |
| `phone` | Kiểu String, tối đa 11 ký tự. Số điện thoại                        |
| `type`  | Kiểu String, tối đa 100 ký tự. Nhóm đối tượng: `work`, `home`, ... |
