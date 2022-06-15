---
layout: default
title: 4.1 API xác minh token
parent: 4. Đặc tả API
grand_parent: Home
sidebar_position: 5
---

![REST API](https://img.shields.io/static/v1?label=API&message=REST&color=orange)

- API xác minh token được sử dụng để xác minh token phục vụ cho việc thiết lập phiên
  làm việc của khách hàng và truy xuất thông tin cá nhân của khách hàng.
- [Cơ chế chia sẻ token](../shareTokenLogin.html)

📣 Update (23/03/2022) Một số merchant đang sử dụng cơ chế đăng nhập cũ (do MB khởi tạo LoginToken) sẽ không được hỗ trợ sau ngày 01/04/2022

## Endpoint

```
    POST /api/merchant/v1/session/verify
```

## Header

```
    Content-Type: application/json
    MERCHANT_CODE: Mã đối tác
    MERCHANT_SECRET: Khóa bí mật của Đối tác
```

## Dữ liệu truyền lên

| Tham số | Mô tả                                           |
| ------- | ----------------------------------------------- |
| `token` | **Bắt buộc** Kiểu String. Login token từ MB App |

## Dữ liệu trả về

| Tham số    | Mô tả                                                                                          |
| ---------- | ---------------------------------------------------------------------------------------------- |
| `cif`      | **Bắt buộc** Kiểu String, tối đa 35 ký tự. Mã khách hàng tại MB                                |
| `fullname` | **Bắt buộc** Kiểu String, tối đa 255 ký tự. Họ và tên khách hàng                               |
| `dob`      | **Bắt buộc** Kiểu Date, Ngày sinh của khách hàng <br /> Theo định dạng `yyyy-MM-dd` (ISO 8601) |
| `idCardNo` | **Bắt buộc** Kiểu String, tối đa 20 ký tự. Số giấy tờ tùy thân của khách hàng                  |
| `mobile`   | **Bắt buộc** Kiểu String, tối đa 20 ký tự. Số điện thoại của khách hàng                        |
| `email`    | **Bắt buộc** Kiểu String, tối đa 100 ký tự. Địa chỉ email của khách hàng                       |
