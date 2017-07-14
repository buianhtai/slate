---
title: Bank Gateway API Reference

language_tabs:
  - json


toc_footers:
  - <a href='#'>Bản quyền thuộc về MSERVICE</a>

includes:
  - errors

search: true
---

# Momo Bank Gateway 
## Technical Integration Document v2.0

  Version |Date |Author |Description 
  -----|-----------|--------------------|-------------------------------
  1.0  |12-06-2017|Tranh |Created 
  2.0  |23-06-2017|Tranh | 
       |          |      |         -Đối ứng bank gateway mới. Sử dụng Restful API 
       |          |      |         -Bỏ field commandType và checksum trong request và response
       |          |      |         -BankTransId thành requestID
       |          |      |         -Bỏ BankCode
       |          |      |         -TransId đổi thành referenceId 
       |          |      |         -Description đổi thành message 
       |          |      |         -Cấu trúc json của register 
       |          |      |         -Bỏ checkFee 
       |          |      |         -Bỏ mục 4 vì không cần checkSum 
  

  
#	1. Giới thiệu chung 
    
*	Thông tin dịch vụ
    - Sử dụng RESTful API để gửi và nhận dữ liệu dưới dạng JSON. 
	- Dữ liệu request và response đều sẽ được mã hóa (Momo sẽ cung cấp cho đối tác key cần thiết )
	
	  **Ví dụ public key**
	  
```json
            -----BEGIN PGP MESSAGE-----
              Version: PGP Personal Security 7.0.3
              qANQR1DBwk4DepqGz+tv7awQC/sGOyvgkqLDEz3QOc4AkDuoTVl9O2y7X260NR47
              w77OngPn3z/01yEpVDmkfrpdXKYmVhylICPg1yvNYTyx6EW5LIOYt1yuxLc+bjKS
              piwrBdCxz5+VT8z9IQz7BNu75GBP5YMJyhZUgwFRDahPITz0ziqL9nBZeUX27PGL
              ZIc32bm/18zLwbLUZi4CSPlnc9PzXTeubwnsaC0ZU1PT+WokkhPRxPrgBHLU/rMj
              zqOoh2/dXGMUFY7F0zitGw1jcj+jIf49hpzPZ5oWChZQjnQdREZgaRenx3jRomol
              BnT0KgGk+cBp8BIM65DyoYdMKE878n+ngTgIYUYkBLnYXfQv9pgagPlQUgmMWSK/
              zRkLS3PpKJFTv629iBXKKDeCteqD4668TRty3N1sEXaFbpMZtaNWJvqlXpbbrAkO
              rvKAxMq9gpA+asf6415NSX29FT4uv4D7FWF3fp2e9it8c30//9yKXQ8pJb0vfz8B
              vZCwIO1me371DScIwI2D8/8EHzQMALxye7O/tpDW3BEU+NEqsHM2nXdebKl7mPk8
              5voUyYZb3vz3PQHNJ+Jg14KybK8Jn7KGji19nHFgFtHN0Qoz4e5aTlZtMksWDaX+
              dT6xfrKBo5wOaQHGAX3NHBAMTCqUoZajsGxsc+dQ/WB7Qw4qdZjmLtzj35HcF7s0
              5RwOWZ2F9cqSj0b994llaT9zo2jXs5ZM/fAZUBPsCp55EFpe52NFKJgyJY92mYi0
              1SK26VMNMdHdp4zHWZdNkhPPG0EgDsz1g+EtY6YXWQYwIKPnQUivf5mhDdhPmWK6
              sAR4D7s2Vgqs2gQnvuFxpkDMc5l2rMTAE5+x228SpMPau27BDxBDKLw1i6ak23C+
              l2qmiqQg0qeSFy2o7+HmyKWCENl2V84N8eLhoE+iyXj5fL2UvMlqVJePTT76Rz6p
              +tD/15JYZo/8uAxIBivaB7P7k2Bqu0bmrCD4wdSKOLzhScxAj15Dtu0kWgEKGs80
              VgTMu2iQLtphN7oObhWzUIf9O3MlqMnBCiOp4VFGebnJcDvullUB4OYZD6ZLIecN
              8BsqsVlqawJbtWpmRf8973Yg2bicP0ISCwFaoDvR8C+wb3h9nJ9EZeO/mZGjJweR
              A6yXK7wyp6JHnvACwFhUkTno7nrdq8cDaG4ssolsUSKnON87ycLFWq/mNs9fhqzF
              Y3y7Q4f7hA4EL83+bxc4YGqzirWHeVXetZdft018+0Oz2Au8gRG5AVd+DX+xlr56
              mJlkrlzYWG7HuEl8CRS7rAZHgRAIV3I7WDeNEYyBQNt/MfzUQY9+BmbtCsTlOnda
              j8IkiL0QIW/9ZyvifxpvzKGKhxdXoqJWVSXLKHGk1qvY9epgw7QWk15crlti0Q4+
              aDXvNieN9imk3UNQe2rncqzIKlbxasjparCKXiErQGFjldtTLrZcf7KjNOJuVG9J
              HoOZC39ur8rkVrgWuSzrvzhpeQl0VlmdviZpocErZYPtnDQGgA3TbXX4lXoMiM1a
              bOxTskUcgIBzN2L9nNfIhVaxJxMd3260SpJxElJ27V6Be97Q+YX4TF9xlH4zWFM3
              NpGg1iXWNRb4VSwPE2+ZEiKirrlMsgXxfZNvAy3bAuSm0b1u7Isa/Jjab96DHff6
              5g5K
              =WRFH
        -----END PGP MESSAGE----- 
```
            
