# 用户登录/注册

## 用户登录

### URL
/user/login/login/

### HTTP请求方式
__POST JSON__

要求数据格式为JSON

### HTTP请求参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
code			     		| String 				| 小程序产生的code

### HTTP响应参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_sid			  	| String 				| 16位会话ID
state						| Bool				| 用户注册状态
result					| Int					| 登录结果

### API 注释

__state__ 为0表示改用户没有绑定手机号码，为1表示该用户已经绑定手机号码

result含义：

值		|意义
--------|--------
200		|请求成功
401		|微信接口出错
500		|未知错误

### 示例

__请求__

```json
{
    "data": {
        "code": "021SUt8Z0zy8312J2l6Z0sEH8Z0SUt8p"
    }
}
```
__响应__

```json
{
    "version": "0.1",
    "response": {
        "user_sid": "408c485e-f138-11e8-b539-6c96cfdf6ce7",
        "state": 1,
        "result": 200
    },
    "context": null
}
```
-------------------------------
## 用户提交手机号获取验证码

### URL
/user/login/submit_pn/

### HTTP请求方式
__POST JSON__

要求数据格式为JSON


### HTTP请求参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
pn			     		| String 				| 手机号
user_sid			  	| String 				| 16位会话ID


### HTTP响应参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_sid			  	| String 				| 16位会话ID
pn			     		| String 				| 手机号
sid                     | String                | 16位会话ID
result					| Int					| 提交结果

### API 注释

__sid__ 不同于 __user_sid__, __sid__ 生命周期短，用户注册后或几分钟后销毁

result含义：

result取值含义：

值		|意义
--------|--------
200		|手机号提交成功
400		|请求格式有误
401		|手机号错误
500		|未知错误

### 示例

__请求__

```json
{
	"data":{
		"pn": "13800138000",
		"user_sid": "e33a7f38-f135-11e8-b30f-6c96cfdf6ce7"
	}
}
```
__响应__

```json
{
    "version": "0.1",
    "response": {
        "user_sid": "e33a7f38-f135-11e8-b30f-6c96cfdf6ce7",
        "pn": "13800138000",
        "result": 200,
        "sid": "SID_03d22557-f137-11e8-a8d6-6c96cfdf6ce7"
    },
    "context": null
}
```

-------------------------------------------

## 用户提交验证码

### URL
/user/login/validate/

### HTTP请求方式
__POST JSON__

要求数据格式为JSON


### HTTP请求参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
pn			     		| String 				| 手机号
user_sid			  	| String 				| 16位会话ID
sid                     | String                | 16位会话ID
vcode                   | String                | 6位验证码


### HTTP响应参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_sid			  	| String 				| 16位会话ID
pn			     		| String 				| 手机号
result					| Int					| 验证结果

### API 注释


result含义：

值		|意义
--------|--------
200		|请求成功
401		|验证错误
404		|未找到sid，sid可能已过期
409		|pn与sid冲突
500		|未知错误

### 示例

__请求__

```json
{
    "data": {
	"pn": "13800138000",
	"sid": "SID_03d22557-f137-11e8-a8d6-6c96cfdf6ce7",
	"vcode": "123456",
	"user_sid": "e33a7f38-f135-11e8-b30f-6c96cfdf6ce7"
    }
}
```
__响应__

```json
{
    "version": "0.1",
    "response": {
        "user_sid": "e33a7f38-f135-11e8-b30f-6c96cfdf6ce7",
        "pn": "13800138000",
        "result": 200
    },
    "context": null
}
```

-------------------------------------------------

## 用户注销登录

### URL
/user/login/logout/

### HTTP请求方式
__GET__

要求数据格式为JSON


### HTTP请求参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_sid			  	| String 				| 16位会话ID


### HTTP响应参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
result					| Int					| 注销结果

### API 注释


result含义：

值		|意义
--------|--------
200		|请求成功
404		|user_sid不存在或者已过期

### 示例

__请求__

/user/login/logout/?user_sid=e33a7f38-f135-11e8-b30f-6c96cfdf6ce7


__响应__

```json
{
    "version": "0.1",
    "response": {
        "reason": "user_id do not exist",
        "result": 404
    }
}
```

# 本页版本信息

## 版本号

0.1.0

## 上次更新时间

2018-11-26