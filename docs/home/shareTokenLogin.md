---
sidebar_position: 1
---

# 1. Chia sẻ Token đăng nhập

## Tích hợp phía client

### Cơ chế nhận token qua URL

- Khi ứng dụng MB App mở ra webview hiển thị nội dung WEB của Đối tác, login
  token chứa thông tin của khách hàng hiện tại sẽ được truyền cho Đối tác thông qua
  URL. Bằng cách thay thế login token vào placeholder <code><strong>**_loginToken_**</strong></code> trên URL do
  đối tác cung cấp
- Ví dụ:
  - LoginToken được MbApp sinh ra là: `ZmRzYWZhc2RmYQ`
  - URL đối tác cung cấp: <code>https://merchant.com/mbapp?loginToken=<strong>**_loginToken_**</strong>#ABCEDF</code>
  - URL được thêm loginToken sẽ là: <code>https://merchant.com/mbapp?loginToken=<strong>ZmRzYWZhc2RmYQ</strong>#ABCEDF</code>
- Ứng dụng WEB của Đối tác thực hiện gọi API xác minh token của hệ thống MB
  Payment Hub để xác minh token và lấy về thông tin của khách hàng hiện tại.
- Lưu ý: Đối tác chỉ nên gọi API xác minh token một lần

<!-- ## 2.2 Tích hợp phía backend
### 2.2.1 API xác minh token
#### 2.2.1.1 Thông tin chung
- API xác minh token được sử dụng để xác minh token phục vụ cho việc thiết lập phiên
làm việc của khách hàng và truy xuất thông tin cá nhân của khách hàng

#### 2.2.1.2 Phương thức kết nối
- URL: {payment_hub_base_url}/api/merchant/v1/session/verify
- Method: POST
- Input content-type: Path variable
- Output content-type: application/json

#### 2.2.1.3 Phương thức xác thực
- Sử dụng các header để xác thực như sau:
    - MERCHANT_CODE: Mã đối tác
    - MERCHANT_SECRET: Khóa bí mật của Đối tác

#### 2.2.1.4 Các trường dữ liệu input

| STT   |  Tham số  |  Kiểu dữ liệu  |  Bắt buộc | Mô tả |
|-------|--------|---------|---------|---------|
|  1 | token | Text | x | Login token từ MB App |

#### 2.2.1.5 Các trường dữ liệu output (HttpStatus 200)

| STT   |  Tham số  |  Kiểu dữ liệu  |  Mô tả |
|-------|--------|---------|---------|
|  1 | cif | Text (35) | Mã khách hàng tại MB |
|  2 | fullname | Text (255) | Họ và tên khách hàng |
|  3 | dob | Text (10) | Ngày sinh của khách hàng <br /> Theo định dạng yyyy-MM-dd (ISO 8601) |
|  4 | idCardNo | Text (20) | Mã khách hàng tại MB |
|  5 | mobile | Text (20) | Mã khách hàng tại MB |
|  6 | email | Text (100) | Mã khách hàng tại MB |

#### 2.2.1.6 Mã lỗi

<table>
  <tr>
    <th>STT</th>
    <th>Response (HttpStatus 401)</th>
    <th> Mô tả</th>
  </tr>
  <tr>
    <td>1</td>
    <td>{"code ": 401,
        "error_code": “unauthorized”,
        "error_data": null}
    </td>
    <td>Sai thông tin xác thực của Đối tác.</td>
  </tr>
</table>

<table>
  <tr>
    <th>STT</th>
    <th>Response (HttpStatus 400)</th>
    <th> Mô tả</th>
  </tr>

  <tr>
    <td>1</td>
    <td>{
        "code ": 400,
        "error_code": “invalid-param”,
        "error_data": null
        }
    </td>
    <td>Dữ liệu truyền lên không hợp lệ do thiếu tham số
hoặc sai định dạng</td>
  </tr>

   <tr>
    <td>2</td>
    <td>{
        "code ": 400,
        "error_code": “invalid-sessiontoken”,
        "error_data": null
        }
    </td>
    <td>Token truyền vào không hợp lệ hoặc đã hết hạn.</td>
  </tr>

  <tr>
    <td>3</td>
    <td>{
        "code ": 400,
        "error_code": “merchant-loginsession-sharing-disabled”,
        "error_data": null
        }
    </td>
    <td>Merchant chưa được kích hoạt tính năng chia sẻ
thông tin đăng nhập.</td>
  </tr>
</table>

- Ngoài ra các trường hợp lỗi không xác định sẽ trả về HttpStatus 500 -->
