#Tomin Single Sign On Server API

###These APIs are usually used for registring or changeing user info by relay parties(EC`IM...etc).The most data format is defined in the [link](http://openid.net/specs/openid-connect-core-1_0.html#StandardClaims),but we still need to add some custom data(like pwd,seed) for some reqirement(like authentication) when using these APIs. 
### 這些API一般是給RP(像EC IM...)用在註冊或是更換使用者資料時使用，大部份的資料規格都是參照此[連結](http://openid.net/specs/openid-connect-core-1_0.html#StandardClaims),不過當我們使用這些API時仍需要為了特定需求(如認證)而需加入一些特定的資料(像pwd,seed)


####API root URL : http://sso.tomin.tw:550/TominOP/oidc
 
 
##verifymember

| API Path | 
| ------ | 
| /verifymember |

| Description|
| ------ |
| SSO中,Subject指的就是會員帳號ID,此API是用來檢查此會員帳號是否已存在，通常是用在RP的註冊流程上|
| In the SSO, Subject is mean the member account ID , so the API is for Checking the subject is exists.Always using in the registry step.|

Input Data Type: x-www-form-unlencoded

| Parameters| Attributes |description|
| --- | --- | --- |
| subject| (required)String | member account ID|

Result:

| JSON key |  description |
| --- | --- |
| ret_code |	The back state code which we defined |  

JSON Content Define:

| ret_code |  ret_description |
| --- | --- |
| 0 |	Without the subject 
| 1 |	The subject is exists  | 

Return example:

{
  "ret_code" : 0
}



##register

| API Path | 
| ------ | 
| /register |

| Description|
| ------ |
| 註冊新使用者 |
| Registring new User	|


Input Data Type: JSON

| Parameters| Attributes |description|
| --- | --- | --- |
| sub | (required)String | Subject - Identifier for the End-User at the Issuer|
| pwd | (required)String | The password encrypt string with seed by AES ( Key Format : ddHHssMMddHHssMM ) |
| seed | (required)String | The AES key which is the timestamp when registering( Format : yyyyMMddHHmmss )|

1.	These 3 parameter data is must required when registring.The other parameter's properties are all optional,their detail format is reference by 
here : [link](http://openid.net/specs/openid-connect-core-1_0.html#StandardClaims)

Result:

| JSON key |  description |
| --- | --- |
| ret_code |	The back state code which we defined | 
| ret_description |	The state's detail description  | 

JSON Content Define:

| ret_code |  ret_description |
| --- | --- |
| 200 |	Register Successful| 
| 201 |	Without ClientID | 

Return example:

{

  "ret_code" : 200,

  "ret_description" : "Register Successful"

}

##updatemember

| API Path | 
| ------ | 
| /updatemember |

| Description|
| ------ |
| 更新指定使用者資料(名字｀電話｀Email`密碼....等) |
| Updating target user data(name phone email pwd ...etc)|


Input Data Type: JSON

| Parameters| Attributes |description|
| --- | --- | --- |
| sub | (required)String | Subject - Identifier for the End-User at the Issuer| 

1. The sub parameter data is must required when registring.The other parameter's properties are all optional,their detail format is reference by 
	here : [link](http://openid.net/specs/openid-connect-core-1_0.html#StandardClaims)

2.	The pwd & seed must change together.

Result:

| JSON key |  description |
| --- | --- |
| ret_code |	The back state code which we defined | 
| ret_description |	The state's detail description  | 

state_code Define:


| ret_code |  ret_description |
| --- | --- |
| 200 |	Update Successful| 
| 201 |	Without ClientID | 
 
 Return example:

{

  "ret_code" : 200,

  "ret_description" : "Update Successful"

}