*	Url kết nối (từ phía đối tác sang Momo )
    -Url Public: https://payment.momo.vn:18185/<api url path >
                <api url path> : xem chi tiết trong mục 2 cột Path.

*	Thiết lập giá trị trong header trong mỗi request như sau :

Key|Values
----|------
content-type |application/pgp-encrypted 
accept |application/pgp-encrypted 
partner-code |Momo sẽ cung cấp cho đối tác 



    
# 2.Register
**URL** : `/api/integrate/register`

**Method** : `POST`

**Request** : `JSON Message`

**Description** : `Dùng để đăng ký tài khoản MOMO `


## 2.1 Request Field

```json
   {
     "phoneNumber": "<PhoneNumber>",
     "fullName": "<Fullname>",
     "personalId": "<PersonalId>",
     "issueDate": "<IssueDate>",
     "issuePlace": "<IssuePlace>",
     "address": {
       "street": "<Street>",
       "ward": "<Ward>",
       "district": "<District>",
       "province": "<Province>",
       "country": "<Country>"
     },
     "accountNumber": "<AccountNumber>",
     "requestId": "<RequestId>",
     "requestTime": "<RequestTime>"
   }
```

Field     |Type   |Level|Require|Description
----------|-------|-----|-------|----------------
PhoneNumber|String|1|Y|Số điện thoại yêu cầu đăng ký map ví.
Fullname|String|1|Y|Tên đầy đủ của chủ tài khoản
PersonalId|String|1|Y|Số CMND của chủ tài khoản
IssueDate|String|1|N|Ngày cấp , Định dạng  dd/MM/yyyy
IssuePlace|String|1|N|Nơi cấp
Address |Json|1|Y| Địa chỉ
        | String   | 2| |Street	<String> : Địa chỉ nhà
        | String   | 2| |Ward	<String> : Phường
        | String   |2|  |District <String>:	Quận/Huyện
        | String   |2|  |Province <String> :	Thành phố /tỉnh
        | String   |2| |Country <String> : Quốc gia 
AccountNumber|String|1|N|Số tài khoản ngân hàng
RequestId |String|1|Y|Mã giao dịch duy nhất trên hệ thống đối tác do đối tác sinh ra
RequestTime|String|1|Y|Ngày giờ thực hiện giao dịch chuẩn ISO 8601 : format yyyy-MM-dd'T'HH:mm:ss'Z'


