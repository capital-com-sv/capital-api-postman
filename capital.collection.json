{
	"info": {
		"_postman_id": "a14df8db-4eea-491e-b993-6d5f4c1d652b",
		"name": "Capital.com Public API",
		"description": "The Capital.com API allows direct access to the latest version of our trading engine.\n\nYou can find our Postman Collection here: [https://github.com/capital-com-sv/capital-api-postman](https://github.com/capital-com-sv/capital-api-postman)\n\n# General information\n\n- Base URL: [https://api-capital.backend-capital.com/](https://api-capital.backend-capital.com/)\n- Base demo URL: [https://demo-api-capital.backend-capital.com/](https://demo-api-capital.backend-capital.com/)\n- In order to use the endpoints a session should be launched. This can be done using the `POST ​​/session` endpoint.\n- Session is active for 10 minutes. In case your inactivity is longer than this period then an error will occur upon next request.\n- The API covers the full range of available instruments, licences and trading functionality.\n    \n\n# Getting started\n\nTo use the API the following simple steps should be taken:\n\n- [<b>Create a trading account</b>](http://capital.com/trading/signup)  \n    Note that a demo account can be used.\n- **Turn on Two-Factor Authentication (2FA)**  \n    2FA should be turned on prior to API key generation. [Instruction for 2FA enabling](https://capital.zendesk.com/hc/en-us/articles/4403995863314-How-can-I-enable-2FA-).\n- **Generate an API key**  \n    To generate the API key, go to Settings > API integrations > Generate new key. There you will need to enter the label of the key, set an optional expiration date, enter the 2FA code and that’s it.\n- **You are all set!**\n    \n\n# Available functionality\n\n#### Market data\n\n- Receive real-time prices for the whole range of available assets with the REST and WebSocket API.\n- Get the price history for the whole range of assets.\n    \n\n#### Trading functionality\n\n- Open positions, set stop and limit orders, set stop loss and take profit levels.\n- Review and change financial account settings (trading modes, leverage sizes).\n- Review trades and orders history.\n    \n\n# Changelog\n\n#### **October 05, 2023**\n\n- Limit of 1 request per second is set for the `POST /session` endpoint.\n    \n\n#### **August 04, 2023**\n\n- Added an opportunity to view the whole list of available markets using the `GET /markets` endpoint\n    \n\n#### **July 04, 2023**\n\n- Set maximum date range for parameters `from`, `to`, `lastPeriod` to 1 day for the `GET /history/activity`\n    \n\n#### **March 23, 2022**\n\n- Limit of 1000 requests per hour is set for the `POST /positions` and `POST /workingorders` in Demo.\n    \n\n#### **March 16, 2022**\n\n- WebSocket API endpoints added to Swagger documentation.\n    \n\n#### **February 10, 2022**\n\n- Release of the first version of the REST and WebSocket API.\n    \n\n# Authentication\n\n## How to start new session?\n\nThere are 2 ways to start the session:\n\n- Using your API key, login and password details.\n- Using your API key, login and encrypted password details.\n    \n\n#### Using your API key, login and password details\n\nHere you should simply use the `POST /session` endpoint and mention the received in the platform’s Settings API key in the `X-CAP-API-KEY` header, login and password info in the `identifier` and `password` parameters. The value of the `encryptedPassword` parameter should be `false`.\n\n#### Using your API key, login and encrypted password details\n\n- First of all you should use the `GET ​/session​/encryptionKey` and mention the generated in the platform’s Settings API key in the `X-CAP-API-KEY` header. As a response you will receive the `encryptionKey` and `timeStamp` parameters;\n- Using the received `encryptionKey` and `timeStamp` parameters you should encrypt your password using the AES encryption method.\n    \n\n**Encryption request example**:\n\n``` java\npublic static String encryptPassword(String encryptionKey, Long timestamp, String password) {\n    try {\n        byte[] input = stringToBytes(password + \"|\" + timestamp);\n        input = Base64.encodeBase64(input);\n        KeyFactory keyFactory = KeyFactory.getInstance(RSA_ALGORITHM);\n        PublicKey publicKey = keyFactory.generatePublic(new X509EncodedKeySpec(Base64.decodeBase64(stringToBytes(encryptionKey))));\n        Cipher cipher = Cipher.getInstance(PKCS1_PADDING_TRANSFORMATION);\n        cipher.init(Cipher.ENCRYPT_MODE, publicKey);\n        byte[] output = cipher.doFinal(input);\n        output = Base64.encodeBase64(output);\n        return bytesToString(output);\n    } catch (Exception e) {\n        throw new RuntimeException(e);\n    }\n}\n\n ```\n\nEncrypted password example:\n\n``` java\nencryptionKey = \"MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA1dOujgcFh/9n4JLJMY4VMWZ7aRrynwKXUC9RuoC8Qu5UOeskxgZ1q5DmAXjkes77KrLfFZYEKtrp2g1TB0MBkSALiyrG+Fl52vhET9/AWRhvHuFyskWI7tEtcGIaOB1FwR0EDO9bnylTaZ+Y9sPbLVA7loAtfaX3HW/TI9JDpdmgzXZ0KrwIxdMRzPxVqQXcA8yJL1m33pvo9mOJ0AsQ8FFuy+ctjI8l/8xUhe2Hk01rpMBXDwI1lSjnvuUUDvAtacxyYVlNsnRvbrMZYp7hyimm27RtvCUXhTX2A94tDB0MFLApURrki+tvTvw5ImDPN8qOdTUzbs8hNtVwTpSxPwIDAQAB\";\ntimestamp = 1647440528194;\npassword = \"1111qqqq\";\n// Result of password encryption with the encryptionKey\nencryptedPassword = \"hUxWlqKRhH6thdjJnR7DvdlGE7ABkcKHrzKDGeE7kQ7nKg91sw7BpYsLDqtxihnlHN2IEmFPZ/ZmOKBAwEAw9/vjELmAZDeKsu3Q6s+Koj4wt8giE1Sxv76JjjOB/667dEeL22IFO1rwTMZ1NS5DrfeYbTfOdQgA0v5eIOS3fH8Pp/mFHodibY28X+zIaNwk6Rcb49l6aiXwM1CAtDl359qK633a+sEB9TR0/C3EaRkuGg8wAQyQ0JERaSYOZ58Dx7pw//cmvk/U5dkQlgli2l6Ts2cMhqYXCD1ZlTDA/rLfl52lgnarfari3n0uh6LicmNeWXJBF5oxj3LCruVwMA==\";\n\n ```\n\n- Go to the `POST ​/session` endpoint, set `true` value for the `encryptedPassword` parameter and mention the received in the platform’s Settings API key in the `X-CAP-API-KEY` header, login and prior **encrypted** password info in the `identifier` and `password` parameters\n    \n\n## After starting the session\n\nOn starting the session you will receive the `CST` and `X-SECURITY-TOKEN` parameters in the response headers. `CST` is an authorization token, `X-SECURITY-TOKEN` shows which financial account is used for the trades. These headers should be passed on subsequent requests to the API. Both tokens are valid for 10 minutes after the last use.\n\n# Symbology\n\n- **Financial accounts**  \n    accountId is the ID of your financial account. Each financial account has its unique ID. To view the full list of the available financial accounts, use the `GET ​​/accounts` endpoint. To find out which financial account is used for trading operations in the API please go to the `GET ​/session` endpoint. To change the financial account use: `PUT ​/session`.\n- **Epic**  \n    Epic is the name of the market pair. You can use the `GET /markets{?searchTerm}` endpoint to find the market pairs you are interested in. A simple market name like ‘Bitcoin’ or ‘BTC’ can be requested with the `searchTerm` parameter and you will receive the full list of the market pairs associated with it. The `GET ​/marketnavigation` endpoint can be used to obtain asset group names. These names can be used with the `GET ​​/marketnavigation​/{nodeId}` endpoint to view the list of assets under the corresponding group.\n- **Watchlists**  \n    The Watchlist is the list of assets which can be seen and created on the platform. The `GET /watchlists` endpoint returns the existing watchlists on your account. Each watchlist has an id parameter which can be used to obtain the corresponding list of assets: `GET ​/watchlists​/{watchlistId}`\n    \n\n# Orders and positions\n\n- When opening a position using the `POST /positions` endpoint a `dealReference` parameter is included in the response. However, a successful response does not always mean that the position has been successfully opened. The status of the position can be confirmed using `GET ​/confirms​/{dealReference}`. This will produce the status of the position together with the `affectedDeals` array. Note that several positions can be opened at a time: this info will be shown in the `affectedDeals` array.\n- It is important to ensure that the correct trading mode is in use with the API. To find out which trading mode is set on your financial account use the `GET ​/accounts​/preferences` method. The `hedgingMode` parameter value shows whether the hedging mode is engaged. This value can be altered using endpoint: `PUT ​/accounts​/preferences`.\n- The leverages set for trades can be obtained using the `GET ​​/accounts​/preferences` endpoint. To change leverages, use `PUT ​​/accounts​/preferences`.\n- Note: Stop loss and take profit values cannot be set when conducting trades with real stocks.\n    \n\n# FAQ\n\n## Which kind of APIs do you have?\n\nOn Capital.com we suggest both REST and WebSocket API. In case of WebSocket API real-time prices updates for max 40 instruments at a time.\n\n## Do you have any limitations on your API?\n\nYes, we do have several limitations in our Capital.com API. Here is the list:\n\n- The maximum request rate is **10 per second** per user.\n- WebSocket session duration is **10 minutes**. In order to keep the session live use the ping endpoint.\n- REST session is also active for **10 minutes**. In case your inactivity is longer than this period then an error will occur upon next request.\n- `POST /session` endpoint limit is **1 request per second** per API key.\n- `POST /positions` and `POST /workingorders` endpoint limit is **1000 requests per hour** in the Demo account.\n- The WebSocket API allows subscription to a maximum of **40 instruments**.\n- WebSocket streaming falls off when the financial account is changed with the help of the `PUT​ /session` endpoint.\n    \n\n## Does your API support all the instruments?\n\nYes, Capital.com API supports all of the instruments which you can find on the platform.\n\n## How to start using Capital.com API?\n\nIn order to start using our Capital.com API you should first of all generate an API key in the `Settings` > `API integrations` section on the platform. Upon doing so you will be able to use this key and your account credentials to authorise for the API usage with the `POST /session` method.\n\n## Can I use Capital.com API on the Demo account?\n\nSure. In order to use your Demo account with our API you should mention the following service as Base URL: [https://demo-api-capital.backend-capital.com/](https://demo-api-capital.backend-capital.com/)\n\n## How to generate an API key?\n\nIn order to generate an API Key you should log in to your account, go to the `Settings` > `API integrations` section and click on the `Generate API key` button.\n\nIn case your 2FA is turned off you will be asked to switch on this function to ensure safe and secure keys usage.\n\nNext you will be presented with the `Generate new key` window where you will be able to name your API Key and set an expiration date (if needed). By default the validity of the API key is 1 year.\n\nAfter that you should enter your 2FA code and wait for an API Key to be generated. Once an API Key is generated you will see an API Key itself. Please, make sure to save this data as it is shown only once.\n\nCongratulations. You should have successfully managed to integrate our API functionality. In case you have any questions - feel free to contact us ([support@capital.com](mailto:support@capital.com)). We will be glad to help you.\n\n## Which kind of API Key privileges can I have?\n\nCurrently we have only 1 type of the API Keys privileges which allows trading. No Read Only API Keys can be generated.\n\n## What does a Custom password field mean during the API key generation process?\n\nA `Custom password` field allows you to generate a separate password for your API key in order you could use it instead of the account password during starting a session with the `POST /session` method. If you set this `Custom password` for the API key you can use only it for starting a session with this particular key.\n\n## How can I create an API key if I registered my account on Capital.com using Facebook, Gmail or Apple ID accounts?\n\nIn case you used Facebook, Gmail or Apple ID accounts for creating your account on the Capital.com platform then you can create an API key with a `Custom password` to it. You should create this password by yourself during the API key generation process and it can be used in order to start a session with the API usage. Mention the set password as a value for the `password` parameter in the `POST /session` method to launch a session. Also mention the email from the Facebook, Gmail or Apple ID accounts as a value for the identifier parameter.\n\nPlease note that you should create passwords for all of your subsequent API keys until the moment you set a password to your Capital.com account. After that moment you can either proceed to create Custom passwords for your API keys or use an account password if you haven't generated a custom one for this API key prior.\n\n## How can I pause or launch an API key?\n\nIn order to pause or launch an API key you can click on the `Pause` or `Play` icons next to the API key in the `Settings` > `API integrations` section. This functionality allows you to either disable or enable a key when you need to do it without deleting a key itself and re-generating a new one.\n\n## How can I view more information about the API key?\n\nIn order to view more information about the API key you have generated please click on an `Eye` icon next to the key in the `Settings` > `API integrations` section.\n\n## I don't see my API Key. What could have happened?\n\nThere are 2 reasons for your API Key to be deleted:\n\n- your account status has changed to either `SUSPENDED` or `BLOCKED`;\n- your API Key has reached an expiration date.\n    \n\nIn all other cases your API Keys should work as expected.\n\n## I see \"****\" instead of my API Key. How can I find a full API Key information?\n\nAccording to the existing procedure the only moment you can see your API Key is during its creation. After that it will always be masked.\n\nIn case you have lost your API Key or didn't record it, you will have to create a new one and make sure that you store a new key in a secure place.\n\n# WebSocket API\n\nIn order to start using WebSocket connect to `wss://api-streaming-capital.backend-capital.com/connect`.\n\nIn order to keep the connection alive, ping service at least once every 10 minutes.\n\nMore information regarding the WebSocket API requests and responses parameters can be found in the table below:\n\n| **Parameter** | **Description** |\n| --- | --- |\n| destination | The subscription destination which performs as an analogue for the request endpoint in the REST API model. |\n| correlationId | Is set to understand for which request the message was received. Helps to track the correlation between the subscription destination and response. |\n| cst | Access token identifying the client. Can be received upon starting the session.  <br>Is equal to `CST` parameter. |\n| securityToken | Account token or account id identifying the client's current account. Can be received upon starting the session.  <br>Is equal to `X-SECURITY-TOKEN` parameter. |\n| payload | An object which contains the data regarding the corresponding markets. |\n\n## Subscribe to market data\n\n**Destination:** `marketData.subscribe`\n\nSubscribe to the price updates by mentioning the epics  \nThe maximum number of epics: 40\n\n**Request message example:**\n\n``` java\n{\n    \"destination\": \"marketData.subscribe\",\n    \"correlationId\": \"1\",\n    \"cst\": \"zvkT26****nsHKk\",\n    \"securityToken\": \"g6K90****QKvCS7\",\n    \"payload\": {\n        \"epics\": [\n            \"OIL_CRUDE\"\n        ]\n    }\n}\n\n ```\n\n**Example of the response message about successful subscription:**\n\n``` java\n{\n    \"status\": \"OK\",\n    \"destination\": \"marketData.subscribe\",\n    \"correlationId\": \"1\",\n    \"payload\": {\n        \"subscriptions\": {\n            \"OIL_CRUDE\": \"PROCESSED\"\n        }\n    }\n}\n\n ```\n\n**Example of the response message with market data updates:**\n\n``` java\n{\n    \"status\": \"OK\",\n    \"destination\": \"quote\",\n    \"payload\": {\n        \"epic\": \"OIL_CRUDE\",\n        \"product\": \"CFD\",\n        \"bid\": 93.87,\n        \"bidQty\": 4976.0,\n        \"ofr\": 93.9,\n        \"ofrQty\": 5000.0,\n        \"timestamp\": 1660297190627\n    }\n}\n\n ```\n\n## Unsubscribe from market data\n\n**Destination:** `marketData.unsubscribe`\n\nUnsubscribe from the prices updates\n\n**Request message example:**\n\n``` java\n{\n    \"destination\": \"marketData.unsubscribe\",\n    \"correlationId\": \"2\",\n    \"cst\": \"zvkT26****nsHKk\",\n    \"securityToken\": \"g6K90****QKvCS7\",\n    \"payload\": {\n        \"epics\": [\n            \"OIL_CRUDE\"\n        ]\n    }\n}\n\n ```\n\n**Example of the response message about successful unsubscription:**\n\n``` java\n{\n    \"status\": \"OK\",\n    \"destination\": \"marketData.unsubscribe\",\n    \"correlationId\": \"2\",\n    \"payload\": {\n        \"subscriptions\": {\n            \"OIL_CRUDE\": \"PROCESSED\"\n        }\n    }\n}\n\n ```\n\n## Subscribe to OHLC market data\n\n**Destination:** `OHLCMarketData.subscribe`\n\nSubscribe to the candlestick bars updates by mentioning the epics, resolutions and bar type\n\nList of request payload parameters:\n\n| **Parameter** | **Format** | **Required?** | **Description** |\n| --- | --- | --- | --- |\n| epics | string\\[\\] | YES | The list of instruments epics  <br>  <br>Notes:  <br>\\- Max number of epics is limited to 40 |\n| resolutions | string\\[\\] | NO | The list of resolutions of requested prices  <br>  <br>Notes:  <br>\\- Default value: `MINUTE`  <br>\\- Possible values: `MINUTE`, `MINUTE_5`, `MINUTE_15`, `MINUTE_30`, `HOUR`, `HOUR_4`, `DAY`, `WEEK` |\n| type | string | NO | Type of candlesticks  <br>  <br>Notes:  <br>\\- Default value: `classic`  <br>\\- Possible values: `classic`, `heikin-ashi` |\n\n**Request message example:**\n\n``` java\n{\n    \"destination\": \"OHLCMarketData.subscribe\",\n    \"correlationId\": \"3\",\n    \"cst\": \"zvkT26****nsHKk\",\n    \"securityToken\": \"g6K90****QKvCS7\",\n    \"payload\": {\n        \"epics\": [\n            \"OIL_CRUDE\",\n            \"AAPL\"\n        ],\n        \"resolutions\": [\n            \"MINUTE_5\"\n        ],\n        \"type\": \"classic\"\n    }\n}\n\n ```\n\n**Example of the response message about successful subscription:**\n\n``` java\n{\n    \"status\": \"OK\",\n    \"destination\": \"OHLCMarketData.subscribe\",\n    \"correlationId\": \"3\",\n    \"payload\": {\n        \"subscriptions\": {\n            \"OIL_CRUDE:MINUTE_5:classic\": \"PROCESSED\",\n            \"AAPL:MINUTE_5:classic\": \"PROCESSED\"\n        }\n    }\n}\n\n ```\n\n**Example of the response message with market data updates:**\n\n``` java\n{\n    \"status\": \"OK\",\n    \"destination\": \"ohlc.event\",\n    \"payload\": {\n        \"resolution\": \"MINUTE_5\",\n        \"epic\": \"AAPL\",\n        \"type\": \"classic\",\n        \"priceType\": \"bid\",\n        \"t\": 1671714000000,\n        \"h\": 134.95,\n        \"l\": 134.85,\n        \"o\": 134.86,\n        \"c\": 134.88\n    }\n}\n\n ```\n\n## Unsubscribe from OHLC market data\n\n**Destination:** `OHLCMarketData.unsubscribe`\n\nUnsubscribe from candlestick bars updates for specific epics, resolutions and bar types.\n\nThe general principle is as follows: you unsubscribe from the parameter you mention in the request. In case you mention epic you unsubscribe from all of the corresponding bar types and resolutions.\n\nList of request payload parameters:\n\n| **Parameter** | **Format** | **Required?** | **Description** |\n| --- | --- | --- | --- |\n| epics | string\\[\\] | YES | The list of instruments epics to be unsubscribed |\n| resolutions | string\\[\\] | NO | The list of price resolutions to be unsubscribed  <br>  <br>Notes:  <br>\\- Default value: All possible values  <br>\\- Possible values: `MINUTE`, `MINUTE_5`, `MINUTE_15`, `MINUTE_30`, `HOUR`, `HOUR_4`, `DAY`, `WEEK` |\n| types | string\\[\\] | NO | Types of candlesticks to be unsubscribed  <br>  <br>Notes:  <br>\\- Default value: all possible values  <br>\\- Possible values: `classic`, `heikin-ashi` |\n\n**Request message example:**\n\n``` java\n// Unsubscribe from candlestick bars updates of OIL_CRUDE epic with MINUTE and MINUTE_5 resolutions and heikin-ashi candlestick type\n{\n    \"destination\": \"OHLCMarketData.unsubscribe\",\n    \"correlationId\": \"4\",\n    \"cst\": \"zvkT26****nsHKk\",\n    \"securityToken\": \"g6K90****QKvCS7\",\n    \"payload\": {\n        \"epics\": [\n            \"OIL_CRUDE\"\n        ],\n        \"resolutions\": [\n            \"MINUTE\",\n            \"MINUTE_5\"\n        ],\n        \"types\": [\n            \"heikin-ashi\"\n        ]\n    }\n}\n\n ```\n\n**Example of the response message about successful unsubscription:**\n\n``` java\n{\n    \"status\": \"OK\",\n    \"destination\": \"OHLCMarketData.unsubscribe\",\n    \"correlationId\": \"4\",\n    \"payload\": {\n        \"subscriptions\": {\n            \"OIL_CRUDE:MINUTE_5:heikin-ashi\": \"PROCESSED\",\n            \"OIL_CRUDE:MINUTE:heikin-ashi\": \"PROCESSED\"\n        }\n    }\n}\n\n ```\n\n## Ping the service\n\n**Destination:** `ping`\n\nPing the service for keeping the connection alive\n\n**Request message example:**\n\n``` java\n{\n    \"destination\": \"ping\",\n    \"correlationId\": \"5\",\n    \"cst\": \"zvkT26****nsHKk\",\n    \"securityToken\": \"g6K90****QKvCS7\"\n}\n\n ```\n\n**Response message example:**\n\n``` java\n{\n    \"status\": \"OK\",\n    \"destination\": \"ping\",\n    \"correlationId\": \"5\",\n    \"payload\": {}\n}\n\n ```",
		"schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json",
		"_exporter_id": "21320616"
	},
	"item": [
		{
			"name": "General",
			"item": [
				{
					"name": "Get server time",
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "{{url}}/time",
							"host": [
								"{{url}}"
							],
							"path": [
								"time"
							]
						},
						"description": "Test connectivity to the API and get the current server time\n\nAuthentication is not required for this endpoint"
					},
					"response": [
						{
							"name": "Successful response",
							"originalRequest": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{url}}/time",
									"host": [
										"{{url}}"
									],
									"path": [
										"time"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Wed, 06 Apr 2022 15:42:44 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n\t\"serverTime\": 1649259764171\n}"
						}
					]
				},
				{
					"name": "Ping the service",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									""
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "GET",
						"header": [
							{
								"key": "X-SECURITY-TOKEN",
								"value": "{{X-SECURITY-TOKEN}}",
								"type": "text",
								"description": "Account token or account id identifying the client's current account"
							},
							{
								"key": "CST",
								"value": "{{CST}}",
								"type": "text",
								"description": "Access token identifying the client"
							}
						],
						"url": {
							"raw": "{{url}}/ping",
							"host": [
								"{{url}}"
							],
							"path": [
								"ping"
							]
						},
						"description": "Ping the service to keep a trading session alive"
					},
					"response": [
						{
							"name": "Successful response",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token or account id identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/ping",
									"host": [
										"{{url}}"
									],
									"path": [
										"ping"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 08:26:54 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"OK\"\n}"
						}
					]
				}
			]
		},
		{
			"name": "Session",
			"item": [
				{
					"name": "Encryption key",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									""
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "GET",
						"header": [
							{
								"key": "X-CAP-API-KEY",
								"value": "{{X-CAP-API-KEY}}",
								"type": "text",
								"description": "The API key obtained from Settings > API Integrations page on the Capital.com trading platform"
							}
						],
						"url": {
							"raw": "{{url}}/session/encryptionKey",
							"host": [
								"{{url}}"
							],
							"path": [
								"session",
								"encryptionKey"
							]
						},
						"description": "Get the encryption key to use in order to send the user password in an encrypted form"
					},
					"response": [
						{
							"name": "Successful response",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "X-CAP-API-KEY",
										"value": "{{X-CAP-API-KEY}}",
										"type": "text",
										"description": "The API key obtained from Settings > API Integrations page on the Capital.com trading platform"
									}
								],
								"url": {
									"raw": "{{url}}/session/encryptionKey",
									"host": [
										"{{url}}"
									],
									"path": [
										"session",
										"encryptionKey"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 07:50:06 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"encryptionKey\": \"MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAxOZgr4OMjNBMKpR+fZpxrDGGwDk3eGnrI+AvRq1X+psNZEjcQ/tR7XkXfy/BzhXKsrdJO4dqwFrULg03olkhapNpo0wr3Jhr3QLPOeX7bAvgL1pkg/1/ySX4ZPZ8tYuGFXRX0v/DeMYJFFiW1NjHS2phTlmVAHy6a5VRx/GmkvBxo/Xh6L0uaIZIbxNRoU1T+4oR7eaIVKtDL5uxX518EgvpU5QNFMg03Z+e5BTczCPR7xmnpKFMsu40zdICtdylxHXBupuh9zeQ5Rbx1xc72x3emUxL4PRCTh/t0gb9mCID4/AIQqSRykY9NpfkXGJV5mBN/3ZHJanHiE2mnVTlbwIBOOBA\",\n    \"timeStamp\": 1649058606014\n}"
						}
					]
				},
				{
					"name": "Session details",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									""
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "GET",
						"header": [
							{
								"key": "X-SECURITY-TOKEN",
								"value": "{{X-SECURITY-TOKEN}}",
								"type": "text",
								"description": "Account token or account id identifying the client's current account"
							},
							{
								"key": "CST",
								"value": "{{CST}}",
								"type": "text",
								"description": "Access token identifying the client"
							}
						],
						"url": {
							"raw": "{{url}}/session",
							"host": [
								"{{url}}"
							],
							"path": [
								"session"
							]
						},
						"description": "Returns the user's session details"
					},
					"response": [
						{
							"name": "Successful response",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token or account id identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/session",
									"host": [
										"{{url}}"
									],
									"path": [
										"session"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 08:26:54 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"clientId\": \"12345678\",\n    \"accountId\": \"12345678901234567\",\n    \"timezoneOffset\": 3,\n    \"locale\": \"en\",\n    \"currency\": \"USD\",\n    \"streamEndpoint\": \"wss://api-streaming-capital.backend-capital.com/\"\n}"
						}
					]
				},
				{
					"name": "Create new session",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									"pm.environment.set(\"X-SECURITY-TOKEN\", pm.response.headers.get(\"X-SECURITY-TOKEN\"));",
									"pm.environment.set(\"CST\", pm.response.headers.get(\"CST\"));"
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "POST",
						"header": [
							{
								"key": "X-CAP-API-KEY",
								"value": "{{X-CAP-API-KEY}}",
								"type": "text",
								"description": "The API key obtained from Settings > API Integrations page on the Capital.com trading platform"
							}
						],
						"body": {
							"mode": "raw",
							"raw": "{\n\t\"identifier\": \"{{identifier}}\",\n\t\"password\": \"{{password}}\"\n}",
							"options": {
								"raw": {
									"language": "json"
								}
							}
						},
						"url": {
							"raw": "{{url}}/session",
							"host": [
								"{{url}}"
							],
							"path": [
								"session"
							]
						},
						"description": "Create a trading session, obtaining session tokens for subsequent API access\n\nSession is active for 10 minutes. In case your inactivity is longer than this period then you need to create a new session\n\nEndpoint limit: 1 request per second\n\nList of request body parameters:\n\n| **Parameter** | **Format** | **Required?** | **Description** |\n| --- | --- | --- | --- |\n| identifier | string | YES | Client login identifier |\n| password | string | YES | Client login password |\n| encryptedPassword | boolean | NO | Whether the password has been encrypted.  <br>Default value: `false` |"
					},
					"response": [
						{
							"name": "Success: Session created (basic password)",
							"originalRequest": {
								"method": "POST",
								"header": [
									{
										"key": "X-CAP-API-KEY",
										"value": "{{X-CAP-API-KEY}}",
										"type": "text",
										"description": "The API key obtained from Settings > API Integrations page on the Capital.com trading platform"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n\t\"identifier\": \"ENTER_YOUR_EMAIL\",\n\t\"password\": \"•••••••\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{url}}/session",
									"host": [
										"{{url}}"
									],
									"path": [
										"session"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "JSON",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 07:34:59 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\r\n\t\"accountType\": \"CFD\",\r\n\t\"accountInfo\": {\r\n\t\t\"balance\": 124.95,\r\n\t\t\"deposit\": 125.18,\r\n\t\t\"profitLoss\": -0.23,\r\n\t\t\"available\": 116.93\r\n\t},\r\n\t\"currencyIsoCode\": \"USD\",\r\n\t\"currencySymbol\": \"$\",\r\n\t\"currentAccountId\": \"12345678901234567\",\r\n\t\"streamingHost\": \"wss://api-streaming-capital.backend-capital.com/\",\r\n\t\"accounts\": [\r\n\t\t{\r\n\t\t\t\"accountId\": \"12345678901234567\",\r\n\t\t\t\"accountName\": \"USD\",\r\n\t\t\t\"preferred\": true,\r\n\t\t\t\"accountType\": \"CFD\"\r\n\t\t},\r\n\t\t{\r\n\t\t\t\"accountId\": \"12345678907654321\",\r\n\t\t\t\"accountName\": \"Second account\",\r\n\t\t\t\"preferred\": false,\r\n\t\t\t\"accountType\": \"CFD\"\r\n\t\t}\r\n\t],\r\n\t\"clientId\": \"12345678\",\r\n\t\"timezoneOffset\": 3,\r\n\t\"hasActiveDemoAccounts\": true,\r\n\t\"hasActiveLiveAccounts\": true,\r\n\t\"trailingStopsEnabled\": false\r\n}"
						},
						{
							"name": "Success: Session created (encrypted password)",
							"originalRequest": {
								"method": "POST",
								"header": [
									{
										"key": "X-CAP-API-KEY",
										"value": "{{X-CAP-API-KEY}}",
										"type": "text",
										"description": "The API key obtained from Settings > API Integrations page on the Capital.com trading platform"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"identifier\": \"{{identifier}}\",\n    \"password\": \"{{encryptedPassword}}\",\n\t\"encryptedPassword\": true\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{url}}/session",
									"host": [
										"{{url}}"
									],
									"path": [
										"session"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "JSON",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 07:34:59 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\r\n\t\"accountType\": \"CFD\",\r\n\t\"accountInfo\": {\r\n\t\t\"balance\": 124.95,\r\n\t\t\"deposit\": 125.18,\r\n\t\t\"profitLoss\": -0.23,\r\n\t\t\"available\": 116.93\r\n\t},\r\n\t\"currencyIsoCode\": \"USD\",\r\n\t\"currencySymbol\": \"$\",\r\n\t\"currentAccountId\": \"12345678901234567\",\r\n\t\"streamingHost\": \"wss://api-streaming-capital.backend-capital.com/\",\r\n\t\"accounts\": [\r\n\t\t{\r\n\t\t\t\"accountId\": \"12345678901234567\",\r\n\t\t\t\"accountName\": \"USD\",\r\n\t\t\t\"preferred\": true,\r\n\t\t\t\"accountType\": \"CFD\"\r\n\t\t},\r\n\t\t{\r\n\t\t\t\"accountId\": \"12345678907654321\",\r\n\t\t\t\"accountName\": \"Second account\",\r\n\t\t\t\"preferred\": false,\r\n\t\t\t\"accountType\": \"CFD\"\r\n\t\t}\r\n\t],\r\n\t\"clientId\": \"12345678\",\r\n\t\"timezoneOffset\": 3,\r\n\t\"hasActiveDemoAccounts\": true,\r\n\t\"hasActiveLiveAccounts\": true,\r\n\t\"trailingStopsEnabled\": false\r\n}"
						},
						{
							"name": "Error: API key missing",
							"originalRequest": {
								"method": "POST",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\n\t\"identifier\": \"{{identifier}}\",\n\t\"password\": \"{{password}}\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{url}}/session",
									"host": [
										"{{url}}"
									],
									"path": [
										"session"
									]
								}
							},
							"status": "Bad Request",
							"code": 400,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 07:43:20 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"errorCode\": \"error.null.api.key\"\n}"
						},
						{
							"name": "Error: Invalid credentials",
							"originalRequest": {
								"method": "POST",
								"header": [
									{
										"key": "X-CAP-API-KEY",
										"value": "{{X-CAP-API-KEY}}",
										"type": "text",
										"description": "The API key obtained from Settings > API Integrations page on the Capital.com trading platform"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n\t\"identifier\": \"test@email.com\",\n\t\"password\": \"invalid\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{url}}/session",
									"host": [
										"{{url}}"
									],
									"path": [
										"session"
									]
								}
							},
							"status": "Unauthorized",
							"code": 401,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 16:23:17 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"errorCode\": \"error.invalid.details\"\n}"
						},
						{
							"name": "Error: Request limit exceeded",
							"originalRequest": {
								"method": "POST",
								"header": [
									{
										"key": "X-CAP-API-KEY",
										"value": "{{X-CAP-API-KEY}}",
										"type": "text",
										"description": "The API key obtained from Settings > API Integrations page on the Capital.com trading platform"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n\t\"identifier\": \"{{identifier}}\",\n\t\"password\": \"{{password}}\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{url}}/session",
									"host": [
										"{{url}}"
									],
									"path": [
										"session"
									]
								}
							},
							"status": "Too Many Requests",
							"code": 429,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 16:23:17 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"errorCode\": \"error.too-many.requests\"\n}"
						}
					]
				},
				{
					"name": "Switches active account",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									""
								],
								"type": "text/javascript"
							}
						}
					],
					"protocolProfileBehavior": {
						"disabledSystemHeaders": {}
					},
					"request": {
						"method": "PUT",
						"header": [
							{
								"key": "X-SECURITY-TOKEN",
								"value": "{{X-SECURITY-TOKEN}}",
								"type": "text",
								"description": "Account token identifying the client's current account"
							},
							{
								"key": "CST",
								"value": "{{CST}}",
								"type": "text",
								"description": "Access token identifying the client"
							}
						],
						"body": {
							"mode": "raw",
							"raw": "{\n    \"accountId\" : \"{{accountId}}\"\n}",
							"options": {
								"raw": {
									"language": "json"
								}
							}
						},
						"url": {
							"raw": "{{url}}/session",
							"host": [
								"{{url}}"
							],
							"path": [
								"session"
							]
						},
						"description": "Switch active account\n\nList of request body parameters:\n\n| **Parameter** | **Format** | **Required?** | **Description** |\n| --- | --- | --- | --- |\n| accountId | string | YES | The identifier of the account being switched to |"
					},
					"response": [
						{
							"name": "Success: Account switched",
							"originalRequest": {
								"method": "PUT",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"accountId\" : \"12345678907654321\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{url}}/session",
									"host": [
										"{{url}}"
									],
									"path": [
										"session"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 08:43:39 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"trailingStopsEnabled\": false,\n    \"dealingEnabled\": true,\n    \"hasActiveDemoAccounts\": false,\n    \"hasActiveLiveAccounts\": true\n}"
						},
						{
							"name": "Error: Invalid accountId",
							"originalRequest": {
								"method": "PUT",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"accountId\" : \"0000000000001\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{url}}/session",
									"host": [
										"{{url}}"
									],
									"path": [
										"session"
									]
								}
							},
							"status": "Bad Request",
							"code": 400,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 15:54:49 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"errorCode\": \"error.invalid.accountId\"\n}"
						}
					]
				},
				{
					"name": "Log out of the current session",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									""
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "DELETE",
						"header": [
							{
								"key": "X-SECURITY-TOKEN",
								"value": "{{X-SECURITY-TOKEN}}",
								"type": "text",
								"description": "Account token identifying the client's current account"
							},
							{
								"key": "CST",
								"value": "{{CST}}",
								"type": "text",
								"description": "Access token identifying the client"
							}
						],
						"url": {
							"raw": "{{url}}/session",
							"host": [
								"{{url}}"
							],
							"path": [
								"session"
							]
						},
						"description": "Log out of the current session"
					},
					"response": [
						{
							"name": "Success: Session closed",
							"originalRequest": {
								"method": "DELETE",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/session",
									"host": [
										"{{url}}"
									],
									"path": [
										"session"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "JSON",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 08:49:17 GMT"
								},
								{
									"key": "Content-Length",
									"value": "0"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"SUCCESS\"\n}"
						}
					]
				}
			]
		},
		{
			"name": "Accounts",
			"item": [
				{
					"name": "All accounts",
					"request": {
						"method": "GET",
						"header": [
							{
								"key": "X-SECURITY-TOKEN",
								"value": "{{X-SECURITY-TOKEN}}",
								"type": "text",
								"description": "Account token identifying the client's current account"
							},
							{
								"key": "CST",
								"value": "{{CST}}",
								"type": "text",
								"description": "Access token identifying the client"
							}
						],
						"url": {
							"raw": "{{url}}/accounts",
							"host": [
								"{{url}}"
							],
							"path": [
								"accounts"
							]
						},
						"description": "Returns a list of accounts belonging to the logged-in client"
					},
					"response": [
						{
							"name": "Successfull response",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/accounts",
									"host": [
										"{{url}}"
									],
									"path": [
										"accounts"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 15:38:27 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"accounts\": [\n        {\n            \"accountId\": \"12345678901234567\",\n            \"accountName\": \"USD\",\n            \"status\": \"ENABLED\",\n            \"accountType\": \"CFD\",\n            \"preferred\": true,\n            \"balance\": {\n                \"balance\": 124.95,\n                \"deposit\": 125.18,\n                \"profitLoss\": -0.23,\n                \"available\": 116.93\n            },\n            \"currency\": \"USD\"\n        },\n        {\n            \"accountId\": \"12345678907654321\",\n            \"accountName\": \"Second account\",\n            \"status\": \"ENABLED\",\n            \"accountType\": \"CFD\",\n            \"preferred\": false,\n            \"balance\": {\n                \"balance\": 100.0,\n                \"deposit\": 100.0,\n                \"profitLoss\": 0.0,\n                \"available\": 0.0\n            },\n            \"currency\": \"USD\"\n        }\n    ]\n}"
						}
					]
				},
				{
					"name": "Account preferences",
					"request": {
						"method": "GET",
						"header": [
							{
								"key": "X-SECURITY-TOKEN",
								"value": "{{X-SECURITY-TOKEN}}",
								"type": "text",
								"description": "Account token identifying the client's current account"
							},
							{
								"key": "CST",
								"value": "{{CST}}",
								"type": "text",
								"description": "Access token identifying the client"
							}
						],
						"url": {
							"raw": "{{url}}/accounts/preferences",
							"host": [
								"{{url}}"
							],
							"path": [
								"accounts",
								"preferences"
							]
						},
						"description": "Returns account preferences, i.e. leverage settings and trading mode"
					},
					"response": [
						{
							"name": "Successful response",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/accounts/preferences",
									"host": [
										"{{url}}"
									],
									"path": [
										"accounts",
										"preferences"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 15:43:01 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"hedgingMode\": false,\n    \"leverages\": {\n        \"SHARES\": {\n            \"current\": 2,\n            \"available\": [\n                1,\n                2,\n                3,\n                5\n            ]\n        },\n        \"CURRENCIES\": {\n            \"current\": 1,\n            \"available\": [\n                1,\n                10,\n                20,\n                30\n            ]\n        },\n        \"INDICES\": {\n            \"current\": 10,\n            \"available\": [\n                1,\n                10,\n                20\n            ]\n        },\n        \"CRYPTOCURRENCIES\": {\n            \"current\": 1,\n            \"available\": [\n                1,\n                2\n            ]\n        },\n        \"COMMODITIES\": {\n            \"current\": 5,\n            \"available\": [\n                1,\n                5,\n                10,\n                20\n            ]\n        }\n    }\n}"
						}
					]
				},
				{
					"name": "Update account preferences",
					"request": {
						"method": "PUT",
						"header": [
							{
								"key": "X-SECURITY-TOKEN",
								"value": "{{X-SECURITY-TOKEN}}",
								"type": "text",
								"description": "Account token identifying the client's current account"
							},
							{
								"key": "CST",
								"value": "{{CST}}",
								"type": "text",
								"description": "Access token identifying the client"
							}
						],
						"body": {
							"mode": "raw",
							"raw": "{\n    \"leverages\": {\n        \"SHARES\": 5,\n        \"CURRENCIES\": 10,\n        \"INDICES\": 20,\n        \"CRYPTOCURRENCIES\": 2,\n        \"COMMODITIES\": 5\n    },\n    \"hedgingMode\": false\n}",
							"options": {
								"raw": {
									"language": "json"
								}
							}
						},
						"url": {
							"raw": "{{url}}/accounts/preferences",
							"host": [
								"{{url}}"
							],
							"path": [
								"accounts",
								"preferences"
							]
						},
						"description": "Update account preferences\n\nList of request body parameters:\n\n| **Parameter** | **Format** | **Required?** | **Description** |\n| --- | --- | --- | --- |\n| leverages | object | NO | Set new leverage values |\n| hedgingMode | boolean | NO | Enable or disable hedging mode |"
					},
					"response": [
						{
							"name": "Successful response",
							"originalRequest": {
								"method": "PUT",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"leverages\": {\n        \"SHARES\": 5,\n        \"CURRENCIES\": 10,\n        \"INDICES\": 20,\n        \"CRYPTOCURRENCIES\": 2,\n        \"COMMODITIES\": 5\n    },\n    \"hedgingMode\": false\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{url}}/accounts/preferences",
									"host": [
										"{{url}}"
									],
									"path": [
										"accounts",
										"preferences"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 15:49:05 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"SUCCESS\"\n}"
						},
						{
							"name": "Error: Invalid leverage value",
							"originalRequest": {
								"method": "PUT",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"leverages\": {\n        \"INDICES\": 600\n    }\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{url}}/accounts/preferences",
									"host": [
										"{{url}}"
									],
									"path": [
										"accounts",
										"preferences"
									]
								}
							},
							"status": "Bad Request",
							"code": 400,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 15:51:54 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"errorCode\": \"error.invalid.leverage.value\"\n}"
						}
					]
				},
				{
					"name": "Account activity history",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									""
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "GET",
						"header": [
							{
								"key": "X-SECURITY-TOKEN",
								"value": "{{X-SECURITY-TOKEN}}",
								"type": "text",
								"description": "Account token identifying the client's current account"
							},
							{
								"key": "CST",
								"value": "{{CST}}",
								"type": "text",
								"description": "Access token identifying the client"
							}
						],
						"url": {
							"raw": "{{url}}/history/activity?from=2022-01-17T15:09:47&to=2022-01-17T15:10:05&lastPeriod=600&detailed=true&dealId={{dealId}}&filter=source!=DEALER;type!=POSITION;status==REJECTED;epic==OIL_CRUDE,GOLD",
							"host": [
								"{{url}}"
							],
							"path": [
								"history",
								"activity"
							],
							"query": [
								{
									"key": "from",
									"value": "2022-01-17T15:09:47",
									"description": "Start date. Date format: YYYY-MM-DDTHH:MM:SS (e.g. 2022-04-01T01:01:00). Filtration by date based on dateUTC parameter"
								},
								{
									"key": "to",
									"value": "2022-01-17T15:10:05",
									"description": "End date. Date format: YYYY-MM-DDTHH:MM:SS (e.g. 2022-04-01T01:01:00). Filtration by date based on dateUTC parameter"
								},
								{
									"key": "lastPeriod",
									"value": "600",
									"description": "Limits the timespan in seconds through to current time (not applicable if a date range has been specified). Cannot be bigger than current Unix timestamp value. Default = 600, max = 86400"
								},
								{
									"key": "detailed",
									"value": "true",
									"description": "Indicates whether to retrieve additional details about the activity. False by default"
								},
								{
									"key": "dealId",
									"value": "{{dealId}}",
									"description": "Get activity information for specific dealId"
								},
								{
									"key": "filter",
									"value": "source!=DEALER;type!=POSITION;status==REJECTED;epic==OIL_CRUDE,GOLD",
									"description": "Filter activity list using FIQL. List of supported parameters: epic, source, status, type "
								}
							]
						},
						"description": "Returns the account activity history\n\nAll query parameters are optional for this request\n\nThe maximum possible date range between `from` and `to` parameters is 1 day. If only one of the parameters is specified (`from` or `to`), the 1-day date range will be selected by default\n\nPossible enum values for parameters in FIQL filter:\n\n| **Parameter** | **ENUM** |\n| --- | --- |\n| source | `CLOSE_OUT`, `DEALER`, `SL`, `SYSTEM`, `TP`, `USER` |\n| status | `ACCEPTED`, `CREATED`, `EXECUTED`, `EXPIRED`, `REJECTED`, `MODIFIED`, `MODIFY_REJECT`, `CANCELLED`, `CANCEL_REJECT`, `UNKNOWN` |\n| type | `POSITION`, `WORKING_ORDER`, `EDIT_STOP_AND_LIMIT`, `SWAP`, `SYSTEM` |"
					},
					"response": [
						{
							"name": "Success: Filter list by date",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/history/activity?from=2022-01-17T15:09:47&to=2022-01-17T15:10:05",
									"host": [
										"{{url}}"
									],
									"path": [
										"history",
										"activity"
									],
									"query": [
										{
											"key": "from",
											"value": "2022-01-17T15:09:47",
											"description": "Start date. Date format: YYYY-MM-DDTHH:MM:SS (e.g. 2022-04-01T01:01:00). Filtration by date based on dateUTC parameter"
										},
										{
											"key": "to",
											"value": "2022-01-17T15:10:05",
											"description": "End date. Date format: YYYY-MM-DDTHH:MM:SS (e.g. 2022-04-01T01:01:00). Filtration by date based on dateUTC parameter"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 16:32:28 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"activities\": [\n        {\n            \"date\": \"2022-01-17T18:09:47.344\",\n            \"dateUTC\": \"2022-01-17T15:09:47.344\",\n            \"epic\": \"OIL_CRUDE\",\n            \"dealId\": \"00018509-0001-54c4-0000-000080430164\",\n            \"source\": \"USER\",\n            \"type\": \"POSITION\",\n            \"status\": \"ACCEPTED\"\n        },\n        {\n            \"date\": \"2022-01-17T18:09:47.344\",\n            \"dateUTC\": \"2022-01-17T15:09:47.344\",\n            \"epic\": \"OIL_CRUDE\",\n            \"dealId\": \"00018509-0001-54c4-0000-000080430163\",\n            \"source\": \"SYSTEM\",\n            \"type\": \"WORKING_ORDER\",\n            \"status\": \"ACCEPTED\"\n        },\n        {\n            \"date\": \"2022-01-17T18:09:47.344\",\n            \"dateUTC\": \"2022-01-17T15:09:47.344\",\n            \"epic\": \"OIL_CRUDE\",\n            \"dealId\": \"00018509-0001-54c4-0000-000080430163\",\n            \"source\": \"USER\",\n            \"type\": \"WORKING_ORDER\",\n            \"status\": \"ACCEPTED\"\n        }\n    ]\n}"
						},
						{
							"name": "Success: Filter list using FIQL filter",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/history/activity?filter=source!=DEALER;type!=POSITION;status==REJECTED;epic==OIL_CRUDE,GOLD",
									"host": [
										"{{url}}"
									],
									"path": [
										"history",
										"activity"
									],
									"query": [
										{
											"key": "filter",
											"value": "source!=DEALER;type!=POSITION;status==REJECTED;epic==OIL_CRUDE,GOLD",
											"description": "Filter activity list using FIQL filtering. List of supported parameters: epic, source, type, status"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 16:33:48 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"activities\": [\n        {\n            \"date\": \"2022-01-03T18:01:48.536\",\n            \"dateUTC\": \"2022-01-03T15:01:48.536\",\n            \"epic\": \"OIL_CRUDE\",\n            \"dealId\": \"00018509-0001-54c4-0000-0000803c0ec6\",\n            \"source\": \"SYSTEM\",\n            \"type\": \"EDIT_STOP_AND_LIMIT\",\n            \"status\": \"REJECTED\"\n        },\n        {\n            \"date\": \"2021-12-27T18:26:31.847\",\n            \"dateUTC\": \"2021-12-27T15:26:31.847\",\n            \"epic\": \"OIL_CRUDE\",\n            \"dealId\": \"00018509-0001-54c4-0000-0000803c08e4\",\n            \"source\": \"SYSTEM\",\n            \"type\": \"EDIT_STOP_AND_LIMIT\",\n            \"status\": \"REJECTED\"\n        },\n        {\n            \"date\": \"2021-12-21T17:02:31.978\",\n            \"dateUTC\": \"2021-12-21T14:02:31.978\",\n            \"epic\": \"OIL_CRUDE\",\n            \"dealId\": \"00018509-0001-54c4-0000-0000803c0456\",\n            \"source\": \"SYSTEM\",\n            \"type\": \"EDIT_STOP_AND_LIMIT\",\n            \"status\": \"REJECTED\"\n        },\n        {\n            \"date\": \"2021-12-21T13:02:39.247\",\n            \"dateUTC\": \"2021-12-21T10:02:39.247\",\n            \"epic\": \"OIL_CRUDE\",\n            \"dealId\": \"00018509-0001-54c4-0000-0000803c03fa\",\n            \"source\": \"SYSTEM\",\n            \"type\": \"EDIT_STOP_AND_LIMIT\",\n            \"status\": \"REJECTED\"\n        },\n        {\n            \"date\": \"2021-12-21T11:02:45.459\",\n            \"dateUTC\": \"2021-12-21T08:02:45.459\",\n            \"epic\": \"OIL_CRUDE\",\n            \"dealId\": \"00018509-0001-54c4-0000-0000803c03ce\",\n            \"source\": \"SYSTEM\",\n            \"type\": \"EDIT_STOP_AND_LIMIT\",\n            \"status\": \"REJECTED\"\n        },\n        {\n            \"date\": \"2021-12-21T10:02:29.220\",\n            \"dateUTC\": \"2021-12-21T07:02:29.220\",\n            \"epic\": \"OIL_CRUDE\",\n            \"dealId\": \"00018509-0001-54c4-0000-0000803c03b7\",\n            \"source\": \"SYSTEM\",\n            \"type\": \"EDIT_STOP_AND_LIMIT\",\n            \"status\": \"REJECTED\"\n        },\n        {\n            \"date\": \"2021-10-27T14:01:42.138\",\n            \"dateUTC\": \"2021-10-27T11:01:42.138\",\n            \"epic\": \"OIL_CRUDE\",\n            \"dealId\": \"00018509-0001-54c4-0000-0000803900a2\",\n            \"source\": \"SYSTEM\",\n            \"type\": \"EDIT_STOP_AND_LIMIT\",\n            \"status\": \"REJECTED\"\n        },\n        {\n            \"date\": \"2021-09-17T12:41:59.500\",\n            \"dateUTC\": \"2021-09-17T09:41:59.500\",\n            \"epic\": \"GOLD\",\n            \"dealId\": \"00601567-0001-54c4-0000-000080370b17\",\n            \"source\": \"SYSTEM\",\n            \"type\": \"EDIT_STOP_AND_LIMIT\",\n            \"status\": \"REJECTED\"\n        }\n    ]\n}"
						},
						{
							"name": "Success: Filter list by dealId with enabled detailed view",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/history/activity?detailed=true&dealId=00018509-0001-54c4-0000-0000803c0ec6",
									"host": [
										"{{url}}"
									],
									"path": [
										"history",
										"activity"
									],
									"query": [
										{
											"key": "detailed",
											"value": "true",
											"description": "Indicates whether to retrieve additional details about the activity. False by default"
										},
										{
											"key": "dealId",
											"value": "00018509-0001-54c4-0000-0000803c0ec6",
											"description": "Get activity infromation for specific dealId"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 16:36:12 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"activities\": [\n        {\n            \"date\": \"2022-01-03T18:01:48.536\",\n            \"dateUTC\": \"2022-01-03T15:01:48.536\",\n            \"epic\": \"OIL_CRUDE\",\n            \"dealId\": \"00018509-0001-54c4-0000-0000803c0ec6\",\n            \"source\": \"SYSTEM\",\n            \"type\": \"EDIT_STOP_AND_LIMIT\",\n            \"status\": \"REJECTED\",\n            \"details\": {\n                \"dealReference\": \"p_00018509-0001-54c4-0000-0000803c0ec6\",\n                \"marketName\": \"Crude Oil\",\n                \"currency\": \"USD\",\n                \"size\": 0,\n                \"direction\": \"SELL\",\n                \"level\": 75.31,\n                \"guaranteedStop\": false\n            }\n        },\n        {\n            \"date\": \"2022-01-03T18:01:48.420\",\n            \"dateUTC\": \"2022-01-03T15:01:48.420\",\n            \"epic\": \"OIL_CRUDE\",\n            \"dealId\": \"00018509-0001-54c4-0000-0000803c0ec6\",\n            \"source\": \"CLOSE_OUT\",\n            \"type\": \"POSITION\",\n            \"status\": \"ACCEPTED\",\n            \"details\": {\n                \"dealReference\": \"p_00018509-0001-54c4-0000-0000803c0ec6\",\n                \"marketName\": \"Crude Oil\",\n                \"currency\": \"USD\",\n                \"size\": 1,\n                \"direction\": \"SELL\",\n                \"level\": 75.2,\n                \"guaranteedStop\": false\n            }\n        },\n        {\n            \"date\": \"2022-01-03T18:01:34.228\",\n            \"dateUTC\": \"2022-01-03T15:01:34.228\",\n            \"epic\": \"OIL_CRUDE\",\n            \"dealId\": \"00018509-0001-54c4-0000-0000803c0ec6\",\n            \"source\": \"USER\",\n            \"type\": \"POSITION\",\n            \"status\": \"ACCEPTED\",\n            \"details\": {\n                \"dealReference\": \"p_00018509-0001-54c4-0000-0000803c0ec6\",\n                \"marketName\": \"Crude Oil\",\n                \"currency\": \"USD\",\n                \"size\": 1,\n                \"direction\": \"BUY\",\n                \"level\": 75.31,\n                \"guaranteedStop\": false\n            }\n        }\n    ]\n}"
						},
						{
							"name": "Error: Invalid date format",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/history/activity?from=2022-01-17",
									"host": [
										"{{url}}"
									],
									"path": [
										"history",
										"activity"
									],
									"query": [
										{
											"key": "from",
											"value": "2022-01-17",
											"description": "Start date. Date format: YYYY-MM-DDTHH:MM:SS (e.g. 2022-04-01T01:01:00). Filtration by date based on dateUTC parameter"
										}
									]
								}
							},
							"status": "Bad Request",
							"code": 400,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 16:38:54 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"errorCode\": \"error.invalid.from\"\n}"
						}
					]
				},
				{
					"name": "Account transactions history",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									""
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "GET",
						"header": [
							{
								"key": "X-SECURITY-TOKEN",
								"value": "{{X-SECURITY-TOKEN}}",
								"type": "text",
								"description": "Account token identifying the client's current account"
							},
							{
								"key": "CST",
								"value": "{{CST}}",
								"type": "text",
								"description": "Access token identifying the client"
							}
						],
						"url": {
							"raw": "{{url}}/history/transactions?from=2021-08-10T00:00:00&to=2021-09-10T00:00:01&lastPeriod=600&type=DEPOSIT",
							"host": [
								"{{url}}"
							],
							"path": [
								"history",
								"transactions"
							],
							"query": [
								{
									"key": "from",
									"value": "2021-08-10T00:00:00",
									"description": "Start date. Date format: YYYY-MM-DDTHH:MM:SS (e.g. 2022-04-01T01:01:00). Filtration by date based on dateUTC parameter"
								},
								{
									"key": "to",
									"value": "2021-09-10T00:00:01",
									"description": "End date. Date format: YYYY-MM-DDTHH:MM:SS (e.g. 2022-04-01T01:01:00). Filtration by date based on dateUTC parameter"
								},
								{
									"key": "lastPeriod",
									"value": "600",
									"description": "Limits the timespan in seconds through to current time (not applicable if a date range has been specified). Cannot be bigger than current Unix timestamp value. Default = 600"
								},
								{
									"key": "type",
									"value": "DEPOSIT",
									"description": "Transaction type. Possible values: INACTIVITY_FEE, RESERVE, VOID, UNRESERVE, WRITE_OFF_OR_CREDIT, CREDIT_FACILITY, FX_COMMISSION, COMPLAINT_SETTLEMENT, DEPOSIT, WITHDRAWAL, REFUND, WITHDRAWAL_MONEY_BACK, TRADE, SWAP, TRADE_COMMISSION, TRADE_COMMISSION_GSL, NEGATIVE_BALANCE_PROTECTION, TRADE_CORRECTION, CHARGEBACK, ADJUSTMENT, BONUS, TRANSFER, CORPORATE_ACTION, CONVERSION, REBATE, TRADE_SLIPPAGE_PROTECTION"
								}
							]
						},
						"description": "Returns the transaction history. By default returns the transactions within the last 10 minutes\n\nAll query parameters are optional for this request"
					},
					"response": [
						{
							"name": "Success: Get list of transactions within last hour",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "https://demo-api-capital.backend-capital.com/api/v1/history/transactions",
									"protocol": "https",
									"host": [
										"demo-api-capital",
										"backend-capital",
										"com"
									],
									"path": [
										"api",
										"v1",
										"history",
										"transactions"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 16:51:09 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"transactions\": [\n        {\n            \"date\": \"2022-04-04T19:51:05.648\",\n            \"dateUtc\": \"2022-04-04T16:51:05.648\",\n            \"instrumentName\": \"NATURALGAS\",\n            \"transactionType\": \"TRADE\",\n            \"note\": \"Trade closed\",\n            \"reference\": \"12345678\",\n            \"size\": \"1.05\",\n            \"currency\": \"USD\"\n        },\n        {\n            \"date\": \"2022-04-04T19:51:00.788\",\n            \"dateUtc\": \"2022-04-04T16:51:00.788\",\n            \"instrumentName\": \"US500\",\n            \"transactionType\": \"TRADE\",\n            \"note\": \"Trade closed\",\n            \"reference\": \"87654321\",\n            \"size\": \"416.0\",\n            \"currency\": \"USD\"\n        }\n    ]\n}"
						},
						{
							"name": "Success: Filter list within last 30 second by type",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/history/transactions?lastPeriod=30&type=DEPOSIT",
									"host": [
										"{{url}}"
									],
									"path": [
										"history",
										"transactions"
									],
									"query": [
										{
											"key": "lastPeriod",
											"value": "30",
											"description": "Limits the timespan in seconds through to current time (not applicable if a date range has been specified). Cannot be bigger than current Unix timestamp value. Default = 600"
										},
										{
											"key": "type",
											"value": "DEPOSIT",
											"description": "Transaction type"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 04 Apr 2022 16:54:52 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"transactions\": [\n        {\n            \"date\": \"2022-04-04T19:54:27.568\",\n            \"dateUtc\": \"2022-04-04T16:54:27.568\",\n            \"transactionType\": \"DEPOSIT\",\n            \"note\": \"Deposit\",\n            \"reference\": \"12345678\",\n            \"size\": \"20.0\",\n            \"currency\": \"USD\"\n        }\n    ]\n}"
						}
					]
				}
			]
		},
		{
			"name": "Trading",
			"item": [
				{
					"name": "Рositions",
					"item": [
						{
							"name": "All positions",
							"event": [
								{
									"listen": "test",
									"script": {
										"exec": [
											""
										],
										"type": "text/javascript"
									}
								}
							],
							"request": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/positions",
									"host": [
										"{{url}}"
									],
									"path": [
										"positions"
									]
								},
								"description": "Returns all open positions for the active account"
							},
							"response": [
								{
									"name": "Successful response",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/positions",
											"host": [
												"{{url}}"
											],
											"path": [
												"positions"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Tue, 05 Apr 2022 14:41:40 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"positions\": [\n        {\n            \"position\": {\n                \"contractSize\": 1,\n                \"createdDate\": \"2022-04-05T12:46:01.872\",\n                \"createdDateUTC\": \"2022-04-05T09:46:01.872\",\n                \"dealId\": \"00018387-0001-54c4-0000-000080560014\",\n                \"dealReference\": \"p_00018387-0001-54c4-0000-000080560014\",\n                \"workingOrderId\": \"00018387-0001-54c4-0000-000080560012\",\n                \"size\": 10.0,\n                \"leverage\": 20,\n                \"upl\": -0.0500,\n                \"direction\": \"BUY\",\n                \"level\": 2.764,\n                \"currency\": \"USD\",\n                \"guaranteedStop\": false\n            },\n            \"market\": {\n                \"instrumentName\": \"Natural Gas\",\n                \"expiry\": \"-\",\n                \"marketStatus\": \"TRADEABLE\",\n                \"epic\": \"NATURALGAS\",\n                \"instrumentType\": \"COMMODITIES\",\n                \"lotSize\": 1,\n                \"high\": 2.798,\n                \"low\": 2.743,\n                \"percentageChange\": 0.8053,\n                \"netChange\": 0.0220,\n                \"bid\": 2.759,\n                \"offer\": 2.764,\n                \"updateTime\": \"2022-04-05T17:41:38.492\",\n                \"updateTimeUTC\": \"2022-04-05T14:41:38.492\",\n                \"delayTime\": 0,\n                \"streamingPricesAvailable\": true,\n                \"scalingFactor\": 1\n            }\n        },\n        {\n            \"position\": {\n                \"contractSize\": 1,\n                \"createdDate\": \"2022-04-05T12:46:10.139\",\n                \"createdDateUTC\": \"2022-04-05T09:46:10.139\",\n                \"dealId\": \"004d0627-0001-54c4-0000-000080560017\",\n                \"dealReference\": \"p_004d0627-0001-54c4-0000-000080560017\",\n                \"workingOrderId\": \"004d0627-0001-54c4-0000-000080560015\",\n                \"size\": 1.0,\n                \"leverage\": 20,\n                \"upl\": -0.80,\n                \"direction\": \"BUY\",\n                \"level\": 3985.1,\n                \"currency\": \"USD\",\n                \"guaranteedStop\": false\n            },\n            \"market\": {\n                \"instrumentName\": \"S&P 500\",\n                \"expiry\": \"2022-02-01\",\n                \"marketStatus\": \"TRADEABLE\",\n                \"epic\": \"US500\",\n                \"instrumentType\": \"INDICES\",\n                \"lotSize\": 1,\n                \"high\": 3984.6,\n                \"low\": 3950.3,\n                \"percentageChange\": -0.0301,\n                \"netChange\": -1.2000,\n                \"bid\": 3984.3,\n                \"offer\": 3985.1,\n                \"updateTime\": \"2022-04-05T17:41:37.991\",\n                \"updateTimeUTC\": \"2022-04-05T14:41:37.991\",\n                \"delayTime\": 0,\n                \"streamingPricesAvailable\": true,\n                \"scalingFactor\": 1\n            }\n        }\n    ]\n}"
								}
							]
						},
						{
							"name": "Single position",
							"event": [
								{
									"listen": "test",
									"script": {
										"exec": [
											""
										],
										"type": "text/javascript"
									}
								}
							],
							"request": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/positions/:dealId",
									"host": [
										"{{url}}"
									],
									"path": [
										"positions",
										":dealId"
									],
									"variable": [
										{
											"key": "dealId",
											"value": "{{dealId}}",
											"description": "Permanent deal reference for a confirmed trade"
										}
									]
								},
								"description": "Returns an open position for the active account by deal identifier"
							},
							"response": [
								{
									"name": "Successful response",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/positions/:dealId",
											"host": [
												"{{url}}"
											],
											"path": [
												"positions",
												":dealId"
											],
											"variable": [
												{
													"key": "dealId",
													"value": "006011e7-0001-54c4-0000-00008056005e",
													"description": "Permanent deal reference for a confirmed trade"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 07:53:40 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"position\": {\n        \"contractSize\": 1,\n        \"createdDate\": \"2022-04-06T10:49:52.056\",\n        \"createdDateUTC\": \"2022-04-06T07:49:52.056\",\n        \"dealId\": \"006011e7-0001-54c4-0000-00008056005e\",\n        \"dealReference\": \"p_006011e7-0001-54c4-0000-00008056005e\",\n        \"workingOrderId\": \"006011e7-0001-54c4-0000-00008056005c\",\n        \"size\": 1.0,\n        \"leverage\": 20,\n        \"upl\": -0.0220,\n        \"direction\": \"BUY\",\n        \"level\": 21.059,\n        \"currency\": \"USD\",\n        \"guaranteedStop\": false\n    },\n    \"market\": {\n        \"instrumentName\": \"Silver\",\n        \"expiry\": \"-\",\n        \"marketStatus\": \"TRADEABLE\",\n        \"epic\": \"SILVER\",\n        \"instrumentType\": \"COMMODITIES\",\n        \"lotSize\": 1,\n        \"high\": 21.167,\n        \"low\": 20.823,\n        \"percentageChange\": 1.8478,\n        \"netChange\": 0.3810,\n        \"bid\": 21.037,\n        \"offer\": 21.057,\n        \"updateTime\": \"2022-04-06T10:53:35.389\",\n        \"updateTimeUTC\": \"2022-04-06T07:53:35.389\",\n        \"delayTime\": 0,\n        \"streamingPricesAvailable\": true,\n        \"scalingFactor\": 1\n    }\n}"
								},
								{
									"name": "Error: Position not found",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/positions/:dealId",
											"host": [
												"{{url}}"
											],
											"path": [
												"positions",
												":dealId"
											],
											"variable": [
												{
													"key": "dealId",
													"value": "00018387-0001-54c4-0000-000080560014",
													"description": "Permanent deal reference for a confirmed trade"
												}
											]
										}
									},
									"status": "Not Found",
									"code": 404,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 07:52:26 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"errorCode\": \"error.not-found.dealId\"\n}"
								}
							]
						},
						{
							"name": "Create position",
							"event": [
								{
									"listen": "test",
									"script": {
										"exec": [
											"pm.environment.set(\"dealReference\", pm.response.json().dealReference);"
										],
										"type": "text/javascript"
									}
								},
								{
									"listen": "prerequest",
									"script": {
										"exec": [
											""
										],
										"type": "text/javascript"
									}
								}
							],
							"protocolProfileBehavior": {
								"disabledSystemHeaders": {}
							},
							"request": {
								"method": "POST",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"epic\": \"SILVER\",\n    \"direction\": \"BUY\",\n    \"size\": 1,\n    \"guaranteedStop\": true,\n    \"stopLevel\": 20,\n    \"profitLevel\": 27\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{url}}/positions",
									"host": [
										"{{url}}"
									],
									"path": [
										"positions"
									]
								},
								"description": "Create orders and positions\n\nPlease note that when creating the position an order is created first with the 'o_' prefix in the `dealReference` parameter\n\nList of request body parameters:\n\n| **Parameter** | **Format** | **Required?** | **Description** |\n| --- | --- | --- | --- |\n| direction | string | YES | Deal direction  <br>  <br>Must be `BUY` or `SELL` |\n| epic | string | YES | Instrument epic identifier |\n| size | number | YES | Deal size |\n| guaranteedStop | boolean | NO | Must be `true` if a guaranteed stop is required  <br>  <br>Notes:  <br>\\- Default value: `false`  <br>\\- If `guaranteedStop` equals `true`, then set `stopLevel`, `stopDistance` or `stopAmount`  <br>\\- Cannot be set if `trailingStop` is `true`  <br>\\- Cannot be set if `hedgingMode` is `true` |\n| trailingStop | boolean | NO | Must be `true` if a trailing stop is required  <br>  <br>Notes:  <br>\\- Default value: `false`  <br>\\- If `trailingStop` equals `true`, then set `stopDistance`  <br>\\- Cannot be set if `guaranteedStop` is `true` |\n| stopLevel | number | NO | Price level when a stop loss will be triggered |\n| stopDistance | number | NO | Distance between current and stop loss triggering price  <br>  <br>Notes:  <br>\\- Required parameter if `trailingStop` is `true` |\n| stopAmount | number | NO | Loss amount when a stop loss will be triggered |\n| profitLevel | number | NO | Price level when a take profit will be triggered |\n| profitDistance | number | NO | Distance between current and take profit triggering price |\n| profitAmount | number | NO | Profit amount when a take profit will be triggered |"
							},
							"response": [
								{
									"name": "Success: Create simple position",
									"originalRequest": {
										"method": "POST",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"body": {
											"mode": "raw",
											"raw": "{\n\t\"epic\": \"SILVER\",\n\t\"direction\": \"BUY\",\n\t\"size\": 1\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{url}}/positions",
											"host": [
												"{{url}}"
											],
											"path": [
												"positions"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Tue, 05 Apr 2022 16:16:03 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"dealReference\": \"o_98c0de50-9cd5-4481-8d81-890c525eeb49\"\n}"
								},
								{
									"name": "Success: Create position with stop loss, take profit and guaranteed stop",
									"originalRequest": {
										"method": "POST",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"epic\": \"SILVER\",\n    \"direction\": \"BUY\",\n    \"size\": 1,\n    \"guaranteedStop\": true,\n    \"stopLevel\": 20,\n    \"profitLevel\": 27\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{url}}/positions",
											"host": [
												"{{url}}"
											],
											"path": [
												"positions"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Tue, 05 Apr 2022 16:18:33 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"dealReference\": \"o_bad96cc0-d297-46cd-ab44-dbcda73d7921\"\n}"
								},
								{
									"name": "Error: Too small stop loss value",
									"originalRequest": {
										"method": "POST",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"epic\": \"SILVER\",\n    \"direction\": \"BUY\",\n    \"size\": 1,\n    \"stopLevel\": 1\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{url}}/positions",
											"host": [
												"{{url}}"
											],
											"path": [
												"positions"
											]
										}
									},
									"status": "Bad Request",
									"code": 400,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Tue, 05 Apr 2022 16:20:42 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"errorCode\": \"error.invalid.stoploss.minvalue: 17.146\"\n}"
								},
								{
									"name": "Error: Too high take profit value",
									"originalRequest": {
										"method": "POST",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"epic\": \"SILVER\",\n    \"direction\": \"BUY\",\n    \"size\": 1,\n    \"profitLevel\": 100\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{url}}/positions",
											"host": [
												"{{url}}"
											],
											"path": [
												"positions"
											]
										}
									},
									"status": "Bad Request",
									"code": 400,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Tue, 05 Apr 2022 16:21:46 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"errorCode\": \"error.invalid.takeprofit.maxvalue: 31.817\"\n}"
								}
							]
						},
						{
							"name": "Update position",
							"event": [
								{
									"listen": "test",
									"script": {
										"exec": [
											"pm.environment.set(\"dealReference\", pm.response.json().dealReference);",
											""
										],
										"type": "text/javascript"
									}
								}
							],
							"protocolProfileBehavior": {
								"disabledSystemHeaders": {}
							},
							"request": {
								"method": "PUT",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"guaranteedStop\": true,\n    \"stopDistance\": 3,\n    \"profitAmount\": 2\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{url}}/positions/:dealId",
									"host": [
										"{{url}}"
									],
									"path": [
										"positions",
										":dealId"
									],
									"variable": [
										{
											"key": "dealId",
											"value": "{{dealId}}",
											"description": "Permanent deal reference for a confirmed trade"
										}
									]
								},
								"description": "Update the position\n\nList of request body parameters:\n\n| **Parameter** | **Format** | **Required?** | **Description** |\n| --- | --- | --- | --- |\n| guaranteedStop | boolean | NO | Must be `true` if a guaranteed stop is required  <br>  <br>Notes:  <br>\\- Default value: `false`  <br>\\- If `guaranteedStop` equals `true`, then set `stopLevel`, `stopDistance` or `stopAmount`  <br>\\- Cannot be set if `trailingStop` is `true`  <br>\\- Cannot be set if `hedgingMode` is `true` |\n| trailingStop | boolean | NO | Must be `true` if a trailing stop is required  <br>  <br>Notes:  <br>\\- Default value: `false`  <br>\\- If `trailingStop` equals `true`, then set `stopDistance`  <br>\\- Cannot be set if `guaranteedStop` is `true` |\n| stopLevel | number | NO | Price level when a stop loss will be triggered |\n| stopDistance | number | NO | Distance between current and stop loss triggering price  <br>  <br>Notes:  <br>\\- Required parameter if `trailingStop` is `true` |\n| stopAmount | number | NO | Loss amount when a stop loss will be triggered |\n| profitLevel | number | NO | Price level when a take profit will be triggered |\n| profitDistance | number | NO | Distance between current and take profit triggering price |\n| profitAmount | number | NO | Profit amount when a take profit will be triggered |"
							},
							"response": [
								{
									"name": "Success: Update stop loss, take profit and guaranteed stop",
									"originalRequest": {
										"method": "PUT",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"guaranteedStop\": true,\n    \"stopDistance\": 3,\n    \"profitAmount\": 2\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{url}}/positions/:dealId",
											"host": [
												"{{url}}"
											],
											"path": [
												"positions",
												":dealId"
											],
											"variable": [
												{
													"key": "dealId",
													"value": "006011e7-0001-54c4-0000-000080560068",
													"description": "Permanent deal reference for a confirmed trade"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 08:44:39 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"dealReference\": \"p_006011e7-0001-54c4-0000-000080560068\"\n}"
								},
								{
									"name": "Error: Too high stop loss value",
									"originalRequest": {
										"method": "PUT",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"stopLevel\": 1000\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{url}}/positions/:dealId",
											"host": [
												"{{url}}"
											],
											"path": [
												"positions",
												":dealId"
											],
											"variable": [
												{
													"key": "dealId",
													"value": "006011e7-0001-54c4-0000-000080560068",
													"description": "Permanent deal reference for a confirmed trade"
												}
											]
										}
									},
									"status": "Bad Request",
									"code": 400,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 08:49:55 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"errorCode\": \"error.invalid.stoploss.maxvalue: 24.302\"\n}"
								},
								{
									"name": "Error: Too low take profit value",
									"originalRequest": {
										"method": "PUT",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"profitLevel\": 1\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{url}}/positions/:dealId",
											"host": [
												"{{url}}"
											],
											"path": [
												"positions",
												":dealId"
											],
											"variable": [
												{
													"key": "dealId",
													"value": "006011e7-0001-54c4-0000-000080560068",
													"description": "Permanent deal reference for a confirmed trade"
												}
											]
										}
									},
									"status": "Bad Request",
									"code": 400,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 08:50:46 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"errorCode\": \"error.invalid.takeprofit.minvalue: 24.302\"\n}"
								},
								{
									"name": "Error: Position not found",
									"originalRequest": {
										"method": "PUT",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"guaranteedStop\": true,\n    \"stopDistance\": 3,\n    \"profitAmount\": 2\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{url}}/positions/:dealId",
											"host": [
												"{{url}}"
											],
											"path": [
												"positions",
												":dealId"
											],
											"variable": [
												{
													"key": "dealId",
													"value": "006011e7-0001-54c4-0000-000080560069",
													"description": "Permanent deal reference for a confirmed trade"
												}
											]
										}
									},
									"status": "Not Found",
									"code": 404,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 10:26:09 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"errorCode\": \"error.not-found.dealId\"\n}"
								}
							]
						},
						{
							"name": "Close position",
							"event": [
								{
									"listen": "test",
									"script": {
										"exec": [
											""
										],
										"type": "text/javascript"
									}
								},
								{
									"listen": "prerequest",
									"script": {
										"exec": [
											""
										],
										"type": "text/javascript"
									}
								}
							],
							"request": {
								"method": "DELETE",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/positions/:dealId",
									"host": [
										"{{url}}"
									],
									"path": [
										"positions",
										":dealId"
									],
									"variable": [
										{
											"key": "dealId",
											"value": "{{dealId}}",
											"description": "Permanent deal reference for a confirmed trade"
										}
									]
								},
								"description": "Close the position"
							},
							"response": [
								{
									"name": "Successful response",
									"originalRequest": {
										"method": "DELETE",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/positions/:dealId",
											"host": [
												"{{url}}"
											],
											"path": [
												"positions",
												":dealId"
											],
											"variable": [
												{
													"key": "dealId",
													"value": "006011e7-0001-54c4-0000-000080560068",
													"description": "Permanent deal reference for a confirmed trade"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 08:57:18 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"dealReference\": \"p_006011e7-0001-54c4-0000-000080560068\"\n}"
								},
								{
									"name": "Error: Position not found",
									"originalRequest": {
										"method": "DELETE",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/positions/:dealId",
											"host": [
												"{{url}}"
											],
											"path": [
												"positions",
												":dealId"
											],
											"variable": [
												{
													"key": "dealId",
													"value": "006011e7-0001-54c4-0000-000080560068",
													"description": "Permanent deal reference for a confirmed trade"
												}
											]
										}
									},
									"status": "Not Found",
									"code": 404,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 09:00:22 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"errorCode\": \"error.not-found.dealId\"\n}"
								}
							]
						}
					]
				},
				{
					"name": "Orders",
					"item": [
						{
							"name": "All working orders",
							"event": [
								{
									"listen": "test",
									"script": {
										"exec": [
											""
										],
										"type": "text/javascript"
									}
								}
							],
							"request": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/workingorders",
									"host": [
										"{{url}}"
									],
									"path": [
										"workingorders"
									]
								},
								"description": "Returns all open working orders for the active account"
							},
							"response": [
								{
									"name": "Successful response",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/workingorders",
											"host": [
												"{{url}}"
											],
											"path": [
												"workingorders"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 09:48:31 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"workingOrders\": [\n        {\n            \"workingOrderData\": {\n                \"dealId\": \"006011e7-0001-54c4-0000-000080560078\",\n                \"direction\": \"BUY\",\n                \"epic\": \"SILVER\",\n                \"orderSize\": 1,\n                \"orderLevel\": 20,\n                \"timeInForce\": \"GOOD_TILL_DATE\",\n                \"goodTillDate\": \"2022-06-09T04:01:00.000\",\n                \"goodTillDateUTC\": \"2022-06-09T01:01:00.000\",\n                \"createdDate\": \"2022-04-06T12:48:28.114\",\n                \"createdDateUTC\": \"2022-04-06T09:48:28.114\",\n                \"guaranteedStop\": true,\n                \"orderType\": \"LIMIT\",\n                \"stopDistance\": -3,\n                \"profitDistance\": 3,\n                \"currencyCode\": \"USD\"\n            },\n            \"marketData\": {\n                \"instrumentName\": \"Silver\",\n                \"expiry\": \"-\",\n                \"marketStatus\": \"TRADEABLE\",\n                \"epic\": \"SILVER\",\n                \"instrumentType\": \"COMMODITIES\",\n                \"lotSize\": 50,\n                \"high\": 24.398,\n                \"low\": 24.193,\n                \"percentageChange\": -0.6198,\n                \"netChange\": -0.152,\n                \"bid\": 24.387,\n                \"offer\": 24.407,\n                \"updateTime\": \"2022-04-06T12:48:31.587\",\n                \"updateTimeUTC\": \"2022-04-06T09:48:31.587\",\n                \"delayTime\": 0,\n                \"streamingPricesAvailable\": true,\n                \"scalingFactor\": 1\n            }\n        },\n        {\n            \"workingOrderData\": {\n                \"dealId\": \"00018387-0001-54c4-0000-000080560019\",\n                \"direction\": \"BUY\",\n                \"epic\": \"NATURALGAS\",\n                \"orderSize\": 1,\n                \"orderLevel\": 6,\n                \"timeInForce\": \"GOOD_TILL_CANCELLED\",\n                \"createdDate\": \"2022-04-06T12:13:46.571\",\n                \"createdDateUTC\": \"2022-04-06T09:13:46.571\",\n                \"guaranteedStop\": false,\n                \"orderType\": \"LIMIT\",\n                \"currencyCode\": \"USD\"\n            },\n            \"marketData\": {\n                \"instrumentName\": \"Natural Gas\",\n                \"expiry\": \"-\",\n                \"marketStatus\": \"TRADEABLE\",\n                \"epic\": \"NATURALGAS\",\n                \"instrumentType\": \"COMMODITIES\",\n                \"lotSize\": 1000,\n                \"high\": 6.194,\n                \"low\": 6.073,\n                \"percentageChange\": 6.4472,\n                \"netChange\": 0.374,\n                \"bid\": 6.185,\n                \"offer\": 6.195,\n                \"updateTime\": \"2022-04-06T12:48:24.795\",\n                \"updateTimeUTC\": \"2022-04-06T09:48:24.795\",\n                \"delayTime\": 0,\n                \"streamingPricesAvailable\": true,\n                \"scalingFactor\": 1\n            }\n        }\n    ]\n}"
								}
							]
						},
						{
							"name": "Create working order",
							"event": [
								{
									"listen": "test",
									"script": {
										"exec": [
											"pm.environment.set(\"dealReference\", pm.response.json().dealReference);",
											""
										],
										"type": "text/javascript"
									}
								},
								{
									"listen": "prerequest",
									"script": {
										"exec": [
											""
										],
										"type": "text/javascript"
									}
								}
							],
							"protocolProfileBehavior": {
								"disabledSystemHeaders": {}
							},
							"request": {
								"method": "POST",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"epic\": \"SILVER\",\n    \"direction\": \"BUY\",\n    \"size\": 1,\n    \"level\": 20,\n    \"type\": \"LIMIT\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{url}}/workingorders",
									"host": [
										"{{url}}"
									],
									"path": [
										"workingorders"
									]
								},
								"description": "Create a limit or stop order\n\nList of request body parameters:\n\n| **Parameter** | **Format** | **Required?** | **Description** |\n| --- | --- | --- | --- |\n| direction | string | YES | Order direction  <br>  <br>Must be `BUY` or `SELL` |\n| epic | string | YES | Instrument epic identifier |\n| size | number | YES | Order size |\n| level | number | YES | Order price |\n| type | string | YES | Order type  <br>  <br>Must be `LIMIT` or `STOP` |\n| goodTillDate | string | NO | Order cancellation date in UTC time  <br>  <br>Date format: `YYYY-MM-DDTHH:MM:SS` (e.g. `2022-06-09T01:01:00`) |\n| guaranteedStop | boolean | NO | Must be `true` if a guaranteed stop is required  <br>  <br>Notes:  <br>\\- Default value: `false`  <br>\\- If `guaranteedStop` equals `true`, then set `stopLevel`, `stopDistance` or `stopAmount`  <br>\\- Cannot be set if `trailingStop` is `true`  <br>\\- Cannot be set if `hedgingMode` is `true` |\n| trailingStop | boolean | NO | Must be `true` if a trailing stop is required  <br>  <br>Notes:  <br>\\- Default value: `false`  <br>\\- If `trailingStop` equals `true`, then set `stopDistance`  <br>\\- Cannot be set if `guaranteedStop` is `true` |\n| stopLevel | number | NO | Price level when a stop loss will be triggered |\n| stopDistance | number | NO | Distance between current and stop loss triggering price  <br>  <br>Notes:  <br>\\- Required parameter if `trailingStop` is `true` |\n| stopAmount | number | NO | Loss amount when a stop loss will be triggered |\n| profitLevel | number | NO | Price level when a take profit will be triggered |\n| profitDistance | number | NO | Distance between current and take profit triggering price |\n| profitAmount | number | NO | Profit amount when a take profit will be triggered |"
							},
							"response": [
								{
									"name": "Success: Create limit order",
									"originalRequest": {
										"method": "POST",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"body": {
											"mode": "raw",
											"raw": "{\n\t\"epic\": \"SILVER\",\n\t\"direction\": \"BUY\",\n\t\"size\": 1,\n\t\"level\": 22,\n\t\"type\": \"LIMIT\"\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{url}}/workingorders",
											"host": [
												"{{url}}"
											],
											"path": [
												"workingorders"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 09:37:44 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"dealReference\": \"o_307bb379-6dd8-4ea7-8935-faf725f0e0a3\"\n}"
								},
								{
									"name": "Success: Create order with stop loss, take profit, guaranteed stop and cancellation date",
									"originalRequest": {
										"method": "POST",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"epic\": \"SILVER\",\n    \"direction\": \"BUY\",\n    \"size\": 1,\n    \"level\": 20,\n    \"type\": \"LIMIT\",\n    \"goodTillDate\": \"2022-06-09T01:01:00\",\n    \"guaranteedStop\": true,\n    \"stopLevel\": 17,\n    \"profitLevel\": 23\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{url}}/workingorders",
											"host": [
												"{{url}}"
											],
											"path": [
												"workingorders"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 09:39:00 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"dealReference\": \"o_d556dcbb-75b5-491f-90ed-6ff899262d05\"\n}"
								},
								{
									"name": "Error: Cancellation date in the past",
									"originalRequest": {
										"method": "POST",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"epic\": \"SILVER\",\n    \"direction\": \"BUY\",\n    \"size\": 1,\n    \"level\": 20,\n    \"type\": \"LIMIT\",\n    \"goodTillDate\": \"2020-06-09T01:01:00\"\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{url}}/workingorders",
											"host": [
												"{{url}}"
											],
											"path": [
												"workingorders"
											]
										}
									},
									"status": "Bad Request",
									"code": 400,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 09:43:10 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"errorCode\": \"error.not-in-future.goodTillDate\"\n}"
								}
							]
						},
						{
							"name": "Update working order",
							"event": [
								{
									"listen": "test",
									"script": {
										"exec": [
											""
										],
										"type": "text/javascript"
									}
								}
							],
							"request": {
								"method": "PUT",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"goodTillDate\": \"2022-06-09T01:01:00\",\n    \"guaranteedStop\": true,\n    \"stopDistance\": 4,\n    \"profitDistance\": 4\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{url}}/workingorders/:dealId",
									"host": [
										"{{url}}"
									],
									"path": [
										"workingorders",
										":dealId"
									],
									"variable": [
										{
											"key": "dealId",
											"value": "{{dealId}}",
											"description": "Permanent deal reference for an order"
										}
									]
								},
								"description": "Update a limit or stop order\n\nList of request body parameters:\n\n| **Parameter** | **Format** | **Required?** | **Description** |\n| --- | --- | --- | --- |\n| level | number | NO | Order price |\n| goodTillDate | string | NO | Order cancellation date in UTC time  <br>  <br>Date format: `YYYY-MM-DDTHH:MM:SS` (e.g. `2022-06-09T01:01:00`) |\n| guaranteedStop | boolean | NO | Must be `true` if a guaranteed stop is required  <br>  <br>Notes:  <br>\\- Default value: `false`  <br>\\- If `guaranteedStop` equals `true`, then set `stopLevel`, `stopDistance` or `stopAmount`  <br>\\- Cannot be set if `trailingStop` is `true`  <br>\\- Cannot be set if `hedgingMode` is `true` |\n| trailingStop | boolean | NO | Must be `true` if a trailing stop is required  <br>  <br>Notes:  <br>\\- Default value: `false`  <br>\\- If `trailingStop` equals `true`, then set `stopDistance`  <br>\\- Cannot be set if `guaranteedStop` is `true` |\n| stopLevel | number | NO | Price level when a stop loss will be triggered |\n| stopDistance | number | NO | Distance between current and stop loss triggering price  <br>  <br>Notes:  <br>\\- Required parameter if `trailingStop` is `true` |\n| stopAmount | number | NO | Loss amount when a stop loss will be triggered |\n| profitLevel | number | NO | Price level when a take profit will be triggered |\n| profitDistance | number | NO | Distance between current and take profit triggering price |\n| profitAmount | number | NO | Profit amount when a take profit will be triggered |"
							},
							"response": [
								{
									"name": "Success: Update stop loss, take profit, guaranteed stop and cancellation date",
									"originalRequest": {
										"method": "PUT",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"goodTillDate\": \"2022-06-09T01:01:00\",\n    \"guaranteedStop\": true,\n    \"stopDistance\": 4,\n    \"profitDistance\": 4\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{url}}/workingorders/:dealId",
											"host": [
												"{{url}}"
											],
											"path": [
												"workingorders",
												":dealId"
											],
											"variable": [
												{
													"key": "dealId",
													"value": "006011e7-0001-54c4-0000-00008056007a"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 10:23:35 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"dealReference\": \"o_56e73aad-45fe-4058-a05b-569b1a6e8ba0\"\n}"
								},
								{
									"name": "Error: Order not found",
									"originalRequest": {
										"method": "PUT",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"goodTillDate\": \"2022-06-09T01:01:00\",\n    \"guaranteedStop\": true,\n    \"stopDistance\": 4,\n    \"profitDistance\": 4\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{url}}/workingorders/:dealId",
											"host": [
												"{{url}}"
											],
											"path": [
												"workingorders",
												":dealId"
											],
											"variable": [
												{
													"key": "dealId",
													"value": "006011e7-0001-54c4-0000-000080560069"
												}
											]
										}
									},
									"status": "Not Found",
									"code": 404,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 10:27:56 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"errorCode\": \"error.not-found.dealId\"\n}"
								}
							]
						},
						{
							"name": "Delete working order",
							"event": [
								{
									"listen": "test",
									"script": {
										"exec": [
											""
										],
										"type": "text/javascript"
									}
								}
							],
							"request": {
								"method": "DELETE",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/workingorders/:dealId",
									"host": [
										"{{url}}"
									],
									"path": [
										"workingorders",
										":dealId"
									],
									"variable": [
										{
											"key": "dealId",
											"value": "{{dealId}}",
											"description": "Permanent deal reference for an order"
										}
									]
								},
								"description": "Delete a limit or stop order"
							},
							"response": [
								{
									"name": "Successful response",
									"originalRequest": {
										"method": "DELETE",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/workingorders/:dealId",
											"host": [
												"{{url}}"
											],
											"path": [
												"workingorders",
												":dealId"
											],
											"variable": [
												{
													"key": "dealId",
													"value": "",
													"description": "Permanent deal reference for an order"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 10:32:53 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"dealReference\": \"o_38323f0c-241a-43b3-8edf-a75d2ae989a5\"\n}"
								},
								{
									"name": "Error: Order not found",
									"originalRequest": {
										"method": "DELETE",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/workingorders/:dealId",
											"host": [
												"{{url}}"
											],
											"path": [
												"workingorders",
												":dealId"
											],
											"variable": [
												{
													"key": "dealId",
													"value": "006011e7-0001-54c4-0000-000080560069",
													"description": "Permanent deal reference for an order"
												}
											]
										}
									},
									"status": "Not Found",
									"code": 404,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 10:31:59 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"errorCode\": \"error.not-found.dealId\"\n}"
								}
							]
						}
					]
				},
				{
					"name": "Position/Order confirmation",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									""
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "GET",
						"header": [
							{
								"key": "X-SECURITY-TOKEN",
								"value": "{{X-SECURITY-TOKEN}}",
								"type": "text",
								"description": "Account token identifying the client's current account"
							},
							{
								"key": "CST",
								"value": "{{CST}}",
								"type": "text",
								"description": "Access token identifying the client"
							}
						],
						"url": {
							"raw": "{{url}}/confirms/:dealReference",
							"host": [
								"{{url}}"
							],
							"path": [
								"confirms",
								":dealReference"
							],
							"variable": [
								{
									"key": "dealReference",
									"value": "{{dealReference}}",
									"description": "Deal reference for an unconfirmed trade"
								}
							]
						},
						"description": "Returns a deal confirmation for the given deal reference\n\nIn case of mentioning the order prefix formed because of the position creation the opened positions IDs will be shown in the `affectedDeals` array"
					},
					"response": [
						{
							"name": "Successful response",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/confirms/:dealReference",
									"host": [
										"{{url}}"
									],
									"path": [
										"confirms",
										":dealReference"
									],
									"variable": [
										{
											"key": "dealReference",
											"value": "o_fcc7e6c0-c150-48aa-bf66-d6c6da071f1a",
											"description": "Deal reference for an unconfirmed trade"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Wed, 06 Apr 2022 07:32:26 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"date\": \"2022-04-06T07:32:19.193\",\n    \"status\": \"OPEN\",\n    \"reason\": \"SUCCESS\",\n    \"dealStatus\": \"ACCEPTED\",\n    \"epic\": \"SILVER\",\n    \"dealReference\": \"o_fcc7e6c0-c150-48aa-bf66-d6c6da071f1a\",\n    \"dealId\": \"006011e7-0001-54c4-0000-000080560043\",\n    \"affectedDeals\": [\n        {\n            \"dealId\": \"006011e7-0001-54c4-0000-000080560045\",\n            \"status\": \"OPENED\"\n        }\n    ],\n    \"level\": 24.285,\n    \"size\": 1,\n    \"direction\": \"BUY\",\n    \"guaranteedStop\": false,\n    \"trailingStop\": false\n}"
						},
						{
							"name": "Error: Deal confirmation not found",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/confirms/:dealReference",
									"host": [
										"{{url}}"
									],
									"path": [
										"confirms",
										":dealReference"
									],
									"variable": [
										{
											"key": "dealReference",
											"value": "o_fcc7e6c0-c150-48aa-bf66-d6c6da071f2b",
											"description": "Deal reference for an unconfirmed trade"
										}
									]
								}
							},
							"status": "Not Found",
							"code": 404,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Wed, 06 Apr 2022 07:33:50 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"errorCode\": \"error.not-found.dealReference\"\n}"
						}
					]
				}
			]
		},
		{
			"name": "Markets Info",
			"item": [
				{
					"name": "Markets",
					"item": [
						{
							"name": "All top-level market categories",
							"event": [
								{
									"listen": "test",
									"script": {
										"exec": [
											""
										],
										"type": "text/javascript"
									}
								}
							],
							"request": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/marketnavigation",
									"host": [
										"{{url}}"
									],
									"path": [
										"marketnavigation"
									]
								},
								"description": "Returns all top-level nodes (market categories) in the market navigation hierarchy"
							},
							"response": [
								{
									"name": "Successful response",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/marketnavigation",
											"host": [
												"{{url}}"
											],
											"path": [
												"marketnavigation"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 10:55:20 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"nodes\": [\n        {\n            \"id\": \"hierarchy_v1.commons_group\",\n            \"name\": \"commons_group\"\n        },\n        {\n            \"id\": \"hierarchy_v1.commodities_group\",\n            \"name\": \"commodities_group\"\n        },\n        {\n            \"id\": \"hierarchy_v1.oil_markets_group\",\n            \"name\": \"oil_markets_group\"\n        }\n    ]\n}"
								}
							]
						},
						{
							"name": "All category sub-nodes",
							"event": [
								{
									"listen": "test",
									"script": {
										"exec": [
											""
										],
										"type": "text/javascript"
									}
								}
							],
							"request": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/marketnavigation/:nodeId?limit=500",
									"host": [
										"{{url}}"
									],
									"path": [
										"marketnavigation",
										":nodeId"
									],
									"query": [
										{
											"key": "limit",
											"value": "500",
											"description": "The maximum number of the markets in answer. Default = 500"
										}
									],
									"variable": [
										{
											"key": "nodeId",
											"value": "{{nodeId}}",
											"description": "Identifier of the node to browse"
										}
									]
								},
								"description": "Returns all sub-nodes (markets) of the given node (market category) in the market navigation hierarchy"
							},
							"response": [
								{
									"name": "Success: List of category sub-nodes",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/marketnavigation/:nodeId",
											"host": [
												"{{url}}"
											],
											"path": [
												"marketnavigation",
												":nodeId"
											],
											"variable": [
												{
													"key": "nodeId",
													"value": "hierarchy_v1.commons_group",
													"description": "Identifier of the node to browse"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 11:06:15 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "Content-Disposition",
											"value": "inline;filename=f.txt"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"nodes\": [\n        {\n            \"id\": \"hierarchy_v1.commons.most_traded\",\n            \"name\": \"Most Traded\"\n        },\n        {\n            \"id\": \"hierarchy_v1.commons.recently_traded\",\n            \"name\": \"Recently Traded\"\n        },\n        {\n            \"id\": \"hierarchy_v1.commons.new\",\n            \"name\": \"New\"\n        },\n        {\n            \"id\": \"hierarchy_v1.commons.top_gainers\",\n            \"name\": \"Top Risers\"\n        },\n        {\n            \"id\": \"hierarchy_v1.commons.top_losers\",\n            \"name\": \"Top Fallers\"\n        },\n        {\n            \"id\": \"hierarchy_v1.commons.most_volatile\",\n            \"name\": \"Most Volatile\"\n        },\n        {\n            \"id\": \"hierarchy_v1.commons.weekend_trading\",\n            \"name\": \"Weekend Trading\"\n        }\n    ]\n}"
								},
								{
									"name": "Success: List of markets in category with limit = 2",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/marketnavigation/:nodeId?limit=2",
											"host": [
												"{{url}}"
											],
											"path": [
												"marketnavigation",
												":nodeId"
											],
											"query": [
												{
													"key": "limit",
													"value": "2",
													"description": "The maximum number of the markets in answer. Default = 500"
												}
											],
											"variable": [
												{
													"key": "nodeId",
													"value": "hierarchy_v1.commodities",
													"description": "Identifier of the node to browse"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 11:13:16 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "Content-Disposition",
											"value": "inline;filename=f.txt"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"nodes\": [],\n    \"markets\": [\n        {\n            \"delayTime\": 0,\n            \"epic\": \"NATURALGAS\",\n            \"netChange\": 0.389,\n            \"lotSize\": 1,\n            \"expiry\": \"-\",\n            \"instrumentType\": \"COMMODITIES\",\n            \"instrumentName\": \"Natural Gas\",\n            \"high\": 6.212,\n            \"low\": 6.073,\n            \"percentageChange\": 6.7057,\n            \"updateTime\": \"2022-04-06T13:13:14.765\",\n            \"updateTimeUTC\": \"2022-04-06T11:13:14.765\",\n            \"bid\": 6.223,\n            \"offer\": 6.229,\n            \"streamingPricesAvailable\": true,\n            \"marketStatus\": \"TRADEABLE\",\n            \"scalingFactor\": 1\n        },\n        {\n            \"delayTime\": 0,\n            \"epic\": \"SILVER\",\n            \"netChange\": -0.266,\n            \"lotSize\": 1,\n            \"expiry\": \"-\",\n            \"instrumentType\": \"COMMODITIES\",\n            \"instrumentName\": \"Silver\",\n            \"high\": 24.405,\n            \"low\": 24.193,\n            \"percentageChange\": -1.0846,\n            \"updateTime\": \"2022-04-06T13:13:14.069\",\n            \"updateTimeUTC\": \"2022-04-06T11:13:14.069\",\n            \"bid\": 24.23,\n            \"offer\": 24.25,\n            \"streamingPricesAvailable\": true,\n            \"marketStatus\": \"TRADEABLE\",\n            \"scalingFactor\": 1\n        }\n    ]\n}"
								},
								{
									"name": "Error: Invalid limit parameter",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/marketnavigation/:nodeId?limit=0",
											"host": [
												"{{url}}"
											],
											"path": [
												"marketnavigation",
												":nodeId"
											],
											"query": [
												{
													"key": "limit",
													"value": "0",
													"description": "The maximum number of the markets in answer. Default = 500"
												}
											],
											"variable": [
												{
													"key": "nodeId",
													"value": "hierarchy_v1.commodities",
													"description": "Identifier of the node to browse"
												}
											]
										}
									},
									"status": "Bad Request",
									"code": 400,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 11:13:16 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "Access-Control-Expose-Headers",
											"value": "CST, X-SECURITY-TOKEN"
										},
										{
											"key": "Content-Disposition",
											"value": "inline;filename=f.txt"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"errorCode\": \"error.invalid.limit\"\n}"
								}
							]
						},
						{
							"name": "Markets details",
							"event": [
								{
									"listen": "test",
									"script": {
										"exec": [
											""
										],
										"type": "text/javascript"
									}
								}
							],
							"request": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/markets?searchTerm=silver&epics=SILVER,NATURALGAS",
									"host": [
										"{{url}}"
									],
									"path": [
										"markets"
									],
									"query": [
										{
											"key": "searchTerm",
											"value": "silver",
											"description": "The term to be used in the search. Has higher priority, than 'epics' parameter meaning that in case both searchTerm and epic are mentioned only searchTerm is taken into consideration."
										},
										{
											"key": "epics",
											"value": "SILVER,NATURALGAS",
											"description": "The epics of the market, separated by a comma. Max number of epics is limited to 50"
										}
									]
								},
								"description": "Returns the details of all or specific markets\n\nIf query parameters are not specified in the request, the list of all available markets will be returned\n\nRequest can include one of the query parameters: `searchTerm` or `epics`\n\nIf both `searchTerm` or `epics` parameters are specified in the request, only `searchTerm` will be used (due to higher priority)"
							},
							"response": [
								{
									"name": "Successful response: searchTerm",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/markets?searchTerm=silver",
											"host": [
												"{{url}}"
											],
											"path": [
												"markets"
											],
											"query": [
												{
													"key": "searchTerm",
													"value": "silver",
													"description": "The term to be used in the search"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 13:17:39 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"markets\": [\n        {\n            \"delayTime\": 0,\n            \"epic\": \"SILVER\",\n            \"netChange\": -0.219,\n            \"lotSize\": 1,\n            \"expiry\": \"-\",\n            \"instrumentType\": \"COMMODITIES\",\n            \"instrumentName\": \"Silver\",\n            \"high\": 24.405,\n            \"low\": 24.119,\n            \"percentageChange\": -0.8929,\n            \"updateTime\": \"2022-04-06T15:17:38.477\",\n            \"updateTimeUTC\": \"2022-04-06T13:17:38.477\",\n            \"bid\": 24.366,\n            \"offer\": 24.386,\n            \"streamingPricesAvailable\": true,\n            \"marketStatus\": \"TRADEABLE\",\n            \"scalingFactor\": 1\n        },\n        {\n            \"delayTime\": 0,\n            \"epic\": \"5CPSG\",\n            \"netChange\": 0.005,\n            \"lotSize\": 1,\n            \"expiry\": \"-\",\n            \"instrumentType\": \"SHARES\",\n            \"instrumentName\": \"Silverlake Axis\",\n            \"high\": 0.318,\n            \"low\": 0.313,\n            \"percentageChange\": 1.5974,\n            \"updateTime\": \"2022-04-06T11:00:00.440\",\n            \"updateTimeUTC\": \"2022-04-06T09:00:00.440\",\n            \"bid\": 0.318,\n            \"offer\": 0.327,\n            \"streamingPricesAvailable\": true,\n            \"marketStatus\": \"CLOSED\",\n            \"scalingFactor\": 1\n        },\n        {\n            \"delayTime\": 0,\n            \"epic\": \"SI\",\n            \"lotSize\": 1,\n            \"expiry\": \"-\",\n            \"instrumentType\": \"SHARES\",\n            \"instrumentName\": \"Silvergate Capital Corporation\",\n            \"updateTime\": \"2022-04-05T21:59:59.446\",\n            \"updateTimeUTC\": \"2022-04-05T19:59:59.446\",\n            \"bid\": 142.7,\n            \"offer\": 143.67,\n            \"streamingPricesAvailable\": true,\n            \"marketStatus\": \"CLOSED\",\n            \"scalingFactor\": 1\n        }\n    ]\n}"
								},
								{
									"name": "Successful response: epics",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/markets?epics=SILVER,NATURALGAS",
											"host": [
												"{{url}}"
											],
											"path": [
												"markets"
											],
											"query": [
												{
													"key": "epics",
													"value": "SILVER,NATURALGAS",
													"description": "The epics of the market, separated by a comma. Max number of epics is limited to 50. Mandatory parameter"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 11:27:12 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"marketDetails\": [\n        {\n            \"instrument\": {\n                \"epic\": \"SILVER\",\n                \"expiry\": \"-\",\n                \"name\": \"Silver\",\n                \"lotSize\": 1,\n                \"type\": \"COMMODITIES\",\n                \"controlledRiskAllowed\": true,\n                \"streamingPricesAvailable\": true,\n                \"currency\": \"USD\",\n                \"marginFactor\": 10,\n                \"marginFactorUnit\": \"PERCENTAGE\",\n                \"openingHours\": {\n                    \"mon\": [\n                        \"00:00 - 22:00\",\n                        \"23:05 - 00:00\"\n                    ],\n                    \"tue\": [\n                        \"00:00 - 22:00\",\n                        \"23:05 - 00:00\"\n                    ],\n                    \"wed\": [\n                        \"00:00 - 22:00\",\n                        \"23:05 - 00:00\"\n                    ],\n                    \"thu\": [\n                        \"00:00 - 22:00\",\n                        \"23:05 - 00:00\"\n                    ],\n                    \"fri\": [\n                        \"00:00 - 22:00\"\n                    ],\n                    \"sat\": [],\n                    \"sun\": [\n                        \"23:05 - 00:00\"\n                    ],\n                    \"zone\": \"UTC\"\n                },\n                \"country\": \"\"\n            },\n            \"dealingRules\": {\n                \"minStepDistance\": {\n                    \"unit\": \"POINTS\",\n                    \"value\": 0.001\n                },\n                \"minDealSize\": {\n                    \"unit\": \"POINTS\",\n                    \"value\": 0.1\n                },\n                \"minControlledRiskStopDistance\": {\n                    \"unit\": \"PERCENTAGE\",\n                    \"value\": 2\n                },\n                \"minNormalStopOrLimitDistance\": {\n                    \"unit\": \"PERCENTAGE\",\n                    \"value\": 0.01\n                },\n                \"maxStopOrLimitDistance\": {\n                    \"unit\": \"PERCENTAGE\",\n                    \"value\": 60\n                },\n                \"marketOrderPreference\": \"AVAILABLE_DEFAULT_ON\",\n                \"trailingStopsPreference\": \"NOT_AVAILABLE\"\n            },\n            \"snapshot\": {\n                \"marketStatus\": \"TRADEABLE\",\n                \"netChange\": -0.335,\n                \"percentageChange\": -1.3659,\n                \"updateTime\": \"2022-04-06T13:27:10.153\",\n                \"delayTime\": 0,\n                \"bid\": 24.181,\n                \"offer\": 24.201,\n                \"high\": 24.405,\n                \"low\": 24.159,\n                \"decimalPlacesFactor\": 3,\n                \"scalingFactor\": 1\n            }\n        },\n        {\n            \"instrument\": {\n                \"epic\": \"NATURALGAS\",\n                \"expiry\": \"-\",\n                \"name\": \"Natural Gas\",\n                \"lotSize\": 1,\n                \"type\": \"COMMODITIES\",\n                \"controlledRiskAllowed\": true,\n                \"streamingPricesAvailable\": true,\n                \"currency\": \"USD\",\n                \"marginFactor\": 10,\n                \"marginFactorUnit\": \"PERCENTAGE\",\n                \"openingHours\": {\n                    \"mon\": [\n                        \"01:00 - 23:00\"\n                    ],\n                    \"tue\": [\n                        \"01:00 - 23:00\"\n                    ],\n                    \"wed\": [\n                        \"01:00 - 23:00\"\n                    ],\n                    \"thu\": [\n                        \"01:00 - 23:00\"\n                    ],\n                    \"fri\": [\n                        \"01:00 - 23:00\"\n                    ],\n                    \"sat\": [],\n                    \"sun\": [],\n                    \"zone\": \"UTC\"\n                },\n                \"country\": \"\"\n            },\n            \"dealingRules\": {\n                \"minStepDistance\": {\n                    \"unit\": \"POINTS\",\n                    \"value\": 0.001\n                },\n                \"minDealSize\": {\n                    \"unit\": \"POINTS\",\n                    \"value\": 0.1\n                },\n                \"minControlledRiskStopDistance\": {\n                    \"unit\": \"PERCENTAGE\",\n                    \"value\": 2\n                },\n                \"minNormalStopOrLimitDistance\": {\n                    \"unit\": \"PERCENTAGE\",\n                    \"value\": 0.1\n                },\n                \"maxStopOrLimitDistance\": {\n                    \"unit\": \"PERCENTAGE\",\n                    \"value\": 30\n                },\n                \"marketOrderPreference\": \"AVAILABLE_DEFAULT_ON\",\n                \"trailingStopsPreference\": \"NOT_AVAILABLE\"\n            },\n            \"snapshot\": {\n                \"marketStatus\": \"TRADEABLE\",\n                \"netChange\": 0.423,\n                \"percentageChange\": 7.2918,\n                \"updateTime\": \"2022-04-06T13:27:11.890\",\n                \"delayTime\": 0,\n                \"bid\": 6.294,\n                \"offer\": 6.3,\n                \"high\": 6.308,\n                \"low\": 6.073,\n                \"decimalPlacesFactor\": 3,\n                \"scalingFactor\": 1\n            }\n        }\n    ]\n}"
								},
								{
									"name": "Error: Empty searchTerm parameter",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/markets?searchTerm=",
											"host": [
												"{{url}}"
											],
											"path": [
												"markets"
											],
											"query": [
												{
													"key": "searchTerm",
													"value": "",
													"description": "The term to be used in the search"
												}
											]
										}
									},
									"status": "Bad Request",
									"code": 400,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 13:18:58 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"errorCode\": \"error.null.searchTerm\"\n}"
								},
								{
									"name": "Error: Empty epics parameter",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/markets",
											"host": [
												"{{url}}"
											],
											"path": [
												"markets"
											]
										}
									},
									"status": "Bad Request",
									"code": 400,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 11:28:34 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"errorCode\": \"error.null.epic\"\n}"
								}
							]
						},
						{
							"name": "Single market details",
							"request": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/markets/:epic",
									"host": [
										"{{url}}"
									],
									"path": [
										"markets",
										":epic"
									],
									"variable": [
										{
											"key": "epic",
											"value": "{{epic}}",
											"description": "The epic of the market"
										}
									]
								},
								"description": "Returns the details of the given market"
							},
							"response": [
								{
									"name": "Successful response",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/markets/:epic",
											"host": [
												"{{url}}"
											],
											"path": [
												"markets",
												":epic"
											],
											"variable": [
												{
													"key": "epic",
													"value": "SILVER",
													"description": "The epic of the market"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 11:17:42 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"instrument\": {\n        \"epic\": \"SILVER\",\n        \"expiry\": \"-\",\n        \"name\": \"Silver\",\n        \"lotSize\": 1,\n        \"type\": \"COMMODITIES\",\n        \"controlledRiskAllowed\": true,\n        \"streamingPricesAvailable\": true,\n        \"currency\": \"USD\",\n        \"marginFactor\": 10,\n        \"marginFactorUnit\": \"PERCENTAGE\",\n        \"openingHours\": {\n            \"mon\": [\n                \"00:00 - 22:00\",\n                \"23:05 - 00:00\"\n            ],\n            \"tue\": [\n                \"00:00 - 22:00\",\n                \"23:05 - 00:00\"\n            ],\n            \"wed\": [\n                \"00:00 - 22:00\",\n                \"23:05 - 00:00\"\n            ],\n            \"thu\": [\n                \"00:00 - 22:00\",\n                \"23:05 - 00:00\"\n            ],\n            \"fri\": [\n                \"00:00 - 22:00\"\n            ],\n            \"sat\": [],\n            \"sun\": [\n                \"23:05 - 00:00\"\n            ],\n            \"zone\": \"UTC\"\n        },\n        \"country\": \"\"\n    },\n    \"dealingRules\": {\n        \"minStepDistance\": {\n            \"unit\": \"POINTS\",\n            \"value\": 0.001\n        },\n        \"minDealSize\": {\n            \"unit\": \"POINTS\",\n            \"value\": 0.1\n        },\n        \"minControlledRiskStopDistance\": {\n            \"unit\": \"PERCENTAGE\",\n            \"value\": 2\n        },\n        \"minNormalStopOrLimitDistance\": {\n            \"unit\": \"PERCENTAGE\",\n            \"value\": 0.01\n        },\n        \"maxStopOrLimitDistance\": {\n            \"unit\": \"PERCENTAGE\",\n            \"value\": 60\n        },\n        \"marketOrderPreference\": \"AVAILABLE_DEFAULT_ON\",\n        \"trailingStopsPreference\": \"NOT_AVAILABLE\"\n    },\n    \"snapshot\": {\n        \"marketStatus\": \"TRADEABLE\",\n        \"netChange\": -0.313,\n        \"percentageChange\": -1.2762,\n        \"updateTime\": \"2022-04-06T13:17:42.113\",\n        \"delayTime\": 0,\n        \"bid\": 24.203,\n        \"offer\": 24.223,\n        \"high\": 24.405,\n        \"low\": 24.193,\n        \"decimalPlacesFactor\": 3,\n        \"scalingFactor\": 1\n    }\n}"
								},
								{
									"name": "Error: Market not found",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/markets/:epic",
											"host": [
												"{{url}}"
											],
											"path": [
												"markets",
												":epic"
											],
											"variable": [
												{
													"key": "epic",
													"value": "INVALID",
													"description": "The epic of the market"
												}
											]
										}
									},
									"status": "Not Found",
									"code": 404,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 11:18:28 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"errorCode\": \"error.not-found.epic\"\n}"
								}
							]
						}
					]
				},
				{
					"name": "Prices",
					"item": [
						{
							"name": "Historical prices",
							"event": [
								{
									"listen": "test",
									"script": {
										"exec": [
											""
										],
										"type": "text/javascript"
									}
								}
							],
							"request": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/prices/:epic?resolution=MINUTE&max=10&from=2022-02-24T00:00:00&to=2022-02-24T01:00:00",
									"host": [
										"{{url}}"
									],
									"path": [
										"prices",
										":epic"
									],
									"query": [
										{
											"key": "resolution",
											"value": "MINUTE",
											"description": "Defines the resolution of requested prices. Possible values are MINUTE, MINUTE_5, MINUTE_15, MINUTE_30, HOUR, HOUR_4, DAY, WEEK"
										},
										{
											"key": "max",
											"value": "10",
											"description": "The maximum number of the values in answer. Default = 10, max = 1000"
										},
										{
											"key": "from",
											"value": "2022-02-24T00:00:00",
											"description": "Start date. Date format: YYYY-MM-DDTHH:MM:SS (e.g. 2022-04-01T01:01:00). Filtration by date based on snapshotTimeUTC parameter"
										},
										{
											"key": "to",
											"value": "2022-02-24T01:00:00",
											"description": "End date. Date format: YYYY-MM-DDTHH:MM:SS (e.g. 2022-04-01T01:01:00). Filtration by date based on snapshotTimeUTC parameter"
										}
									],
									"variable": [
										{
											"key": "epic",
											"value": "{{epic}}",
											"description": "Instrument epic"
										}
									]
								},
								"description": "Returns historical prices for a particular instrument\n\nAll query parameters are optional for this request\n\nBy default returns the minute prices within the last 10 minutes"
							},
							"response": [
								{
									"name": "Success: Default response",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/prices/:epic",
											"host": [
												"{{url}}"
											],
											"path": [
												"prices",
												":epic"
											],
											"variable": [
												{
													"key": "epic",
													"value": "SILVER",
													"description": "Instrument epic"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 13:27:24 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"prices\": [\n        {\n            \"snapshotTime\": \"2022-04-06T15:18:00\",\n            \"snapshotTimeUTC\": \"2022-04-06T13:18:00\",\n            \"openPrice\": {\n                \"bid\": 24.356,\n                \"ask\": 24.376\n            },\n            \"closePrice\": {\n                \"bid\": 24.378,\n                \"ask\": 24.398\n            },\n            \"highPrice\": {\n                \"bid\": 24.378,\n                \"ask\": 24.398\n            },\n            \"lowPrice\": {\n                \"bid\": 24.355,\n                \"ask\": 24.375\n            },\n            \"lastTradedVolume\": 187\n        },\n        {\n            \"snapshotTime\": \"2022-04-06T15:19:00\",\n            \"snapshotTimeUTC\": \"2022-04-06T13:19:00\",\n            \"openPrice\": {\n                \"bid\": 24.379,\n                \"ask\": 24.399\n            },\n            \"closePrice\": {\n                \"bid\": 24.379,\n                \"ask\": 24.399\n            },\n            \"highPrice\": {\n                \"bid\": 24.389,\n                \"ask\": 24.409\n            },\n            \"lowPrice\": {\n                \"bid\": 24.373,\n                \"ask\": 24.393\n            },\n            \"lastTradedVolume\": 168\n        },\n        {\n            \"snapshotTime\": \"2022-04-06T15:20:00\",\n            \"snapshotTimeUTC\": \"2022-04-06T13:20:00\",\n            \"openPrice\": {\n                \"bid\": 24.378,\n                \"ask\": 24.398\n            },\n            \"closePrice\": {\n                \"bid\": 24.4,\n                \"ask\": 24.42\n            },\n            \"highPrice\": {\n                \"bid\": 24.4,\n                \"ask\": 24.42\n            },\n            \"lowPrice\": {\n                \"bid\": 24.375,\n                \"ask\": 24.395\n            },\n            \"lastTradedVolume\": 183\n        },\n        {\n            \"snapshotTime\": \"2022-04-06T15:21:00\",\n            \"snapshotTimeUTC\": \"2022-04-06T13:21:00\",\n            \"openPrice\": {\n                \"bid\": 24.399,\n                \"ask\": 24.419\n            },\n            \"closePrice\": {\n                \"bid\": 24.395,\n                \"ask\": 24.415\n            },\n            \"highPrice\": {\n                \"bid\": 24.405,\n                \"ask\": 24.425\n            },\n            \"lowPrice\": {\n                \"bid\": 24.388,\n                \"ask\": 24.408\n            },\n            \"lastTradedVolume\": 196\n        },\n        {\n            \"snapshotTime\": \"2022-04-06T15:22:00\",\n            \"snapshotTimeUTC\": \"2022-04-06T13:22:00\",\n            \"openPrice\": {\n                \"bid\": 24.394,\n                \"ask\": 24.414\n            },\n            \"closePrice\": {\n                \"bid\": 24.399,\n                \"ask\": 24.419\n            },\n            \"highPrice\": {\n                \"bid\": 24.4,\n                \"ask\": 24.42\n            },\n            \"lowPrice\": {\n                \"bid\": 24.383,\n                \"ask\": 24.403\n            },\n            \"lastTradedVolume\": 171\n        },\n        {\n            \"snapshotTime\": \"2022-04-06T15:23:00\",\n            \"snapshotTimeUTC\": \"2022-04-06T13:23:00\",\n            \"openPrice\": {\n                \"bid\": 24.398,\n                \"ask\": 24.418\n            },\n            \"closePrice\": {\n                \"bid\": 24.381,\n                \"ask\": 24.401\n            },\n            \"highPrice\": {\n                \"bid\": 24.405,\n                \"ask\": 24.425\n            },\n            \"lowPrice\": {\n                \"bid\": 24.38,\n                \"ask\": 24.4\n            },\n            \"lastTradedVolume\": 161\n        },\n        {\n            \"snapshotTime\": \"2022-04-06T15:24:00\",\n            \"snapshotTimeUTC\": \"2022-04-06T13:24:00\",\n            \"openPrice\": {\n                \"bid\": 24.38,\n                \"ask\": 24.4\n            },\n            \"closePrice\": {\n                \"bid\": 24.387,\n                \"ask\": 24.407\n            },\n            \"highPrice\": {\n                \"bid\": 24.399,\n                \"ask\": 24.419\n            },\n            \"lowPrice\": {\n                \"bid\": 24.38,\n                \"ask\": 24.4\n            },\n            \"lastTradedVolume\": 155\n        },\n        {\n            \"snapshotTime\": \"2022-04-06T15:25:00\",\n            \"snapshotTimeUTC\": \"2022-04-06T13:25:00\",\n            \"openPrice\": {\n                \"bid\": 24.388,\n                \"ask\": 24.408\n            },\n            \"closePrice\": {\n                \"bid\": 24.389,\n                \"ask\": 24.409\n            },\n            \"highPrice\": {\n                \"bid\": 24.393,\n                \"ask\": 24.413\n            },\n            \"lowPrice\": {\n                \"bid\": 24.384,\n                \"ask\": 24.404\n            },\n            \"lastTradedVolume\": 118\n        },\n        {\n            \"snapshotTime\": \"2022-04-06T15:26:00\",\n            \"snapshotTimeUTC\": \"2022-04-06T13:26:00\",\n            \"openPrice\": {\n                \"bid\": 24.389,\n                \"ask\": 24.409\n            },\n            \"closePrice\": {\n                \"bid\": 24.373,\n                \"ask\": 24.393\n            },\n            \"highPrice\": {\n                \"bid\": 24.39,\n                \"ask\": 24.41\n            },\n            \"lowPrice\": {\n                \"bid\": 24.37,\n                \"ask\": 24.39\n            },\n            \"lastTradedVolume\": 143\n        },\n        {\n            \"snapshotTime\": \"2022-04-06T15:27:00\",\n            \"snapshotTimeUTC\": \"2022-04-06T13:27:00\",\n            \"openPrice\": {\n                \"bid\": 24.372,\n                \"ask\": 24.392\n            },\n            \"closePrice\": {\n                \"bid\": 24.375,\n                \"ask\": 24.395\n            },\n            \"highPrice\": {\n                \"bid\": 24.376,\n                \"ask\": 24.396\n            },\n            \"lowPrice\": {\n                \"bid\": 24.371,\n                \"ask\": 24.391\n            },\n            \"lastTradedVolume\": 44\n        }\n    ],\n    \"instrumentType\": \"COMMODITIES\"\n}"
								},
								{
									"name": "Success: Use not default resolution, start date and max parameters",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/prices/:epic?resolution=MINUTE_15&max=4&from=2022-02-24T00:00:00",
											"host": [
												"{{url}}"
											],
											"path": [
												"prices",
												":epic"
											],
											"query": [
												{
													"key": "resolution",
													"value": "MINUTE_15",
													"description": "Defines the resolution of requested prices. Possible values are MINUTE, MINUTE_5, MINUTE_15, MINUTE_30, HOUR, HOUR_4, DAY, WEEK"
												},
												{
													"key": "max",
													"value": "4",
													"description": "The maximum number of the values in answer. Default = 10, max = 1000"
												},
												{
													"key": "from",
													"value": "2022-02-24T00:00:00",
													"description": "Start date. Date format: YYYY-MM-DDTHH:MM:SS (e.g. 2022-04-01T01:01:00). Filtration by date based on snapshotTimeUTC parameter"
												}
											],
											"variable": [
												{
													"key": "epic",
													"value": "SILVER",
													"description": "Instrument epic"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 14:26:30 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"prices\": [\n        {\n            \"snapshotTime\": \"2022-02-24T01:00:00\",\n            \"snapshotTimeUTC\": \"2022-02-24T00:00:00\",\n            \"openPrice\": {\n                \"bid\": 24.541,\n                \"ask\": 24.561\n            },\n            \"closePrice\": {\n                \"bid\": 24.527,\n                \"ask\": 24.547\n            },\n            \"highPrice\": {\n                \"bid\": 24.557,\n                \"ask\": 24.577\n            },\n            \"lowPrice\": {\n                \"bid\": 24.522,\n                \"ask\": 24.542\n            },\n            \"lastTradedVolume\": 858\n        },\n        {\n            \"snapshotTime\": \"2022-02-24T01:15:00\",\n            \"snapshotTimeUTC\": \"2022-02-24T00:15:00\",\n            \"openPrice\": {\n                \"bid\": 24.526,\n                \"ask\": 24.546\n            },\n            \"closePrice\": {\n                \"bid\": 24.532,\n                \"ask\": 24.552\n            },\n            \"highPrice\": {\n                \"bid\": 24.561,\n                \"ask\": 24.581\n            },\n            \"lowPrice\": {\n                \"bid\": 24.510,\n                \"ask\": 24.530\n            },\n            \"lastTradedVolume\": 1005\n        },\n        {\n            \"snapshotTime\": \"2022-02-24T01:30:00\",\n            \"snapshotTimeUTC\": \"2022-02-24T00:30:00\",\n            \"openPrice\": {\n                \"bid\": 24.531,\n                \"ask\": 24.551\n            },\n            \"closePrice\": {\n                \"bid\": 24.570,\n                \"ask\": 24.590\n            },\n            \"highPrice\": {\n                \"bid\": 24.578,\n                \"ask\": 24.598\n            },\n            \"lowPrice\": {\n                \"bid\": 24.531,\n                \"ask\": 24.551\n            },\n            \"lastTradedVolume\": 1214\n        },\n        {\n            \"snapshotTime\": \"2022-02-24T01:45:00\",\n            \"snapshotTimeUTC\": \"2022-02-24T00:45:00\",\n            \"openPrice\": {\n                \"bid\": 24.569,\n                \"ask\": 24.589\n            },\n            \"closePrice\": {\n                \"bid\": 24.583,\n                \"ask\": 24.603\n            },\n            \"highPrice\": {\n                \"bid\": 24.587,\n                \"ask\": 24.607\n            },\n            \"lowPrice\": {\n                \"bid\": 24.561,\n                \"ask\": 24.581\n            },\n            \"lastTradedVolume\": 771\n        }\n    ],\n    \"instrumentType\": \"COMMODITIES\"\n}"
								},
								{
									"name": "Error: Invalid resolution parameter",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/prices/:epic?resolution=MINUTE_3",
											"host": [
												"{{url}}"
											],
											"path": [
												"prices",
												":epic"
											],
											"query": [
												{
													"key": "resolution",
													"value": "MINUTE_3",
													"description": "Defines the resolution of requested prices. Possible values are MINUTE, MINUTE_5, MINUTE_15, MINUTE_30, HOUR, HOUR_4, DAY, WEEK"
												}
											],
											"variable": [
												{
													"key": "epic",
													"value": "SILVER",
													"description": "Instrument epic"
												}
											]
										}
									},
									"status": "Bad Request",
									"code": 400,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 14:28:17 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"errorCode\": \"error.invalid.resolution\"\n}"
								}
							]
						}
					]
				},
				{
					"name": "Client Sentiment",
					"item": [
						{
							"name": "Client sentiment for markets",
							"event": [
								{
									"listen": "test",
									"script": {
										"exec": [
											"pm.environment.set(\"marketId\", pm.response.json().clientSentiments[1].marketId)"
										],
										"type": "text/javascript"
									}
								}
							],
							"request": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/clientsentiment?marketIds=SILVER,NATURALGAS",
									"host": [
										"{{url}}"
									],
									"path": [
										"clientsentiment"
									],
									"query": [
										{
											"key": "marketIds",
											"value": "SILVER,NATURALGAS",
											"description": "Comma separated list of market identifiers"
										}
									]
								},
								"description": "Returns the client sentiment for the given market"
							},
							"response": [
								{
									"name": "Successful response",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/clientsentiment/?marketIds=SILVER,NATURALGAS",
											"host": [
												"{{url}}"
											],
											"path": [
												"clientsentiment",
												""
											],
											"query": [
												{
													"key": "marketIds",
													"value": "SILVER,NATURALGAS",
													"description": "Comma separated list of market identifiers"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 15:36:36 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"clientSentiments\": [\n        {\n            \"marketId\": \"SILVER\",\n            \"longPositionPercentage\": 91.85,\n            \"shortPositionPercentage\": 8.15\n        },\n        {\n            \"marketId\": \"NATURALGAS\",\n            \"longPositionPercentage\": 62.97,\n            \"shortPositionPercentage\": 37.03\n        }\n    ]\n}"
								},
								{
									"name": "Error: Market not found",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/clientsentiment/?marketIds=NOTFOUND",
											"host": [
												"{{url}}"
											],
											"path": [
												"clientsentiment",
												""
											],
											"query": [
												{
													"key": "marketIds",
													"value": "NOTFOUND",
													"description": "Comma separated list of market identifiers"
												}
											]
										}
									},
									"status": "Not Found",
									"code": 404,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 15:37:10 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"errorCode\": \"error.not-found.epic\"\n}"
								}
							]
						},
						{
							"name": "Client sentiment for market",
							"request": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/clientsentiment/:marketId",
									"host": [
										"{{url}}"
									],
									"path": [
										"clientsentiment",
										":marketId"
									],
									"variable": [
										{
											"key": "marketId",
											"value": "{{marketId}}",
											"description": "Market identifier"
										}
									]
								},
								"description": "Returns the client sentiment for the given market"
							},
							"response": [
								{
									"name": "Successful response",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/clientsentiment/:marketId",
											"host": [
												"{{url}}"
											],
											"path": [
												"clientsentiment",
												":marketId"
											],
											"variable": [
												{
													"key": "marketId",
													"value": "SILVER",
													"description": "Market identifier"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 15:34:26 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"marketId\": \"SILVER\",\n    \"longPositionPercentage\": 91.85,\n    \"shortPositionPercentage\": 8.15\n}"
								},
								{
									"name": "Error: Market not found",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "X-SECURITY-TOKEN",
												"value": "{{X-SECURITY-TOKEN}}",
												"type": "text",
												"description": "Account token identifying the client's current account"
											},
											{
												"key": "CST",
												"value": "{{CST}}",
												"type": "text",
												"description": "Access token identifying the client"
											}
										],
										"url": {
											"raw": "{{url}}/clientsentiment/:marketId",
											"host": [
												"{{url}}"
											],
											"path": [
												"clientsentiment",
												":marketId"
											],
											"variable": [
												{
													"key": "marketId",
													"value": "NOTFOUND",
													"description": "Market identifier"
												}
											]
										}
									},
									"status": "Not Found",
									"code": 404,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 06 Apr 2022 15:40:43 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Vary",
											"value": "Origin"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Method"
										},
										{
											"key": "Vary",
											"value": "Access-Control-Request-Headers"
										},
										{
											"key": "Content-Security-Policy",
											"value": "connect-src 'self'"
										},
										{
											"key": "CST",
											"value": "CST_TOKEN"
										},
										{
											"key": "X-SECURITY-TOKEN",
											"value": "SECURITY_TOKEN"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "X-XSS-Protection",
											"value": "1; mode=block"
										},
										{
											"key": "Cache-Control",
											"value": "no-cache, no-store, max-age=0, must-revalidate"
										},
										{
											"key": "Pragma",
											"value": "no-cache"
										},
										{
											"key": "Expires",
											"value": "0"
										},
										{
											"key": "X-Frame-Options",
											"value": "DENY"
										}
									],
									"cookie": [],
									"body": "{\n    \"errorCode\": \"error.not-found.epic\"\n}"
								}
							]
						}
					]
				}
			]
		},
		{
			"name": "Watchlists",
			"item": [
				{
					"name": "All watchlists",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									""
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "GET",
						"header": [
							{
								"key": "X-SECURITY-TOKEN",
								"value": "{{X-SECURITY-TOKEN}}",
								"type": "text",
								"description": "Account token identifying the client's current account"
							},
							{
								"key": "CST",
								"value": "{{CST}}",
								"type": "text",
								"description": "Access token identifying the client"
							}
						],
						"url": {
							"raw": "{{url}}/watchlists",
							"host": [
								"{{url}}"
							],
							"path": [
								"watchlists"
							]
						},
						"description": "Returns all watchlists belonging to the current user"
					},
					"response": [
						{
							"name": "Successful response",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/watchlists",
									"host": [
										"{{url}}"
									],
									"path": [
										"watchlists"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Wed, 06 Apr 2022 14:42:31 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"watchlists\": [\n        {\n            \"id\": \"123456\",\n            \"name\": \"Hello world\",\n            \"editable\": true,\n            \"deleteable\": true,\n            \"defaultSystemWatchlist\": false\n        },\n        {\n            \"id\": \"123457\",\n            \"name\": \"watchlist1\",\n            \"editable\": true,\n            \"deleteable\": true,\n            \"defaultSystemWatchlist\": false\n        }\n    ]\n}"
						}
					]
				},
				{
					"name": "Single watchlist",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									""
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "GET",
						"header": [
							{
								"key": "X-SECURITY-TOKEN",
								"value": "{{X-SECURITY-TOKEN}}",
								"type": "text",
								"description": "Account token identifying the client's current account"
							},
							{
								"key": "CST",
								"value": "{{CST}}",
								"type": "text",
								"description": "Access token identifying the client"
							}
						],
						"url": {
							"raw": "{{url}}/watchlists/:watchlistId",
							"host": [
								"{{url}}"
							],
							"path": [
								"watchlists",
								":watchlistId"
							],
							"variable": [
								{
									"key": "watchlistId",
									"value": "{{watchlistId}}",
									"description": "Identifier of the watchlist"
								}
							]
						},
						"description": "Returns a watchlist for the given watchlist identifier"
					},
					"response": [
						{
							"name": "Successful response",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/watchlists/:watchlistId",
									"host": [
										"{{url}}"
									],
									"path": [
										"watchlists",
										":watchlistId"
									],
									"variable": [
										{
											"key": "watchlistId",
											"value": "123456",
											"description": "Identifier of the watchlist"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Wed, 06 Apr 2022 14:45:06 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"markets\": [\n        {\n            \"instrumentName\": \"Silver\",\n            \"expiry\": \"-\",\n            \"epic\": \"SILVER\",\n            \"instrumentType\": \"COMMODITIES\",\n            \"marketStatus\": \"TRADEABLE\",\n            \"lotSize\": 50,\n            \"high\": 24.558,\n            \"low\": 24.119,\n            \"percentageChange\": -0.4689,\n            \"netChange\": -0.115,\n            \"bid\": 24.395,\n            \"offer\": 24.415,\n            \"updateTime\": \"2022-04-06T17:45:05.197\",\n            \"updateTimeUTC\": \"2022-04-06T14:45:05.197\",\n            \"delayTime\": 0,\n            \"streamingPricesAvailable\": true,\n            \"scalingFactor\": 1\n        },\n        {\n            \"instrumentName\": \"Natural Gas\",\n            \"expiry\": \"-\",\n            \"epic\": \"NATURALGAS\",\n            \"instrumentType\": \"COMMODITIES\",\n            \"marketStatus\": \"TRADEABLE\",\n            \"lotSize\": 1000,\n            \"high\": 6.431,\n            \"low\": 6.073,\n            \"percentageChange\": 9.7397,\n            \"netChange\": 0.565,\n            \"bid\": 6.332,\n            \"offer\": 6.34,\n            \"updateTime\": \"2022-04-06T17:45:05.694\",\n            \"updateTimeUTC\": \"2022-04-06T14:45:05.694\",\n            \"delayTime\": 0,\n            \"streamingPricesAvailable\": true,\n            \"scalingFactor\": 1\n        }\n    ]\n}"
						},
						{
							"name": "Error: Watchlist not found",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/watchlists/:watchlistId",
									"host": [
										"{{url}}"
									],
									"path": [
										"watchlists",
										":watchlistId"
									],
									"variable": [
										{
											"key": "watchlistId",
											"value": "00001",
											"description": "Identifier of the watchlist"
										}
									]
								}
							},
							"status": "Not Found",
							"code": 404,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Wed, 06 Apr 2022 14:46:38 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"errorCode\": \"error.invalid.watchlist\"\n}"
						}
					]
				},
				{
					"name": "Create watchlist",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									""
								],
								"type": "text/javascript"
							}
						}
					],
					"protocolProfileBehavior": {
						"disabledSystemHeaders": {}
					},
					"request": {
						"method": "POST",
						"header": [
							{
								"key": "X-SECURITY-TOKEN",
								"value": "{{X-SECURITY-TOKEN}}",
								"type": "text",
								"description": "Account token identifying the client's current account"
							},
							{
								"key": "CST",
								"value": "{{CST}}",
								"type": "text",
								"description": "Access token identifying the client"
							}
						],
						"body": {
							"mode": "raw",
							"raw": "{\n\t\"epics\": [\n\t\t\"SILVER\",\n\t\t\"NATURALGAS\"\n\t],\n\t\"name\": \"Lorem\"\n}",
							"options": {
								"raw": {
									"language": "json"
								}
							}
						},
						"url": {
							"raw": "{{url}}/watchlists",
							"host": [
								"{{url}}"
							],
							"path": [
								"watchlists"
							]
						},
						"description": "Create a watchlist\n\nList of request body parameters:\n\n| **Parameter** | **Format** | **Required?** | **Description** |\n| --- | --- | --- | --- |\n| name | string | YES | Watchlist name  <br>  <br>Min length = 1  <br>Max length = 20 |\n| epics | array\\[string\\] | NO | List of market epics to be associated with this new watchlist |"
					},
					"response": [
						{
							"name": "Success: Watchlist created",
							"originalRequest": {
								"method": "POST",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n\t\"name\": \"Lorem ipsum\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{url}}/watchlists",
									"host": [
										"{{url}}"
									],
									"path": [
										"watchlists"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Wed, 06 Apr 2022 15:13:16 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"watchlistId\": \"123458\",\n    \"status\": \"SUCCESS\"\n}"
						},
						{
							"name": "Success: Not all instruments added",
							"originalRequest": {
								"method": "POST",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n\t\"epics\": [\n\t\t\"SILVER\",\n\t\t\"NATURALGAS\",\n\t\t\"NOTFOUND\"\n\t],\n\t\"name\": \"Lorem\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{url}}/watchlists",
									"host": [
										"{{url}}"
									],
									"path": [
										"watchlists"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Wed, 06 Apr 2022 15:17:23 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"watchlistId\": \"123459\",\n    \"status\": \"SUCCESS_NOT_ALL_INSTRUMENTS_ADDED\"\n}"
						},
						{
							"name": "Error: Incorrect name length",
							"originalRequest": {
								"method": "POST",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n\t\"epics\": [\n\t\t\"SILVER\",\n\t\t\"NATURALGAS\"\n\t],\n\t\"name\": \"Lorem ipsum dolor sit amet\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{url}}/watchlists",
									"host": [
										"{{url}}"
									],
									"path": [
										"watchlists"
									]
								}
							},
							"status": "Bad Request",
							"code": 400,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Wed, 06 Apr 2022 15:14:41 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"errorCode\": \"error.size.createwatchlistrequest.name\"\n}"
						}
					]
				},
				{
					"name": "Add market to watchlist",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									""
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "PUT",
						"header": [
							{
								"key": "X-SECURITY-TOKEN",
								"value": "{{X-SECURITY-TOKEN}}",
								"type": "text",
								"description": "Account token identifying the client's current account"
							},
							{
								"key": "CST",
								"value": "{{CST}}",
								"type": "text",
								"description": "Access token identifying the client"
							}
						],
						"body": {
							"mode": "raw",
							"raw": "{\n    \"epic\": \"SILVER\"\n}",
							"options": {
								"raw": {
									"language": "json"
								}
							}
						},
						"url": {
							"raw": "{{url}}/watchlists/:watchlistId",
							"host": [
								"{{url}}"
							],
							"path": [
								"watchlists",
								":watchlistId"
							],
							"variable": [
								{
									"key": "watchlistId",
									"value": "{{watchlistId}}",
									"description": "Identifier of the watchlist"
								}
							]
						},
						"description": "Add a market to the watchlist\n\nList of request body parameters:\n\n| **Parameter** | **Format** | **Required?** | **Description** |\n| --- | --- | --- | --- |\n| epic | string | YES | Instrument epic identifier |"
					},
					"response": [
						{
							"name": "Success: Instrument added to the watchlist",
							"originalRequest": {
								"method": "PUT",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"epic\": \"SILVER\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{url}}/watchlists/:watchlistId",
									"host": [
										"{{url}}"
									],
									"path": [
										"watchlists",
										":watchlistId"
									],
									"variable": [
										{
											"key": "watchlistId",
											"value": "123456",
											"description": "Identifier of the watchlist"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Wed, 06 Apr 2022 15:21:50 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"SUCCESS\"\n}"
						},
						{
							"name": "Error: Instrument not found",
							"originalRequest": {
								"method": "PUT",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"epic\": \"NOTFOUND\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{url}}/watchlists/:watchlistId",
									"host": [
										"{{url}}"
									],
									"path": [
										"watchlists",
										":watchlistId"
									],
									"variable": [
										{
											"key": "watchlistId",
											"value": "123456",
											"description": "Identifier of the watchlist"
										}
									]
								}
							},
							"status": "Not Found",
							"code": 404,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Wed, 06 Apr 2022 15:23:13 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"errorCode\": \"error.not-found.epic\"\n}"
						}
					]
				},
				{
					"name": "Remove market from watchlist",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									""
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "DELETE",
						"header": [
							{
								"key": "X-SECURITY-TOKEN",
								"value": "{{X-SECURITY-TOKEN}}",
								"type": "text",
								"description": "Account token identifying the client's current account"
							},
							{
								"key": "CST",
								"value": "{{CST}}",
								"type": "text",
								"description": "Access token identifying the client"
							}
						],
						"url": {
							"raw": "{{url}}/watchlists/:watchlistId/:epic",
							"host": [
								"{{url}}"
							],
							"path": [
								"watchlists",
								":watchlistId",
								":epic"
							],
							"variable": [
								{
									"key": "watchlistId",
									"value": "{{watchlistId}}",
									"description": "Identifier of the watchlist"
								},
								{
									"key": "epic",
									"value": "{{epic}}",
									"description": "Instrument epic identifier"
								}
							]
						},
						"description": "Remove a market from the watchlist"
					},
					"response": [
						{
							"name": "Success: Instrument removed form the watchlist",
							"originalRequest": {
								"method": "DELETE",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/watchlists/:watchlistId/:epic",
									"host": [
										"{{url}}"
									],
									"path": [
										"watchlists",
										":watchlistId",
										":epic"
									],
									"variable": [
										{
											"key": "watchlistId",
											"value": "123456",
											"description": "Identifier of the watchlist"
										},
										{
											"key": "epic",
											"value": "SILVER",
											"description": "Instrument epic identifier"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Wed, 06 Apr 2022 15:24:50 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"SUCCESS\"\n}"
						},
						{
							"name": "Error: Instrument not found in the watchlist",
							"originalRequest": {
								"method": "DELETE",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/watchlists/:watchlistId/:epic",
									"host": [
										"{{url}}"
									],
									"path": [
										"watchlists",
										":watchlistId",
										":epic"
									],
									"variable": [
										{
											"key": "watchlistId",
											"value": "123456",
											"description": "Identifier of the watchlist"
										},
										{
											"key": "epic",
											"value": "GOLD",
											"description": "Instrument epic identifier"
										}
									]
								}
							},
							"status": "Not Found",
							"code": 404,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Wed, 06 Apr 2022 15:28:23 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"errorCode\": \"error.not-found.epic\"\n}"
						}
					]
				},
				{
					"name": "Delete watchlist",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									""
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "DELETE",
						"header": [
							{
								"key": "X-SECURITY-TOKEN",
								"value": "{{X-SECURITY-TOKEN}}",
								"type": "text",
								"description": "Account token identifying the client's current account"
							},
							{
								"key": "CST",
								"value": "{{CST}}",
								"type": "text",
								"description": "Access token identifying the client"
							}
						],
						"url": {
							"raw": "{{url}}/watchlists/:watchlistId",
							"host": [
								"{{url}}"
							],
							"path": [
								"watchlists",
								":watchlistId"
							],
							"variable": [
								{
									"key": "watchlistId",
									"value": "{{watchlistId}}",
									"description": "Identifier of the watchlist"
								}
							]
						},
						"description": "Delete the watchlist"
					},
					"response": [
						{
							"name": "Success: Watchlist deleted",
							"originalRequest": {
								"method": "DELETE",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/watchlists/:watchlistId",
									"host": [
										"{{url}}"
									],
									"path": [
										"watchlists",
										":watchlistId"
									],
									"variable": [
										{
											"key": "watchlistId",
											"value": "123456",
											"description": "Identifier of the watchlist"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Wed, 06 Apr 2022 15:31:25 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"SUCCESS\"\n}"
						},
						{
							"name": "Error: Watchlist not found",
							"originalRequest": {
								"method": "DELETE",
								"header": [
									{
										"key": "X-SECURITY-TOKEN",
										"value": "{{X-SECURITY-TOKEN}}",
										"type": "text",
										"description": "Account token identifying the client's current account"
									},
									{
										"key": "CST",
										"value": "{{CST}}",
										"type": "text",
										"description": "Access token identifying the client"
									}
								],
								"url": {
									"raw": "{{url}}/watchlists/:watchlistId",
									"host": [
										"{{url}}"
									],
									"path": [
										"watchlists",
										":watchlistId"
									],
									"variable": [
										{
											"key": "watchlistId",
											"value": "123450",
											"description": "Identifier of the watchlist"
										}
									]
								}
							},
							"status": "Not Found",
							"code": 404,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Wed, 06 Apr 2022 15:31:34 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Vary",
									"value": "Origin"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Method"
								},
								{
									"key": "Vary",
									"value": "Access-Control-Request-Headers"
								},
								{
									"key": "Content-Security-Policy",
									"value": "connect-src 'self'"
								},
								{
									"key": "CST",
									"value": "CST_TOKEN"
								},
								{
									"key": "X-SECURITY-TOKEN",
									"value": "SECURITY_TOKEN"
								},
								{
									"key": "X-Content-Type-Options",
									"value": "nosniff"
								},
								{
									"key": "X-XSS-Protection",
									"value": "1; mode=block"
								},
								{
									"key": "Cache-Control",
									"value": "no-cache, no-store, max-age=0, must-revalidate"
								},
								{
									"key": "Pragma",
									"value": "no-cache"
								},
								{
									"key": "Expires",
									"value": "0"
								},
								{
									"key": "X-Frame-Options",
									"value": "DENY"
								}
							],
							"cookie": [],
							"body": "{\n    \"errorCode\": \"error.not-found.watchlist\"\n}"
						}
					]
				}
			]
		}
	],
	"event": [
		{
			"listen": "prerequest",
			"script": {
				"type": "text/javascript",
				"exec": [
					""
				]
			}
		},
		{
			"listen": "test",
			"script": {
				"type": "text/javascript",
				"exec": [
					"pm.test(\"Status code is 200\", () => pm.response.to.have.status(200));"
				]
			}
		}
	]
}