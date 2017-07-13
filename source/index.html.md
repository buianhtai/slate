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

    Sử dụng RESTful API để gửi và nhận dữ liệu dưới dạng JSON. 
	Dữ liệu request và response đều sẽ được mã hóa (Momo sẽ cung cấp cho đối tác key cần thiết )

*	Url kết nối (từ phía đối tác sang Momo )

    Url Public: https://payment.momo.vn:18185/<api url path >
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
