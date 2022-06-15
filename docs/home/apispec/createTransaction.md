---
layout: default
title: 4.2 API Khởi tạo giao dịch
parent: 4. Đặc tả API
grand_parent: Home
sidebar_position: 5
---

![REST API](https://img.shields.io/static/v1?label=API&message=REST&color=orange)

- API khởi tạo giao dịch được gọi từ server của Đối tác để thiết lập một giao dịch thanh
  toán mới để người dùng có thể thực hiện thanh toán trên MB App.

⚠️ **LƯU Ý:** API này chỉ sử dụng cho khách hàng đăng ký sử dụng tính năng thanh toán.

-📣 Update (23/03/2022):

Thêm trường sessionId
Thêm trường allowCard
Trường paymentType trở thành **BẮT BUỘC**

## Endpoint

```
    POST /api/merchant/v1/transaction
```

## Header

```
    Content-Type: application/json
    MERCHANT_CODE: Mã đối tác
    MERCHANT_SECRET: Khóa bí mật của Đối tác
```

## Dữ liệu truyền lên

| Tham số          | Mô tả                                                                                                                                                                                                             |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `sessionId`      | **BẮT BUỘC**. Mã phiên đăng nhập (Được trả về từ API xác minh token) Trường này được thêm vào bản update ngày 23/03/2022 và sẽ được hỗ trợ **KHÔNG** bắt buộc đến hết ngày 01/04/2022                             |
| `allowCard`      | **KHÔNG** bắt buộc. Cho phép thanh toán bằng thẻ hay không `true`: Có cho phép `false`: Không cho phép                                                                                                            |
| `cif`            | **BẮT BUỘC**. Kiểu String, tối đa 45 ký tự. Mã khách hàng tại MB                                                                                                                                                  |
| `amount`         | **BẮT BUỘC**. Kiểu Long. Số tiền thực hiện giao dịch **Yêu cầu:** 0 ≤ `amount` < 10 tỉ VND                                                                                                                        |
| `description`    | **BẮT BUỘC**. Kiểu String, tối đa 200 ký tự. Nội dung giao dịch                                                                                                                                                   |
| `type`           | **BẮT BUỘC**. Kiểu String, tối đa 45 ký tự. Mã loại giao dịch                                                                                                                                                     |
| `successMessage` | **KHÔNG** bắt buộc. Kiểu String, tối đa 2000 ký tự. Thông báo khi khách hàng thanh toán thành công _Nếu không truyền tham số này, hệ thống sẽ sử dụng thông báo mặc định của hệ thống._                           |
| `metadata`       | **KHÔNG** bắt buộc. Kiểu String, tối đa 500 ký tự. Chuỗi dữ liệu bất kỳ chưa dữ liệu bổ sung cho giao dịch và sẽ được trả về cho Đối tác khi truy vấn thông tin giao dịch hoặc khi thông báo giao dịch thành công |

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
| `createdTime`    | Kiểu Date. Thời điểm tạo giao dịch <br /> Theo định dạng `yyyy-MM-dd'T'HH:mm:ss` (ISO 8601)                                                                                                                                                                                                                                                                |
| `paidTime`       | Kiểu Date. Thời điểm thanh toán <br /> Theo định dạng `yyyy-MM-dd'T'HH:mm:ss` (ISO 8601)                                                                                                                                                                                                                                                                   |
| `status`         | Kiểu String, tối đa 45 ký tự. Trạng thái của giao dịch; bao gồm: <br />`PENDING`: Đang chờ thanh toán <br />`PAID`: Đã thanh toán                                                                                                                                                                                                                          |
| `fundingSource`  | Kiểu String, tối đa 2000 ký tự. Nguồn tiền được khách hàng sử dụng để thanh toán <br />`ACCOUNT`: Nguồn TKTT <br />`CARD`: Nguồn thẻ (bao gồm `CREDIT_CARD` & `PREPAID_CARD`)                                                                                                                                                                              |
| `cardType`       | Kiểu String, tối đa 100 ký tự. Loại thẻ được khách hàng sử dụng để thanh toán <br />`BMC` <br />`MBVT_VISA_CREDIT` <br />`SIMPLE` <br />`VIETTEL_PAYROLL` <br />`MBVG_VISA_CREDIT` <br />`VISA_CREDIT` <br />`SME_CREDIT` <br />`JCB_CREDIT` <br />`SSC` <br />`PRIORITY_MBVG_VISA_CREDIT` <br />`PRIORITY_VISA_CREDIT` <br />`NEWPLUS` <br />`VIETTELPAY` |
