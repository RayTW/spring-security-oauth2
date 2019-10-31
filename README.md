# spring-security-oauth2

## 1. 理解OAuth 2.0
[OAuth](https://en.wikipedia.org/wiki/OAuth)是一個關於授權（authorization）的開放網絡標準，在全世界得到廣泛應用，目前的版本是2.0版。
## 2. 協議的參與者
OAuth2.0相關的專業術語：
* RO (Resource Owner): 資源所有者，對資源具有授權能力的人。
* Third-party application：第三方應用程序，又稱"客戶端"（cli​​ent）。
* HTTP service：HTTP服務提供商。
* User Agent：用戶代理，本文中是指瀏覽器。
* AS (Authorization Server): 授權服務器，它認證RO的身份，為RO提供授權審批流程，並最終頒發授權令牌(Access Token)。
* RS (Resource Server): 資源服務器，即服務提供商存放用戶資源的服務器。讀者請注意，為了便於協議的描述，這裡只是在邏輯上把AS與RS區分開來；在物理上，AS與RS的功能可以由同一個服務器來提供服務。

## 3. OAuth流程
OAuth在"客戶端"與"服務提供商"之間，設置了一個授權層（authorization layer）。 "客戶端"不能直接登錄"服務提供商"，只能登錄授權層，以此將用戶與客戶端區分開來。 "客戶端"登錄授權層所用的令牌（token），與用戶的密碼不同。用戶可以在登錄的時候，指定授權層令牌的權限範圍和有效期。

"客戶端"登錄授權層以後，"服務提供商"根據令牌的權限範圍和有效期，向"客戶端"開放用戶儲存的資料。

OAuth 2.0的運行流程如下圖，摘自[RFC 6749](https://tools.ietf.org/html/rfc6749)。

![](static/Protocol_Flow.jpg)

> * （A）用戶打開客戶端以後，客戶端要求用戶給予授權。
> * （B）用戶同意給予客戶端授權。
> * （C）客戶端使用上一步獲得的授權，向認證服務器申請令牌。
> * （D）認證服務器對客戶端進行認證以後，確認無誤，同意發放令牌。
> * （E）客戶端使用令牌，向資源服務器申請獲取資源。
> * （F）資源服務器確認令牌無誤，同意向客戶端開放資源。

## 4. 客戶端的授權模式
客戶端必須得到用戶的授權（authorization grant），才能獲得令牌（access token）。 OAuth 2.0定義了四種授權方式。
* [授權碼模式](code-grant/README.md)（authorization code）
* [簡化模式](implicit-grant/README.md)（implicit）
* [密碼模式](password-grant/README.md)（resource owner password credentials）
* [客戶端模式](client-grant/README.md)（client credentials）


說明：OAuth 2.0說明出自[理解OAuth 2.0](http://www.ruanyifeng.com/blog/2014/05/oauth_2_0.html), 代碼取自網絡
