# Response code detail


<aside class="notice">.Thông tin chi tiết bảng mã lỗi trả về của API</aside>


7. Response code(Integer) | Description(String) | Mô tả bằng tiếng việt(String)
---------- | ----------  | ----------
0 | Success | Thành công
01|Invalid Username / Password. | Tài khoản / Mật khẩu không đúng.
02|Invalid  DataSign. | DataSign không đúng. 
03| The account doesn’t exist in M_Service system. | Tài khoản không tồn tại trong hệ thống M_Service
04|The account has been already registered with another bank.|Tài khoản đã được đăng kí với ngân hàng khác. 
05|The account has been already registered with this bank.|Tài khoản đã được đăng kí với ngân hàng. 
06|The account is not registered with any bank.|Tài khoản chưa được đăng kí với bất kì ngân hàng nào.
07|The password can’t be decrypted.|Mật khẩu không được giải mã.
09|IdNumber is already registered for 3 wallet.|IdNumber đã được đăng ký cho 3 ví
10|The SessionId is expired.|Phiên làm việc đã hết hạn.
11|The Transaction is timeout.|Giao dịch vượt quá thời gian.
12|Over limited transaction per days.|Vượt qua số giao dịch giới hạn trong ngày.
13|Amount is invalid.|Số tiền không hợp lệ.
14|Duplicate TransId.|Giao dịch  bị trùng.
15|The service is upgrading.|Dịch vụ đang được nâng cấp.
16|Invalid Parameters.|Các tham số không hợp lệ.
17|Insufficient funds|Không đủ tiền giao dịch.
18|Wallet Balance Exceeded|Vượt quá số dư trong Ví.
19|ChannelCode is invalid|Kênh dịch vụ không hợp lệ.
20|Balance over limit|Số dư vượt giới hạn.
21|Invalid payment token or payment token is linked with other phoneNumber|Mã thanh toán không đúng hoặc mã thanh toán được liên kết với số điện thoại khác.
22|Invalid date format|Thời gian không hợp lệ.
23|Amount is pending or on process. Please finish the previous transaction|Số tiền đang chờ xử lí. Vui lòng hoàn thành các giao dịch trước đó.
30|Webservice Error|Dịch vụ  bị lỗi.

