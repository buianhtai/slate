# 7.Response code detail


<aside class="notice">.Thông tin chi tiết bảng mã lỗi trả về của API</aside>


 Response code(Integer) | Description(String) | Mô tả bằng tiếng việt(String)
---------- | ----------  | ----------
0    | Success                                  |   Thành công
-1   |	"Fail"                                  |   Thất bại
1    |"Invalid signature"                       |   Chữ ký không hợp lệ
2    |	"Can't decrypt message"                 |   Không thể giải mã thông tin
3    |"Invalid username"                        |   Tên giao dịch không hợp lệ
4    | 	"Invalid walletId"                      |   Mã WalletId không không hợp lệ
5    |	"Invalid password"                      |   Mật khẩu không hợp lệ
6    |	invalid json string format              |   Chuỗi json không hợp lệ
7    |	"Insufficient funds"                    |   Không đủ tiền giao dịch.
8    |	"Duplicate request id"                  |   Trùng requestId
9    |	"Invalid partner code"                  |   Mẫ đối tác không hợp lệ
10   |	"Unknown result. Please check manual to get final result"|  Lỗi không xác định.
11   |	"Other Error"                           |   Lỗi khác
400  |	"The account doesn't exist in M_Service system"             |   Tài khoản không tồn tại trong hệ thống M_Service
401  |	"The account has been already registered with another bank" |   Tài khoản đẵ đăng ký với ngân hàng khác
402  |	"The account has been already registered with this bank"    |   Tài khoản đã đăng ký với ngân hàng
403  |	"The account is not registered with any bank"               |   Tài khoản chưa đăng ký với ngân hàng
404  |	"The account is inactive"                                   |   Tài khoản ngưng hoạt động
405  |	"IdNumber is already registered for 3 wallet")              |   IdNumber đã được đăng ký cho 3 ví
406  |	"The Transaction is timeout"                                |   Giao dịch vượt quá thời gian.
407  |	"Over limited transaction per day"                          |   Vượt qua số giao dịch giới hạn trong ngày.
408  |	"Amount is invalid"                                         |   Số tiền không hợp lệ
409  |	"The service is upgrading"                                  |   Dịch vụ đang được nâng cấp
410  |	"Invalid Parameters: %s"                                    |   Các tham số không hợp lệ.
411  |	"Wallet Balance Exceeded"                                   |   Vượt quá số dư trong Ví.
412  |	"ChannelCode is invalid"                                    |   Kênh dịch vụ không hợp lệ.
413  |	"Balance over limit"                                        |   Số dư vượt giới hạn.
414  |	"Invalid payment token or payment token is linked with other phoneNumber"|  Mã thanh toán không đúng hoặc mã thanh toán được liên kết với số điện thoại khác.
415  |	"Invalid date format"                                       |   Thời gian không hợp lệ.
416  |	"Amount is pending or on process. Please finish the previous transaction"|  Số tiền đang chờ xử lí. Vui lòng hoàn thành các giao dịch trước đó.
417  |	"Invalid reference Id"                                      |   Số tham chiếu không hợp lệ
418  |	"Otp timeout"                                               |   OTP hết hiệu lực
419  |	"Bank offline"                                              |   Dịch vụ ngừng hoạt 
420  |	"DB error"                                                  |   Lỗi DB
421  |	"Enable Wallet Exists"                                      |   Cho phép không cần tạo ví
422  |	"Transaction not complete"                                  |   Giao dịch chưa hoàn tất
423	 |"Internal Error"                                              |   Dịch vụ  bị lỗi.
424  | "Invalid request Id"                                         |   RequestId không hợp lệ.
425  | "Invalid encrypt data"                                       |   Chuỗi mã hoá không hợp lệ.
