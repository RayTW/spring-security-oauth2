密碼模式: Resource Owner Password Credentials Grant
---

密碼模式（Resource Owner Password Credentials Grant）中，用戶向客戶端提供自己的用戶名和密碼。客戶端使用這些信息，向"服務商提供商"索要授權。

在這種模式中，用戶必須把自己的密碼給客戶端，但是客戶端不得儲存密碼。這通常用在用戶對客戶端高度信任的情況下，比如客戶端是操作系統的一部分，或者由一個著名公司出品。而認證服務器只有在其他授權模式無法執行的情況下，才能考慮使用這種模式。

![](../static/password_grant.png)

它的步驟如下：
> * （A）用戶向客戶端提供用戶名和密碼。
> * （B）客戶端將用戶名和密碼發給認證服務器，向後者請求令牌。
> * （C）認證服務器確認無誤後，向客戶端提供訪問令牌。

B步驟中，客戶端發出的HTTP請求，包含以下參數：
* grant_type：表示授權類型，此處的值固定為"password"，必選項。
* username：表示用戶名，必選項。
* password：表示用戶的密碼，必選項。
* scope：表示權限範圍，可選項。
下面是一個例子。
```
     POST /token HTTP/1.1
     Host: server.example.com
     Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
     Content-Type: application/x-www-form-urlencoded

     grant_type=password&username=johndoe&password=A3ddj3w
```

C步驟中，認證服務器向客戶端發送訪問令牌，下面是一個例子。
```
     HTTP/1.1 200 OK
     Content-Type: application/json;charset=UTF-8
     Cache-Control: no-store
     Pragma: no-cache

     {
       "access_token":"2YotnFZFEjr1zCsicMWpAA",
       "token_type":"example",
       "expires_in":3600,
       "refresh_token":"tGzv3JOkF0XG5Qx2TlKWIA",
       "example_parameter":"example_value"
     }
```

整個過程中，客戶端不得保存用戶的密碼。

# 實際應用

**1. 獲取access_token**

`POST`請求：
```
http://localhost:8080/oauth/token
```

`Content-Type: application/x-www-form-urlencoded`

`Authorization`:

參數名稱 | 參數值 | 參數說明
---|--- |---
Username | clientapp | 放在Authorization, 客戶端的用戶名
Password | 123456 | 放在Authorization, 客戶端的密碼

`Parameters`:

參數名稱 | 參數值 | 參數說明
---|--- |---
username | tom | 用戶的用戶名
password | 123456 | 用戶的密碼
grant_type | password | 授權類型

返回示例：
```
{
    "access_token": "6833fa31-d39f-4f4e-bc85-adb86668c20c",
    "token_type": "bearer",
    "expires_in": 2591999,
    "scope": "admin"
}
```

**2. 使用access_token獲取數據**

`GET`請求：`http://localhost:8080/api/users?access_token=6833fa31-d39f-4f4e-bc85-adb86668c20c`
結果：
```
[
    {
        "name": "adolfo",
        "email": "adolfo@mailinator.com"
    },
    {
        "name": "demigreite",
        "email": "demigreite@mailinator.com"
    },
    {
        "name": "jujuba",
        "email": "jujuba@mailinator.com"
    }
]
```
