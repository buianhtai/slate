---
title: Bank Gateway API Reference

language_tabs:
  - json


toc_footers:
  - <a href='#'>Copyright MSERVICE</a>

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
       |          |      |         -Convert SOAP webservice to REST webservice
       |          |      |         -Remove  field *commandType*, *checksum* in  request và response
       |          |      |         -Change *BankTransId* to *requestID*
       |          |      |         -Remove *BankCode* field
       |          |      |         -Change *TransId* to *referenceId*
       |          |      |         -Change *Description* to  *message*
       |          |      |         -Restructure address JSON
       |          |      |         -Remove *checkFee* field
       |          |      |         -Remove 4th topic as not require *checksum*
  

  
#	1. Introducion
    
*	Service information
    - MOMO provide API for partner integrate online payment .
    - Use RESTful web service to send and receive data as JSON. 
    - The entire request and response is encrypted using the PGP encryption software to send 
     (encrypt and sign) and receive (decrypt) (MOMO and partner must provide public key )
     
	  **Example public key**

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

*	URL : 
  -  Url Public: https://payment.momo.vn:18185/<api url path >
                <api url path> :the below lists the standard methods that have a well-defined meaning for all resources and collections.


*	Setting HTTP request headers :

Key|Values
----|------
content-type |application/pgp-encrypted 
accept |application/pgp-encrypted 
partner-code |Momo provide



    
# 2.Register
**URL** : `/api/integrate/register`

**Method** : `POST`

**Request** : `JSON Message`

**Description** : `Allow register a MOMO wallet `


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
PhoneNumber|String|1|Y|Phone number requires registration map wallet.
Fullname|String|1|Y|The full name of the account holder
PersonalId|String|1|Y|ID number of account holder
IssueDate|String|1|N|Date of issue of ID card,format  dd/MM/yyyy
IssuePlace|String|1|N| Place of issue of ID card
Address |Json|1|Y| Address of account holer
        | String   | 2| |Street	<String> : Home address of the account holder. 
        | String   | 2| |Ward	<String> : ward 
        | String   |2|  |District <String>:	District
        | String   |2|  |Province <String> :	Province
        | String   |2| |Country <String> : Country
AccountNumber|String|1|N|Bank account number
RequestId |String|1|Y|The unique transaction code generated by the partner
RequestTime|String|1|Y|Date and time of transaction with  ISO 8601 : format yyyy-MM-dd'T'HH:mm:ss'Z'


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
RequestId|String|The unique transaction code generated by the partner
ReferenceId|String|The unique transaction code on the M_Service system.
ResponseTime|String|Response time : format yyyy-MM-dd'T'HH:mm:ss'Z'
ResultCode|Int|Return code described as an appendix.
Message| String|Detailed description of the ResultCode returned.
Token|String|Character string used to identify the account when using with unregister method.

`
# 3.UnRegister
**URL** : `/api/integrate/unregister`

**Method** : `POST`

**Request** : `JSON Message`

**Description** : `Allow unregister a MOMO wallet`

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
RequestId|String|1|Y|The unique transaction code generated by the partner
RequestTime|String|1|Y|Date and time of transaction: format yyyy-MM-dd'T'HH:mm:ss'Z'
PhoneNumber|String|1|Y|Phone number requires registration map wallet.
Token|String|1|Y|The identifier string is provided in the register function.


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
RequestId|String|   The unique transaction code generated by the partner
ResponseTime|String| Response time : format yyyy-MM-dd'T'HH:mm:ss'Z'
ReferenceId|String| The unique transaction code on the M_Service system.
ResultCode|Int|Return code described as an appendix.
Message| String|    Detailed description of the ResultCode returned.

# 4	CheckAgent
**URL** : `/api/integrate/checkagent`

**Method** : `POST`

**Request** : `JSON Message`

**Description** : `Used to check wallet information`


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
RequestId|String|1|Y|The unique transaction code generated by the partner
RequestTime|String|1|Y|Date and time of transaction: format yyyy-MM-dd'T'HH:mm:ss'Z'
PhoneNumber|String|1|Y|Phone number requires registration map wallet.


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
RequestId |String| The unique transaction code generated by the partner
ReferenceId|String|The unique transaction code on the M_Service system.
ResponseTime|String| Response time : format yyyy-MM-dd'T'HH:mm:ss'Z'
ResultCode|Int|Return code described as an appendix.
Message |String|Detailed description of the ResultCode returned.
PersonalId|String|ID number of account holder
FullName|String|Account holder's name



# 5	CheckStatus
**URL** : `/api/integrate/checkstatus`

**Method** : `POST`

**Request** : `JSON Message`

**Description** : `Used to check the status of the transaction`

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
RequestId|String|1|Y|The unique transaction code generated by the partner
RequestTime|String|1|Y|Date and time of transaction: format yyyy-MM-dd'T'HH:mm:ss'Z'
PhoneNumber|String|1|Y|Phone number requires registration map wallet.
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
RequestId |String|The unique transaction code generated by the partner
ResponseTime|String| Response time : format yyyy-MM-dd'T'HH:mm:ss'Z'
ReferenceId|String|The unique transaction code on the M_Service system.
ResultCode|Int|Return code described as an appendix.
Message |String|Description .


# 6 CashIn
**URL** : `/api/integrate/cashin`

**Method** : `POST`

**Request** : `JSON Message`

**Description** : `Allow customer receive money from Bank`


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
RequestId|String|1|Y| Unique Request Identifier from partner
RequestTime| String|1|Y|  Transaction time : format yyyy-MM-dd'T'HH:mm:ss'Z'
PhoneNumber|String|1|Y| Phone Number receive money.
Amount |Long  |1|Y| Amount money transferred


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
RequestId|String|The unique transaction code generated by the partner
ResponseTime|String|Response time : Format:  yyyy-MM-dd'T'HH:mm:ss'Z'
ReferenceId|String|The unique transaction code on the M_Service system.
ResultCode|Int|Return code described as an appendix.
Message |String|Detailed description of the ResultCode returned.
