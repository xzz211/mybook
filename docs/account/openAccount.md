# 开通余额账户

#### 接口地址

```
POST ：http://{{mswallet}}/V9/wallet/api/account/generalBalanceOpen
```



#### 接口说明

1. 企业开户和余额开户共用一个接口

2. 兼容老的所有接口

3. 支持功能

   1. 通过已经绑定的银行卡开通
   2. 新卡开通
4. 开户状态描述

   1. 余额账户状态：

      - 1-开户资料已提交
      - 21-短信验证通过
      - 41-待打款认证
      - 2-开户成功
      - 22-开户失败

   2. 账户状态

      - true：（2-开户成功；41-待打款认证）

      - false：（1-开户资料已提交；21-短信验证通过；22-开户失败）

      能否重新开户标准：

      　　账户状态为true不可重新开户，账户状态为false，且余额账户状态为21-短信验证通过，不可重新开户；其他情况可重新开户

#### 入参

| **序号** | **参数名**        | **类型** | **是否必须** | **描述**               |
| :------: | :---------------- | :------: | :----------: | ---------------------- |
|    1     | type              |  String  |      是      | 注册类型 1-个人 5-企业 |
|    2     | uid               |   Long   |      否      | 用户ID                 |
|    3     | projectId         |  String  |      否      | 项目ID                 |
|    4     | personalOpenReq   |  object  |      否      | 个人开户必填           |
|    5     | enterpriseOpenReq |  object  |      否      | 企业开户必填           |

##### 个人开户：

| **序号** | **参数名**     | **类型** | **是否必须**  | **描述**                                            | **示例**                                                     |
| -------- | -------------- | -------- | ------------ | --------------------------------------------------- | ------------------------------------------------------------ |
| 4.1      | foreverFlg | boolean|<div style="width: 30pt">否 </div>|<div style="width: 80pt"> 证件是否长期有效</div> | true/false |
| 4.2      | expirationDate | String   | 否           | 证件到期日 foreverFlg为false时需填写 格式：YYYYMMDD |                                                              |
| 4.3      | cardId         | Long     | 否           | 绑定的银行卡sid。此参数不为空，下面参数不用传       |                                                              |
| 4.4      | name           | String   | 否           | 姓名，cardId不为空时必传                            |                                                              |
| 4.5      | certType       | String   | 否           | 证件类型，只支持身份证类型，可不传                  |                                                              |
| 4.6      | certNo         | String   | 否           | 证件号码，cardId不为空时必传                        |                                                              |
| 4.7      | mobile         | String   | 否           | 手机号，cardId不为空时必传                          |                                                              |
| 4.8      | bankCode       | String   | 否           | 银行编码，cardId不为空时必传                        | 先根据获取银行信息列表接口（http://{{mswallet}}/V4/wallet/api/dictionary/findAll) 获取所有的银行信息，以供用户选择对应银行。用户选择银行后，将该银行对应的code作为本接口的银行编码入参。 |
| 4.9      | bankCardNo     | String   | 否           | 银行卡号，cardId不为空时必传                        | . |

##### 企业开户：

| **序号** | **参数名**      | **类型** | **是否必须** | **描述**                                            | **示例**                                                     |
| -------- | --------------- | -------- | ------------ | --------------------------------------------------- | ------------------------------------------------------------ |
| 5.1      | name            | String   | 是           | 企业名称                                            |                                                              |
| 5.2      | englishName     | String   | 否           | 企业英文名 默认：NoEnglishName                      |                                                              |
| 5.3      | certNo          | String   | 是           | 统一信用社会代码                                    |                                                              |
| 5.4      | bankCode        | String   | 是           | 银行编码。                                          | 先根据获取银行信息列表接口（http://{{mswallet}}/V4/wallet/api/dictionary/findAll 获取所有的银行信息，以供用户选择对应银行。用户选择银行后，将该银行对应的code作为本接口的银行编码入参。 |
| 5.5      | bankCardNo      | String   | 是           | 绑定银行的对公账户                                  |                                                              |
| 5.6      | legalName       | String   | 是           | 法人姓名                                            |                                                              |
| 5.7      | legalCertNo     | String   | 是           | 法人身份证号                                        |                                                              |
| 5.8      | legalForeverFlg | boolean  | 是           | 法人证件长期有效标识                                |                                                              |
| 5.9      | legalExpireDate | String   | 否           | 法人证件到期时间:forever_flag为false时必输 YYYYMMDD |                                                              |
| 5.10     | legalMobile     | String   | 是           | 法人手机号                                          |                                                              |
| 5.11     | operName        | String   | 是           | 经办人姓名                                          |                                                              |
| 5.12     | operCertNo      | String   | 是           | 经办人身份证号                                      |                                                              |
| 5.13     | operMobile      | String   | 是           | 经办人手机号                                        |                                                              |

##### 入参示例：

```json
{
  "type": "",
  "uid": 0,
  "projectId": "",
  "personalOpenReq": {
    "cardId": 0,
    "name": "",
    "certType": "",
    "certNo": "",
    "foreverFlg": false,
    "expirationDate":"",
    "mobile": "",
    "bankCode": "",
    "bankCardNo": ""
  },
  "enterpriseOpenReq": {
    "name": "",
    "englishName": "",
    "certNo": "",
    "bankCode": "",
    "bankCardNo": "",
    "legalName": "",
    "legalCertNo": "",
    "legalForeverFlg": false,
    "legalExpireDate":"",
    "legalMobile": "",
    "operName": "",
    "operCertNo": "",
    "operMobile": ""
  }
}
```

##### 出参：

公共参数

| **序号** | **参数名**    | **类型** | **是否必须** | **描述**                         |
| -------- | ------------- | -------- | ------------ | -------------------------------- |
| 1        | statusCode    | String   | 是           | 业务处理结果编码。 0为处理成功。 |
| 2        | statusMessage | String   | 否           | 业务处理结果编码描述             |
| 3        | data          | Object   | 否           | 个性化业务返回对象               |

私有参数

| **序号** | **参数名**       | **类型**                  | **是否必须** | **描述**         |
| -------- | ---------------- | ------------------------- | ------------ | ---------------- |
| 1        | openFlowNo       | String                    | 是           | 开户业务流水号   |
| 2        | openStatus       | String                    | 是           | 开户状态         |
| 3        | openStatusDesc   | String                    | 是           | 开户状态描述     |
| 4        | smsSendNo        | String                    | 是           | 短信验证码编号   |
| 5        | acctNo           | String                    | 是           | 开户账号         |
| 6        | extAcctNo        | String                    | 否           | 外部账号         |
| 7        | activeStatus     | String                    | 否           | 激活状态         |
| 8        | activeStatusDesc | String                    | 否           | 激活状态描述     |
| 9        | amount           | String                    | 否           | 打款认证金额     |
| 10       | activeLastTime   | String                    | 否           | 最后打款日期     |
| 11       | imageFiles       | List*<*UploadImageFile*>* | 否           | 上传影音文件信息 |
| 11.1     | code             | String                    | 否           | 影音文件类型     |
| 11.2     | desc             | String                    | 否           | 影音文件描述     |