---
layout: default
title: 3.1 Truyền dữ liệu payment transaction cho MB App
parent: 3. Tích hợp client
grand_parent: home
sidebar_position: 1
---

# Thông tin chung

- Sau khi Backend của Đối tác đã khởi tạo thành công giao dịch (bằng việc gọi sang
  API của MB Payment Hub) thì Đối tác cần truyền dữ liệu giao dịch này cho MB App
  để người dùng có thể bắt đầu thực hiện thanh toán cho giao dịch.

> ⚠️**LƯU Ý:** Để dùng được tính năng thanh toán, đối tác cần thông tin về tài **_khoản chuyên thu_** để đội vận hành MBBANK cấu hình.

## Phương thức kết nối

- Ứng dụng WEB của Đối tác thực hiện gọi hàm `Javascript` để truyền dữ liệu giao dịch
  cho MB App.
- Cú pháp:

```js
    window['ReactNativeWebView'].postMessage(JSON.stringify({
        type: 'PAYMENT_HUB_TRANSACTION',
        data: {
            merchant: {
                code: 'MBAL',
                name: 'Bảo hiểm nhân thọ MB AGEAS LIFE',
            },
            type: {
                code: 'BHUT',
                name: 'Mua bảo hiểm ung thư',
                allowCard: true,
            },
            id: 'AJX014TUYI1121',
            amount: 1000000,
            description: 'Mua bao hiem ung thu MBAL 615000',
            successMessage: 'Cám ơn bạn đã mua bảo hiểm. MBAL sẽ liên lạc lại với bạn trong vòng 24h'
    }))
```

## Dữ liệu truyền lên

| Tham số               | Mô tả                                                                                                         |
| --------------------- | ------------------------------------------------------------------------------------------------------------- |
| `type`                | **Bắt buộc** Kiểu String, tối đa 30 ký tự. Loại dữ liệu mặc định truyền `PAYMENT_HUB_TRANSACTION`             |
| `data.merchant.code`  | **Bắt buộc** Kiểu String, tối đa 100 ký tự. Mã đối tác                                                        |
| `data.merchant.name`  | **Bắt buộc** Kiểu String, tối đa 256 ký tự.Tên đối tác                                                        |
| `data.type.code`      | **Bắt buộc** Kiểu String, tối đa 100 ký tự. Mã loại giao dịch                                                 |
| `data.type.name`      | **Bắt buộc** Kiểu String, tối đa 256 ký tự. Tên loại giao dịch                                                |
| `data.type.allowCard` | **Bắt buộc** Kiểu boolean. Có cho phép thanh toán bằng thẻ hay không? <br /> `true`: Có <br /> `false`: Không |
| `data.id`             | **Bắt buộc** Kiểu String, tối đa 45 ký tự. ID giao dịch được trả về từ MB Payment Hub                         |
| `data.amount`         | **Bắt buộc** Kiểu Long. Số tiền thực hiện giao dịch <br /> **Không được âm**                                  |
| `data.description`    | **Bắt buộc** Kiểu String, tối đa 200 ký tự. Nội dung giao dịch                                                |
| `data.successMessage` | **Không** bắt buộc. Kiểu String tối đa 2000 ký tự. Thông báo khi thanh toán thành công                        |
