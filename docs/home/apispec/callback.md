---
layout: default
title: 4.4 API callback khi giao dịch được thanh toán
parent: 4. Đặc tả API
grand_parent: Home
sidebar_position: 7
---

![REST API](https://img.shields.io/static/v1?label=API&message=REST&color=orange)

- API do Đối tác cung cấp cho hệ thống MB Payment Hub gọi để thông báo khi một
  giao dịch được thanh toán thành công.

⚠️ **LƯU Ý:** API này chỉ sử dụng cho khách hàng đăng ký sử dụng tính năng thanh toán.

📣 Update (23/03/2022): <br/><span/>

> - Thay thế thuật toán `SHA1` thành `SHA256`<br/>

- Sử dụng checksum dạng HmacSha256 với khóa bí mật để validate checksum của đối tác
  (tham số CALLBACK_CHECKSUM_SECRET)
- Đối tác cần tạo ra mã checksum để so sánh với giá trị checksum được gọi sang để
  đảm bảo rằng lời gọi API xuất phát từ hệ thống của MB Payment Hub và các trường
  thông tin không bị chỉnh sửa trái phép

- Các bước tạo checksum:

      - **Bước 1**: Tạo chuỗi dữ liệu cần mã hóa dựa trên các trường dữ liệu được truyền sang khi

  gọi API của đối tác. Chú ý, nếu trường dữ liệu là NULL thì khi ghép chuỗi sẽ sử dụng giá
  trị chuỗi rỗng - Ví dụ: Đối với yêu cầu checksum có cấu trúc là:
  <br /> `merchantCode +transactionId + typeCode + cif + amount + status` <br />

      - Trong đó: <br />
          - ```merchantCode```: Mã đối tác<br />
          - ```transactionId```: ID giao dịch<br />
          - ```typeCode```: Mã loại giao dịch<br />
          - ```cif```: Mã khách hàng tại MB<br />
          - ```amount```: Số tiền thực hiện giao dịch<br />
          - ```status```: Trạng thái giao dịch<br />
          => Chuỗi dữ liệu tương ứng cần mã hóa là:<br />
          <p><span style="color: red">MIC</span><span style="color: green">AJX014TUYI1121</span><span style="color: #ad33ff">BHUT</span><span style="color: red">103267334</span><span style="color: green">100000</span><span style="color: #ad33ff">PAID</span></p>

      - **Bước 2**:  Băm chuỗi dữ liệu bằng thuật toán ```HMAC_SHA256``` với khóa bí mật của đối tác để

  tạo ra chuỗi nhị phân sau đó mã hóa chuỗi nhị phân bằng thuật toán `Base64`

## Endpoint

```
    URL: Do đối tác tự đình nghĩa và gửi lại cho hệ thống MB Payment Hub. API cần được public ra internet
    Method: POST
    Content-Type: application/json
```

## Header

```
    Do đối tác cung cấp các tham số tĩnh để truyền qua Headers
```

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
| `checksum`       | Kiểu String, Chuỗi mã hóa tạo ra dựa trên các tham số                                                                                                                                                                                                                                                                                                      |