## 2.2 Response Field
```json
       {
              "requestId": "<RequestId>",
              "referenceId": "<ReferenceId>",
              "responseTime": "<ResponseTime>",
              "resultCode": "<ResultCode>",
              "message ": "<Message>",
              "token": "<Token>"
       }
```
Field|Date Type|Description
---------- | ----------  | -------------
RequestId|String|Mã giao dịch duy nhất trên hệ thống đối tác do đối tác sinh ra
ReferenceId|String|Mã giao dịch duy nhất trên hệ thống của M_Service.
ResponseTime|String|Ngày giờ giao dịch của Mservice:
            |      |  Format:  yyyy-MM-dd'T'HH:mm:ss'Z'
ResultCode|Int|Mã trả về. Được mô tả như trong phần phụ lục.
Message| String|Mô tả chi tiết về ResultCode trả về.
Token|String|Chuỗi để xác định tài khoản khi sử dung lệnh checkFee

`
# 3.UnRegister
**URL** : `/api/integrate/unregister`

**Method** : `POST`

**Request** : `JSON Message`

**Description** : `Dùng để huỷ đăng ký ví`


## 3.1 Request Field

```json
{
  "requestId": "<RequestId>",
  "requestTime": "<RequestTime>",
  "phoneNumber": "<PhoneNumber>",
  "token": "<Token>"
}
```

Field     |Type   |Level|Require|Description
----------|-------|-----|-------|----------------
RequestId|String|1|Y|Mã giao dịch duy nhất trên hệ thống đối tác do đối tác sinh ra
RequestTime|String|1|Y|Ngày giờ thực hiện giao dịch: format yyyy-MM-dd'T'HH:mm:ss'Z'
PhoneNumber|String|1|Y|Số điện thoại yêu cầu đăng ký map ví.
Token|String|1|Y|Chuỗi định danh được cung cấp trong hàm register


## 3.2 Response Field
```json
{
  "requestId": "<RequestId>",
  "responseTime": "<ResponseTime>",
  "referenceId": "<ReferenceId>",
  "resultCode": "<ResultCode>",
  "message ": "<Message>"
}
```

Field|Date Type|Description
---------- | ----------  | -------------
RequestId|String|   Mã giao dịch duy nhất trên hệ thống đối tác do đối tác sinh ra
ResponseTime|String| Ngày giờ trả thông tin: format yyyy-MM-dd'T'HH:mm:ss'Z'
ReferenceId|String| Mã giao dịch duy nhất trên hệ thống của M_Service.
ResultCode|Int|Mã trả về. Được mô tả như trong phần phụ lục.
Message| String|    Mô tả chi tiết về ResultCode trả về.

# 4	CheckAgent
**URL** : `/api/integrate/checkagent`

**Method** : `POST`

**Request** : `JSON Message`

**Description** : `Dùng để kiểm tra thông tin ví`


## 4.1 Request Field

```json
{
  	   "requestId": "<RequestId>",
       "requestTime": "<RequestTime>",
       "phoneNumber": "<PhoneNumber>"
}

```

Field     |Type   |Level|Require|Description
----------|-------|-----|-------|----------------
RequestId|String|1|Y|Mã giao dịch duy nhất trên hệ thống đối của Mservice
RequestTime|String|1|Y|Ngày giờ thực hiện giao dịch: format yyyy-MM-dd'T'HH:mm:ss'Z'
PhoneNumber|String|1|Y|Số điện thoại yêu cầu đăng ký map ví.


## 4.2 Response Field
```json
{
  "requestId": "<RequestId>",
  "referenceId": "<ReferenceId>",
  "responseTime":"<ResponseTime>",
  "resultCode": <ResultCode>,
  "message": "<Message>",
  "personalId": "<PersonalId>",
  "fullName": "<FullName>"
}
```

Field|Date Type|Description
---------- | ----------  | -------------
RequestId |String| Mã giao dịch duy nhất trên hệ thống đối tác do đối tác sinh ra
ReferenceId|String|Mã giao dịch duy nhất trên hệ thống của M_Service.
ResponseTime|String| Ngày giờ trả thông tin: format yyyy-MM-dd'T'HH:mm:ss'Z'
ResultCode|Int|Mã trả về. Được mô tả như trong phần phụ lục.
Message |String|Mô tả chi tiết về ResultCode trả về.
PersonalId|String|Số CMND của chủ tài khoản
FullName|String|Tên của chủ tài khoản



# 5	CheckStatus
**URL** : `/api/integrate/checkstatus`

**Method** : `POST`

**Request** : `JSON Message`

**Description** : `Dùng để kiểm tra trạng thái giao dịch

