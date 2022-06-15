---
layout: default
title: 4.3 API Lấy thông tin giao dịch
parent: 4. Đặc tả API
grand_parent: Home
sidebar_position: 6
---

![REST API](https://img.shields.io/static/v1?label=API&message=REST&color=orange)

- API lấy thông tin giao dịch được sử dụng để lấy về thông tin của giao dịch trong
  trường hợp backend của Đối tác không nhận được callback của hệ thống MB Payment Hub.

⚠️ **LƯU Ý:** API này chỉ sử dụng cho khách hàng đăng ký sử dụng tính năng thanh toán.

## Endpoint

```
    GET /api/merchant/v1/transaction/{transactionId}
```

## Header

```
    Content-Type: application/json
    MERCHANT_CODE: Mã đối tác
    MERCHANT_SECRET: Khóa bí mật của Đối tác
```

## Dữ liệu truyền lên

| Tham số         | Mô tả                                                        |
| --------------- | ------------------------------------------------------------ |
| `transactionId` | **BẮT BUỘC**. Kiểu String, tối đa 30 ký tự. ID của giao dịch |

## Dữ liệu trả về

| Tham số          | Mô tả                                                                                                                                                                                                                                                                                                                                                      |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`             | Kiểu String, tối đa 30 ký tự. ID của giao dịch                                                                                                                                                                                                                                                                                                             |
| `merchant.code`  | Kiểu String, tối đa 100 ký tự. Mã đối tác                                                                                                                                                                                                                                                                                                                  |
| `merchant.name`  | Kiểu String, tối đa 256 ký tự. Tên đối tác                                                                                                                                                                                                                                                                                                                 |
| `cif`            | Kiểu String, tối đa 45 ký tự. Mã khách hàng MB                                                                                                                                                                                                                                                                                                             |
| `amount`         | Kiểu Long. Số tiền thực hiện giao dịch                                                                                                                                                                                                                                                                                                                     |
| `description`    | Kiểu String, tối đa 200 ký tự. Nội dung giao dịch                                                                                                                                                                                                                                                                                                          |
| `type.code`      | Kiểu String, tối đa 100 ký tự. Mã loại giao dịch                                                                                                                                                                                                                                                                                                           |
| `type.name`      | Kiểu String, tối đa 256 ký tự. Tên loại giao dịch                                                                                                                                                                                                                                                                                                          |
| `type.allowCard` | Kiểu Boolean. Cho phép thanh toán bằng thẻ hay không <br /> `true`: Có cho phép <br /> `false`: Không cho phép                                                                                                                                                                                                                                             |
| `successMessage` | Kiểu String, tối đa 2000 ký tự. Thông báo khi thanh toán thành công                                                                                                                                                                                                                                                                                        |
| `metadata`       | Kiểu String, tối đa 500 ký tự. Chuỗi dữ liệu bổ sung thông tin cho giao dịch được Đối tác truyền vào khi khởi tạo giao dịch                                                                                                                                                                                                                                |
| `createdTime`    | Kiểu Date. Thời điểm tạo giao dịch <br /> Theo định dạng `yyyy-MM-dd’T’HH:mm:ss` (ISO 8601)                                                                                                                                                                                                                                                                |
| `paidTime`       | Kiểu Date. Thời điểm thanh toán <br /> Theo định dạng `yyyy-MM-dd’T’HH:mm:ss` (ISO 8601)                                                                                                                                                                                                                                                                   |
| `status`         | Kiểu String, tối đa 45 ký tự. Trạng thái của giao dịch, bao gồm: <br /> `PENDING`: Đang chờ thanh toán <br /> `PAID`: Đã thanh toán                                                                                                                                                                                                                        |
| `fundingSource`  | Kiểu String, tối đa 100 ký tự. Nguồn tiền được khách hàng sử dụng để thanh toán <br /> `ACCOUNT`: Nguồn TKTT <br /> `CARD`: Nguồn thẻ (bao gồm `CREDIT_CARD` & `PREPAID_CARD`)                                                                                                                                                                             |
| `cardType`       | Kiểu String, tối đa 100 ký tự. Loại thẻ được khách hàng sử dụng để thanh toán <br />`BMC` <br />`MBVT_VISA_CREDIT` <br />`SIMPLE` <br />`VIETTEL_PAYROLL` <br />`MBVG_VISA_CREDIT` <br />`VISA_CREDIT` <br />`SME_CREDIT` <br />`JCB_CREDIT` <br />`SSC` <br />`PRIORITY_MBVG_VISA_CREDIT` <br />`PRIORITY_VISA_CREDIT` <br />`NEWPLUS` <br />`VIETTELPAY` |