## 5.1 Request Field

```json
    {
      "requestId": "<RequestId>",
      "requestTime": "<RequestTime>",
      "phoneNumber": "<PhoneNumber>",
      "checkedRequestId":"<CheckedRequestId>"
    }

```


Field     |Type   |Level|Require|Description
----------|-------|-----|-------|----------------
RequestId|String|1|Y|Mã giao dịch duy nhất trên hệ thống đối của Mservice
RequestTime|String|1|Y|Ngày giờ thực hiện giao dịch: format yyyy-MM-dd'T'HH:mm:ss'Z'
PhoneNumber|String|1|Y|Số điện thoại yêu cầu đăng ký map ví.
CheckedRequestId|String|1|Y|RequestId của request cashin (chuyển tiền vào ví), 



## 5.2 Response Field
```json
{
  "requestId": "<RequestId>",
  "responseTime":"<ResponseTime>",
  "referenceId": "<ReferenceId>",
  "resultCode": <ResultCode>,
  "message": "<Message>"
}
```

Field|Date Type|Description
---------- | ----------  | -------------
RequestId |String|Mã giao dịch duy nhất trên hệ thống đối tác do đối tác sinh ra
ResponseTime|String| Ngày giờ trả thông tin: format yyyy-MM-dd'T'HH:mm:ss'Z'
ReferenceId|String|Mã giao dịch duy nhất trên hệ thống của M_Service.
ResultCode|Int|Mã trả về. Được mô tả như trong phần phụ lục.
Message |String|Mô tả chi tiết về ResultCode trả về.


# 6 CashIn
**URL** : `/api/integrate/cashin`

**Method** : `POST`

**Request** : `JSON Message`

**Description** : `Dùng để nạp tiền vào ví MOMO`


## 6.1 Request Field

```json
    {
      "requestId": "<RequestId>",
      "requestTime": "<RequestTime>",
      "phoneNumber": "<PhoneNumber>",
      "amount": <Amount>
    }
```
Field     |Type   |Level|Require|Description
----------|-------|-----|-------|----------------
RequestId|String|1|Y| Mã giao dịch duy nhất trên hệ thống đối tác do đối tác sinh ra
RequestTime| String|1|Y|  Ngày giờ thực hiện giao dịch: format yyyy-MM-dd'T'HH:mm:ss'Z'
PhoneNumber|String|1|Y| Số ví yêu cầu chuyển tiền đến.
Amount |Long  |1|Y| Số tiền 


## 6.2 Response Field
```json

{
  "requestId": "<RequestId>",
  "responseTime":"<ResponseTime>",
  "referenceId": "<Message>",
  "resultCode": <ResultCode>,
  "message": "<Message>"
}
```



Field|Date Type|Description
---------- | ----------  | -------------
RequestId|String|Mã giao dịch duy nhất trên hệ thống đối tác do đối tác sinh ra
ResponseTime|String|Ngày giờ trả kết quả giao dịch: Format:  yyyy-MM-dd'T'HH:mm:ss'Z'
ReferenceId|String|Mã giao dịch duy nhất trên hệ thống của M_Service.
ResultCode|Int|Mã trả về. Được mô tả như trong phần phụ lục.
Message |String|Mô tả chi tiết về ResultCode trả về.
