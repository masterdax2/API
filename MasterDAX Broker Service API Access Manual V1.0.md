---
title: MasterDAX Broker Service API Access Manual V1.0
---

<!-- TOC -->

- [1. Introduction](#1-introduction)
    - [1.1. Access Preparation](#11-access-preparation)
    - [1.2. Instructions for Trade Process](#12-instructions-for-trade-process)
        - [1.2.1. Broker’s User Trade Process](#121-brokers-user-trade-process)
        - [1.2.2. Broker Settlement Process](#122-broker-settlement-process)
    - [1.3. Request Interaction](#13-request-interaction)
        - [1.3.1. URI scheme](#131-uri-scheme)
        - [1.3.2. Instructions to Request Interaction](#132-instructions-to-request-interaction)
        - [1.3.3. Signature Method](#133-signature-method)
- [2. Standard Interface for the Exchange](#2-standard-interface-for-the-exchange)
    - [2.1. Configure Coins and symbols](#21-configure-coins-and-symbols)
        - [2.1.1. Broker Coin List](#211-broker-coin-list)
        - [2.1.2. Broker symbol List](#212-broker-symbol-list)
        - [2.1.3. Input Broker’s symbols and Handling Fees](#213-input-brokers-symbols-and-handling-fees)
        - [2.1.4. Query Broker’s Input symbols Fee](#214-query-brokers-input-symbols-fee)
            - [2.1.4.1. Single symbol query](#2141-single-symbol-query)
            - [2.1.4.2. All symbols list query](#2142-all-symbols-list-query)
    - [2.2. User Assets](#22-user-assets)
        - [2.2.1. Create a User](#221-create-a-user)
        - [2.2.2. Modify Whitelist Users](#222-modify-whitelist-users)
        - [2.2.3. User Assets Query](#223-user-assets-query)
    - [2.3. User Deposit](#23-user-deposit)
        - [2.3.1. Get User Deposit Address](#231-get-user-deposit-address)
        - [2.3.2. User Deposit Callback](#232-user-deposit-callback)
        - [2.3.3. Deposit Record Query](#233-deposit-record-query)
    - [2.4. Exchange](#24-exchange)
        - [2.4.1. Market Depth Query](#241-market-depth-query)
        - [2.4.2. Get K-line](#242-get-k-line)
        - [2.4.3. GET Historical trades](#243-get-historical-trades)
        - [2.4.4. 24H Data Query](#244-24h-data-query)
        - [2.4.5. User Trade Ordering](#245-user-trade-ordering)
        - [2.4.6. User Order Cancellation](#246-user-order-cancellation)
        - [2.4.7. User Order Status Query](#247-user-order-status-query)
        - [2.4.8. User In-progress Order List Query](#248-user-in-progress-order-list-query)
        - [2.4.9. User Processed Order Query](#249-user-processed-order-query)
        - [2.4.10. Query all User's trade Records](#2410-query-all-users-trade-records)
    - [2.5. User Withdrawal](#25-user-withdrawal)
        - [2.5.1. Broker User Coin Withdrawal Application](#251-broker-user-coin-withdrawal-application)
        - [2.5.2. Query User’s Amount to be Withdrawn](#252-query-users-amount-to-be-withdrawn)
        - [2.5.3. Query Withdrawals Unverified](#253-query-withdrawals-unverified)
        - [2.5.4. User Withdrawal Confirmation](#254-user-withdrawal-confirmation)
        - [2.5.5. Query User’s Total Amount Withdrawn](#255-query-users-total-amount-withdrawn)
        - [2.5.6. Query User’s Withdrawal Records](#256-query-users-withdrawal-records)
        - [2.5.7. User Withdrawal Callback](#257-user-withdrawal-callback)
- [3. Broker Settlement API](#3-broker-settlement-api)
    - [3.1. Settlement Account Asset Query](#31-settlement-account-asset-query)
    - [3.2. Settlement Account Asset Withdraw Application](#32-settlement-account-asset-withdraw-application)
    - [3.3. Settlement Account Asset Withdraw Status Callback](#33-settlement-account-asset-withdraw-status-callback)
    - [3.4. Settlement Account Asset Withdraw  Record Query](#34-settlement-account-asset-withdraw--record-query)
    - [3.5. symbol Sharing Ratio Query](#35-symbol-sharing-ratio-query)
    - [3.6. Settlement Record Query](#36-settlement-record-query)
- [4. Error Code](#4-error-code)
- [5. Appendix](#5-appendix)
    - [5.1. PUBLIC](#51-public)
        - [5.1.1. Depth](#511-depth)
            - [5.1.1.1. Parameters](#5111-parameters)
            - [5.1.1.2. Responses example](#5112-responses-example)
        - [5.1.2. HOURS](#512-hours)
            - [5.1.2.1. Responses example](#5121-responses-example)
        - [5.1.3. TRADED ORDER](#513-traded-order)
            - [5.1.3.1. Parameters](#5131-parameters)
            - [5.1.3.2. Responses example](#5132-responses-example)
    - [5.2. PRIVATE](#52-private)
        - [5.2.1. User asset query (based on the symbol that the broker supports and assigns to user symbol list)](#521-user-asset-query-based-on-the-symbol-that-the-broker-supports-and-assigns-to-user-symbol-list)
            - [5.2.1.1. Parameters](#5211-parameters)
            - [5.2.1.2. Responses](#5212-responses)
            - [5.2.1.3. Consumes](#5213-consumes)
            - [5.2.1.4. Produces](#5214-produces)
            - [5.2.1.5. Tags](#5215-tags)
        - [5.2.2. Get User deposit Address](#522-get-user-deposit-address)
            - [5.2.2.1. Parameters](#5221-parameters)
            - [5.2.2.2. Responses](#5222-responses)
            - [5.2.2.3. Consumes](#5223-consumes)
            - [5.2.2.4. Produces](#5224-produces)
            - [5.2.2.5. Tags](#5225-tags)
        - [5.2.3. Deposit Callback](#523-deposit-callback)
            - [5.2.3.1. Parameters](#5231-parameters)
            - [5.2.3.2. Responses](#5232-responses)
            - [5.2.3.3. Consumes](#5233-consumes)
            - [5.2.3.4. Produces](#5234-produces)
            - [5.2.3.5. Tags](#5235-tags)
        - [5.2.4. Broker Coin List Query (including Withdrawal Fee)](#524-broker-coin-list-query-including-withdrawal-fee)
            - [5.2.4.1. Parameters](#5241-parameters)
            - [5.2.4.2. Responses](#5242-responses)
            - [5.2.4.3. Consumes](#5243-consumes)
            - [5.2.4.4. Produces](#5244-produces)
            - [5.2.4.5. Tags](#5245-tags)
        - [5.2.5. Broker Settlement Account Asset Query](#525-broker-settlement-account-asset-query)
            - [5.2.5.1. Parameters](#5251-parameters)
            - [5.2.5.2. Responses](#5252-responses)
            - [5.2.5.3. Consumes](#5253-consumes)
            - [5.2.5.4. Produces](#5254-produces)
            - [5.2.5.5. Tags](#5255-tags)
        - [5.2.6. Get K-line (Paged Query)](#526-get-k-line-paged-query)
            - [5.2.6.1. Parameters](#5261-parameters)
            - [5.2.6.2. Responses](#5262-responses)
            - [5.2.6.3. Consumes](#5263-consumes)
            - [5.2.6.4. Produces](#5264-produces)
            - [5.2.6.5. Tags](#5265-tags)
        - [5.2.7. Broker User Deposit Record Query](#527-broker-user-deposit-record-query)
            - [5.2.7.1. Parameters](#5271-parameters)
            - [5.2.7.2. Responses](#5272-responses)
            - [5.2.7.3. Consumes](#5273-consumes)
            - [5.2.7.4. Produces](#5274-produces)
            - [5.2.7.5. Tags](#5275-tags)
        - [5.2.8. User Order Cancellation](#528-user-order-cancellation)
            - [5.2.8.1. Parameters](#5281-parameters)
            - [5.2.8.2. Responses](#5282-responses)
            - [5.2.8.3. Consumes](#5283-consumes)
            - [5.2.8.4. Produces](#5284-produces)
            - [5.2.8.5. Tags](#5285-tags)
        - [5.2.9. User in-progress Order List Query](#529-user-in-progress-order-list-query)
            - [5.2.9.1. Parameters](#5291-parameters)
            - [5.2.9.2. Responses](#5292-responses)
            - [5.2.9.3. Consumes](#5293-consumes)
            - [5.2.9.4. Produces](#5294-produces)
            - [5.2.9.5. Tags](#5295-tags)
        - [5.2.10. User Processed Order Status Query](#5210-user-processed-order-status-query)
            - [5.2.10.1. Parameters](#52101-parameters)
            - [5.2.10.2. Responses](#52102-responses)
            - [5.2.10.3. Consumes](#52103-consumes)
            - [5.2.10.4. Produces](#52104-produces)
            - [5.2.10.5. Tags](#52105-tags)
        - [5.2.11. User Trade Ordering](#5211-user-trade-ordering)
            - [5.2.11.1. Parameters](#52111-parameters)
            - [5.2.11.2. Responses](#52112-responses)
            - [5.2.11.3. Consumes](#52113-consumes)
            - [5.2.11.4. Produces](#52114-produces)
            - [5.2.11.5. Tags](#52115-tags)
        - [5.2.12. User Single Order Status Query](#5212-user-single-order-status-query)
            - [5.2.12.1. Parameters](#52121-parameters)
            - [5.2.12.2. Responses](#52122-responses)
            - [5.2.12.3. Consumes](#52123-consumes)
            - [5.2.12.4. Produces](#52124-produces)
            - [5.2.12.5. Tags](#52125-tags)
        - [5.2.13. Broker Settlement Record Query](#5213-broker-settlement-record-query)
            - [5.2.13.1. Parameters](#52131-parameters)
            - [5.2.13.2. Responses](#52132-responses)
            - [5.2.13.3. Consumes](#52133-consumes)
            - [5.2.13.4. Produces](#52134-produces)
            - [5.2.13.5. Tags](#52135-tags)
        - [5.2.14. Single symbol Query](#5214-single-symbol-query)
            - [5.2.14.1. Parameters](#52141-parameters)
            - [5.2.14.2. Responses](#52142-responses)
            - [5.2.14.3. Consumes](#52143-consumes)
            - [5.2.14.4. Produces](#52144-produces)
            - [5.2.14.5. Tags](#52145-tags)
        - [5.2.15. Query all symbols List](#5215-query-all-symbols-list)
            - [5.2.15.1. Parameters](#52151-parameters)
            - [5.2.15.2. Responses](#52152-responses)
            - [5.2.15.3. Consumes](#52153-consumes)
            - [5.2.15.4. Produces](#52154-produces)
            - [5.2.15.5. Tags](#52155-tags)
        - [5.2.16. Input Coil Pairs and Fees](#5216-input-coil-pairs-and-fees)
            - [5.2.16.1. Parameters](#52161-parameters)
            - [5.2.16.2. Responses](#52162-responses)
            - [5.2.16.3. Consumes](#52163-consumes)
            - [5.2.16.4. Produces](#52164-produces)
            - [5.2.16.5. Tags](#52165-tags)
        - [5.2.17. Symbol Sharing Ratio Query](#5217-symbol-sharing-ratio-query)
            - [5.2.17.1. Parameters](#52171-parameters)
            - [5.2.17.2. Responses](#52172-responses)
            - [5.2.17.3. Consumes](#52173-consumes)
            - [5.2.17.4. Produces](#52174-produces)
            - [5.2.17.5. Tags](#52175-tags)
        - [5.2.18. Symbol List Query by Coins](#5218-symbol-list-query-by-coins)
            - [5.2.18.1. Parameters](#52181-parameters)
            - [5.2.18.2. Responses](#52182-responses)
            - [5.2.18.3. Consumes](#52183-consumes)
            - [5.2.18.4. Produces](#52184-produces)
            - [5.2.18.5. Tags](#52185-tags)
        - [5.2.19. Broker User Trade Record Query](#5219-broker-user-trade-record-query)
            - [5.2.19.1. Parameters](#52191-parameters)
            - [5.2.19.2. Responses](#52192-responses)
            - [5.2.19.3. Consumes](#52193-consumes)
            - [5.2.19.4. Produces](#52194-produces)
            - [5.2.19.5. Tags](#52195-tags)
        - [5.2.20. Create User](#5220-create-user)
            - [5.2.20.1. Parameters](#52201-parameters)
            - [5.2.20.2. Responses](#52202-responses)
            - [5.2.20.3. Consumes](#52203-consumes)
            - [5.2.20.4. Produces](#52204-produces)
            - [5.2.20.5. Tags](#52205-tags)
        - [5.2.21. Modify Whitelist User](#5221-modify-whitelist-user)
            - [5.2.21.1. Parameters](#52211-parameters)
            - [5.2.21.2. Responses](#52212-responses)
            - [5.2.21.3. Consumes](#52213-consumes)
            - [5.2.21.4. Produces](#52214-produces)
            - [5.2.21.5. Tags](#52215-tags)
        - [5.2.22. Broker User Coin Withdrawal Confirmation](#5222-broker-user-coin-withdrawal-confirmation)
            - [5.2.22.1. Parameters](#52221-parameters)
            - [5.2.22.2. Responses](#52222-responses)
            - [5.2.22.3. Consumes](#52223-consumes)
            - [5.2.22.4. Produces](#52224-produces)
            - [5.2.22.5. Tags](#52225-tags)
        - [5.2.23. Query Balance to be Withdrawn](#5223-query-balance-to-be-withdrawn)
            - [5.2.23.1. Parameters](#52231-parameters)
            - [5.2.23.2. Responses](#52232-responses)
            - [5.2.23.3. Consumes](#52233-consumes)
            - [5.2.23.4. Produces](#52234-produces)
            - [5.2.23.5. Tags](#52235-tags)
        - [5.2.24. Total Withdrawals](#5224-total-withdrawals)
            - [5.2.24.1. Parameters](#52241-parameters)
            - [5.2.24.2. Responses](#52242-responses)
            - [5.2.24.3. Consumes](#52243-consumes)
            - [5.2.24.4. Produces](#52244-produces)
            - [5.2.24.5. Tags](#52245-tags)
        - [5.2.25. Single Coin Withdrawal Unverified](#5225-single-coin-withdrawal-unverified)
            - [5.2.25.1. Parameters](#52251-parameters)
            - [5.2.25.2. Responses](#52252-responses)
            - [5.2.25.3. Consumes](#52253-consumes)
            - [5.2.25.4. Produces](#52254-produces)
            - [5.2.25.5. Tags](#52255-tags)
        - [5.2.26. Broker Assets Withdraw Application](#5226-broker-assets-withdraw-application)
            - [5.2.26.1. Parameters](#52261-parameters)
            - [5.2.26.2. Responses](#52262-responses)
            - [5.2.26.3. Consumes](#52263-consumes)
            - [5.2.26.4. Produces](#52264-produces)
            - [5.2.26.5. Tags](#52265-tags)
        - [5.2.27. Broker Withdraw Records](#5227-broker-withdraw-records)
            - [5.2.27.1. Parameters](#52271-parameters)
            - [5.2.27.2. Responses](#52272-responses)
            - [5.2.27.3. Consumes](#52273-consumes)
            - [5.2.27.4. Produces](#52274-produces)
            - [5.2.27.5. Tags](#52275-tags)
        - [5.2.28. Broker User Coin Withdrawal Application](#5228-broker-user-coin-withdrawal-application)
            - [5.2.28.1. Parameters](#52281-parameters)
            - [5.2.28.2. Responses](#52282-responses)
            - [5.2.28.3. Consumes](#52283-consumes)
            - [5.2.28.4. Produces](#52284-produces)
            - [5.2.28.5. Tags](#52285-tags)
        - [5.2.29. Withdrawal Callback](#5229-withdrawal-callback)
            - [5.2.29.1. Parameters](#52291-parameters)
            - [5.2.29.2. Responses](#52292-responses)
            - [5.2.29.3. Consumes](#52293-consumes)
            - [5.2.29.4. Produces](#52294-produces)
    - [5.3. Definitions](#53-definitions)
        - [5.3.1. ApiResponse«BrokerPageModel«BrokerAssetDto»»](#531-apiresponse«brokerpagemodel«brokerassetdto»»)
        - [5.3.2. ApiResponse«BrokerSymbolFeeData»](#532-apiresponse«brokersymbolfeedata»)
        - [5.3.3. ApiResponse«KlineQueryPages»](#533-apiresponse«klinequerypages»)
        - [5.3.4. ApiResponse«List«AssetDto»»](#534-apiresponse«list«assetdto»»)
        - [5.3.5. ApiResponse«List«BrokerConfigAssetDto»»](#535-apiresponse«list«brokerconfigassetdto»»)
        - [5.3.6. ApiResponse«List«BrokerSymbolFeeData»»](#536-apiresponse«list«brokersymbolfeedata»»)
        - [5.3.7. ApiResponse«List«SymbolData»»](#537-apiresponse«list«symboldata»»)
        - [5.3.8. ApiResponse«List«TransferInAddressDto»»](#538-apiresponse«list«transferinaddressdto»»)
        - [5.3.9. ApiResponse«Map«string,bigdecimal»»](#539-apiresponse«map«stringbigdecimal»»)
        - [5.3.10. ApiResponse«Map«string,int»»](#5310-apiresponse«map«stringint»»)
        - [5.3.11. ApiResponse«PageInfo«MatchOrderDetail»»](#5311-apiresponse«pageinfo«matchorderdetail»»)
        - [5.3.12. ApiResponse«PageInfo«MatchRecordDto»»](#5312-apiresponse«pageinfo«matchrecorddto»»)
        - [5.3.13. ApiResponse«PageModel«DepositDetailDto»»](#5313-apiresponse«pagemodel«depositdetaildto»»)
        - [5.3.14. ApiResponse«PageModel«SettleRecordDto»»](#5314-apiresponse«pagemodel«settlerecorddto»»)
        - [5.3.15. ApiResponse«PageModel«TradeOrderDto»»](#5315-apiresponse«pagemodel«tradeorderdto»»)
        - [5.3.16. ApiResponse«PageModel«WithdrawCoinDetailDto»»](#5316-apiresponse«pagemodel«withdrawcoindetaildto»»)
        - [5.3.17. ApiResponse«SymbolSharingData»](#5317-apiresponse«symbolsharingdata»)
        - [5.3.18. ApiResponse«UserData»](#5318-apiresponse«userdata»)
        - [5.3.19. ApiResponse«Void»](#5319-apiresponse«void»)
        - [5.3.20. ApiResponse«bigdecimal»](#5320-apiresponse«bigdecimal»)
        - [5.3.21. AssetDto](#5321-assetdto)
        - [5.3.22. AssetRequest](#5322-assetrequest)
        - [5.3.23. BrokerAssetAccountRequest](#5323-brokerassetaccountrequest)
        - [5.3.24. BrokerAssetDto](#5324-brokerassetdto)
        - [5.3.25. BrokerAssetRequest](#5325-brokerassetrequest)
        - [5.3.26. BrokerConfigAssetDto](#5326-brokerconfigassetdto)
        - [5.3.27. BrokerPageModel«BrokerAssetDto»](#5327-brokerpagemodel«brokerassetdto»)
        - [5.3.28. BrokerSymbolFeeData](#5328-brokersymbolfeedata)
        - [5.3.29. BrokerWithdrawRequest](#5329-brokerwithdrawrequest)
        - [5.3.30. CancelOrderReq](#5330-cancelorderreq)
        - [5.3.31. CreateUserReq](#5331-createuserreq)
        - [5.3.32. DepositDetailDto](#5332-depositdetaildto)
        - [5.3.33. DepositQueryRequest](#5333-depositqueryrequest)
        - [5.3.34. KlineQueryPages](#5334-klinequerypages)
        - [5.3.35. KlineQueryReq](#5335-klinequeryreq)
        - [5.3.36. KlineRecord](#5336-klinerecord)
        - [5.3.37. Map«string,bigdecimal»](#5337-map«stringbigdecimal»)
        - [5.3.38. Map«string,int»](#5338-map«stringint»)
        - [5.3.39. MatchOrderDetail](#5339-matchorderdetail)
        - [5.3.40. MatchOrderPageQueryReq](#5340-matchorderpagequeryreq)
        - [5.3.41. MatchOrderReq](#5341-matchorderreq)
        - [5.3.42. MatchRecordDto](#5342-matchrecorddto)
        - [5.3.43. MatchRecordPageQueryReq](#5343-matchrecordpagequeryreq)
        - [5.3.44. ModifyWhitelistReq](#5344-modifywhitelistreq)
        - [5.3.45. PageInfo«MatchOrderDetail»](#5345-pageinfo«matchorderdetail»)
        - [5.3.46. PageInfo«MatchRecordDto»](#5346-pageinfo«matchrecorddto»)
        - [5.3.47. PageModel«DepositDetailDto»](#5347-pagemodel«depositdetaildto»)
        - [5.3.48. PageModel«SettleRecordDto»](#5348-pagemodel«settlerecorddto»)
        - [5.3.49. PageModel«TradeOrderDto»](#5349-pagemodel«tradeorderdto»)
        - [5.3.50. PageModel«WithdrawCoinDetailDto»](#5350-pagemodel«withdrawcoindetaildto»)
        - [5.3.51. PageRequest](#5351-pagerequest)
        - [5.3.52. Pages«KlineRecord»](#5352-pages«klinerecord»)
        - [5.3.53. QueryOrderReq](#5353-queryorderreq)
        - [5.3.54. SettleQueryRequest](#5354-settlequeryrequest)
        - [5.3.55. SettleRecordDto](#5355-settlerecorddto)
        - [5.3.56. Symbol](#5356-symbol)
        - [5.3.57. SymbolData](#5357-symboldata)
        - [5.3.58. SymbolFeeAddReq](#5358-symbolfeeaddreq)
        - [5.3.59. SymbolFeeListQueryReq](#5359-symbolfeelistqueryreq)
        - [5.3.60. SymbolFeeQueryReq](#5360-symbolfeequeryreq)
        - [5.3.61. SymbolQueryReq](#5361-symbolqueryreq)
        - [5.3.62. SymbolSharingData](#5362-symbolsharingdata)
        - [5.3.63. TradeOrderDto](#5363-tradeorderdto)
        - [5.3.64. TradeOrderQueryRequest](#5364-tradeorderqueryrequest)
        - [5.3.65. TransferInAddressDto](#5365-transferinaddressdto)
        - [5.3.66. UnVerifiedCountRequest](#5366-unverifiedcountrequest)
        - [5.3.67. UserData](#5367-userdata)
        - [5.3.68. WithdrawCoinDetailDto](#5368-withdrawcoindetaildto)
        - [5.3.69. WithdrawCoinRequest](#5369-withdrawcoinrequest)
        - [5.3.70. WithdrawConfirmRequest](#5370-withdrawconfirmrequest)
        - [5.3.71. WithdrawQueryRequest](#5371-withdrawqueryrequest)
        - [5.3.72. WithdrawTotalAmountRequest](#5372-withdrawtotalamountrequest)
        - [5.3.73. DepositApiResponseDto](#5373-depositapiresponsedto)
        - [5.3.74. DepositResponseData](#5374-depositresponsedata)
        - [5.3.75. WithdrawApiResponseDto](#5375-withdrawapiresponsedto)
        - [5.3.76. WithdrawResponseData](#5376-withdrawresponsedata)

<!-- /TOC -->

As a service provider, MasterDAX provides all brokers’ exchanges such services as exchange ordering and matching, user assets and cash withdrawal. Moreover, as the broker of exchanges, we will credit the gains of your handling fees into your account on T+0 day, and the assets can be withdrawaled at any time. 
# 1. Introduction
As the cloud service provider for exchanges, MasterDAX provides brokers and their users the following services:

| Role | Service Provided | Remarks |
| :---- | :----- | :----- |
| Broker user |Main functions such as user deposit, Token Trading, withdrawal, etc. | |
| Broker | The user's Token Trading fee and the withdrawal fee are settled to the broker's account on T+0 day.   | |


## 1.1. Access Preparation
After having signed a contract with MasterDAX, you will have a unique `broker ID`, brokerId, and a corresponding `accessKey`, `sercretKey`, for signature verification. Please provide the following information before access:
</br>

-  Callback address</br>
-  Bond IP, supporting up to 5 IPs

## 1.2. Instructions for Trade Process
### 1.2.1. Broker’s User Trade Process
After accessing the interface provided by the documentation, the user can order,cancel order and operate others at the exchange. The specific process is as follows:

![云交易所接入流程](user_flow.png)

![用户提现](User_Withdrawal.png)

### 1.2.2. Broker Settlement Process
Once the broker’s user generates fees (trade fee and withdrawal fee) on the exchange, MasterDAX will settle the broker's fee income to the broker's account opened in MasterDAX on `T+0` days as agreed. The broker may initiate any transfer the fee income to its own address via API at its discretion. The specific process is as follows: 

![运营商提现](Broker_Withdrawal.png)

## 1.3. Request Interaction
### 1.3.1. URI scheme
*Host* : https://api.masterdax.com

### 1.3.2. Instructions to Request Interaction
1. Submittal
    
    Convert the encapsulated request parameters to `JSON format`, and submit them to the server via POST method. 

2. Server response

    The server firstly performs parameter security verification on the user request data, and after being verified, the response data will be responded to the client in `JSON format` according to the business logic.

<a name="signature"></a>

### 1.3.3. Signature Method

1. Splicing `Body` data with the `secretKey` without any characters added
2. Sha256 encryption; convert to HEX uppercase strings

```
private String generateSign(String json, String secretKey) {
    String payload = json + secretKey;
    log.debug("payload：" + payload);
    return DigestUtils.sha256Hex(payload).toUpperCase();
}
```

# 2. Standard Interface for the Exchange
## 2.1. Configure Coins and symbols
> Please check the trade coins and symbols supported by the exchange before access. MasterDAX trade services are only available for the supported coins and symbols.  In case of any doubt, please contact the business professionals.

### 2.1.1. Broker Coin List
Query all the coins supported by the exchanges

> Request method：POST</br>
> Interface name：[/v1/coin/broker-configAsset-list](#brokerassetlistusingpost)

### 2.1.2. Broker symbol List
Query all the symbols supported by the exchanges
> Request method：POST</br>
> Interface name：[/v1/symbol/symbols/coin](#getsymbolsbycoinusingpost)

### 2.1.3. Input Broker’s symbols and Handling Fees
The symbols of the broker's exchange, like `EOS/BTC`, needs to be input into MasterDAX before obtaining such data as depth and K-line.</br>
**Note**：The fees is maintained by the broker. MasterDAX will calculate the user’s fee based on this field when the trade is matched.
> Request method：POST</br>
> Interface name：[/v1/symbol/save-update-fee](#addfeeusingpost)


### 2.1.4. Query Broker’s Input symbols Fee
#### 2.1.4.1. Single symbol query
> Request method：POST</br>
> Interface name：[/v1/symbol/get-fee](#getfeeusingpost)


#### 2.1.4.2. All symbols list query

> Request method：POST</br>
> Interface name：[/v1/symbol/get-fees](#getfeeusingpost_1)


## 2.2. User Assets
### 2.2.1. Create a User
After the broker's user completing the registration, the user's `uid` needs to be synchronized to MasterDAX, so that the user can complete subsequent deposit, trade and other operations.
> Request method：POST</br>
> Interface name： [/v1/user/create-user](#createuserusingpost)

### 2.2.2. Modify Whitelist Users
The broker can set a whitelist for a specific user, and the whitelist user’s trade fee is 0.

> Request method：POST</br>
> Interface name： [/v1/user/modify-whitelist](#modifywhitelistusingpost)


### 2.2.3. User Assets Query
Supports querying all of the user's assets, including available balances and frozen balances.

> Request method：POST</br>
> Interface name： [/v1/asset/accounts](#getuseraccountassetsusingpost)


## 2.3. User Deposit
### 2.3.1. Get User Deposit Address
When the user clicking on the deposit, an interface can be called to obtain the deposit address. If the user didn’t have any deposit address system before, the system will automatically assign one for him. 

> Request method：POST</br>
> Interface name： [/v1/coin-transfer/in-address-query](#getcointransferinaddressusingpost)


### 2.3.2. User Deposit Callback
After the user deposits his account, the callback address provided by the broker is called back to the broker for notifying that the account is deposited. 

> Request method：POST</br>
> Interface name： [DepositCallBack](#depositCallBack)


### 2.3.3. Deposit Record Query
Support for querying  deposit records of single user and all users.

> Request method：POST</br>
> Interface name： [/v1/deposit/deposit-coin-details](#getdepositcoinusingpost)

    
## 2.4. Exchange
### 2.4.1. Market Depth Query
Support for querying all depth data of MasterDAX.

> Request method：GET</br>
> Interface name： [/trade/trade?symbol=symbolCode](#getdepthendpoint)


### 2.4.2. Get K-line
Support for querying all K-line of MasterDAX.

> Request method：POST</br>Symbol
> Interface name： [/v1/data/kline/kline-pages](#getklinepagesusingpost)


### 2.4.3. GET Historical trades
Supports for querying the historical trade records of MasterDAX by symbol

> Request method：POST</br>
> Interface name： [/trade/info?symbol=BTC_EOS](#gettradedendpoint)

### 2.4.4. 24H Data Query
Support the latest trade price of a certain symbol, 24H up and down, 24H highest price, 24H lowest price, 24H volume and other data.

> Request method：GET</br>
> Interface name： [/trade/detail](#gettradedetail)


### 2.4.5. User Trade Ordering
The user's order on a certain symbol is sent to MasterDAX for processing.

> Request method：POST</br>
> Interface name： [/v1/match/order](#matchorderusingpost)


### 2.4.6. User Order Cancellation
The user's order cancellation on a certain symbol is sent to MasterDAX for processing.

> Request method：POST</br>
> Interface name： [/v1/match/match-order/cancel](#cancelmatchorderusingpost)


### 2.4.7. User Order Status Query
According to the order number, the information such as the status of the order of the user in a certain symbol is queried.

> Request method：POST</br>
> Interface name：  [/v1/match/order-query](#orderqueryusingpost)


### 2.4.8. User In-progress Order List Query
Query the user's order list for a symbol order with a status of `waiting` and `pending`.

> Request method：POST</br>
> Interface name： [/v1/match/match-order/current](#getmatchorderdetailusingpost)

### 2.4.9. User Processed Order Query
Query the user's order list for a certain symbol order with a status of `success` and `cancel`.

> Request method：POST</br>
> Interface name：  [/v1/match/match-order/history](#gethistorymatchorderusingpost)


### 2.4.10. Query all User's trade Records
Query the trade orders list for all users on a symbol order.

> Request method：POST</br>
> Interface name：  [/v1/trade/userTradeRecord](#getusertraderecordusingpost)


## 2.5. User Withdrawal
### 2.5.1. Broker User Coin Withdrawal Application
This interface is called when the user initiates the withdrawal operation to deduct its corresponding assets.

> Request method：POST</br>
> Interface name：  [/v1/withdraw/withdraw-coin-user](#userwithdrawcoinusingpost)


### 2.5.2. Query User’s Amount to be Withdrawn
When the user initiates the withdrawal operation, This interface is called to query the current balance that can be withdrawn.

> Request method：POST</br>
> Interface name：  [/v1/withdraw/query-balance](#querybalanceusingpost)


### 2.5.3. Query Withdrawals Unverified 
If the user-initiated withdrawal request needs to be reviewed in the broker's control center, the interface can be queried to obtain the unverified amount of the withdrawal request for a certain coin.

> Request method：POST</br>
> Interface name：  [/v1/withdraw/unverifiedCount](#queryunverifiedcountusingpost)


### 2.5.4. User Withdrawal Confirmation
If the user-initiated withdrawal request needs to be reviewed in the broker's control center, this interface can be queried. Once review status sent is `PASS`, Withdrawal will be triggered and callbacked to the broker, if the review status sent is `REFUSE`, the system will refund the coins deducted to the user’s assets.

> Request method：POST</br>
> Interface name：  [/v1/withdraw/confirm](#confirmusingpost)


### 2.5.5. Query User’s Total Amount Withdrawn
The total withdrawal amount that the user initiates.

> Request method：POST</br>
> Interface name：  [/v1/withdraw/queryWithdrawTotal](#querywithdrawtotalusingpost)


### 2.5.6. Query User’s Withdrawal Records
Query the user-initiated withdrawal record, which can be queried by `UID` and `Status`. Display all user withdrawal records when `UID` is `NULL`.
 

> Request method：POST</br>
> Interface name：[/v1/withdraw/withdraw-coin-details](#getwithdrawcoinusingpost)

### 2.5.7. User Withdrawal Callback
After the user withdraws the account or withdraws the trigger limit, the audit failure callback notifies the broker.

> Request method：POST</br>
> Interface name： [WithdrawCallBack](#withdrawCallBack)


# 3. Broker Settlement API
The fee generated by the user trades will be settled to the broker in real time on `T+0` day. The broker can query and settle in the settlement account.

## 3.1. Settlement Account Asset Query
Query the total assets of the broker's settlement account, and the fee generated by the user trades and withdrawal fee will enter into the settlement account.
 

> Request method：POST</br>
> Interface name：  [/v1/coin/brokerAsset-query](#querybrokerfinanceusingpost)


## 3.2. Settlement Account Asset Withdraw Application
The assets in the settlement account can be transferred to the broker's own address.
 

> Request method：POST</br>
> Interface name：  [/v1/withdraw/withdraw-coin-broker](#brokerwithdrawcoinusingpost)


## 3.3. Settlement Account Asset Withdraw Status Callback
After the successful application of transfer out of the settlement account, the system will callback the withdraw status to the broker, and the status includes `REFUSE` and `RECEIVED`.

> Request method：POST</br>
> Interface name： [Callback address provided by the insurer](#withdrawCallBack)



## 3.4. Settlement Account Asset Withdraw  Record Query
Query the assets withdraw records of the settlement account. When `UID=0`, means the broker's withdraw records.
 

> Request method：POST</br>
> Interface name：  [/v1/withdraw/withdraw-coin-details](#getwithdrawcoinusingpost)


## 3.5. symbol Sharing Ratio Query
Query the fee generated by the user trades and symbol sharing ratio of MasterDAX.
 

> Request method：POST</br>
> Interface name：  [/v1/symbol/sharings](#getsharingusingpost)


## 3.6. Settlement Record Query
Query the fee settlement records generated by user trades and withdrawals.
 

> Request method：POST</br>
> Interface name：  [/v1/settle/settle-record](#querysettlerecordusingpost)


# 4. Error Code

|code|msg|
|---|---|
|**SUCCESS**|Success|//Success
|**FAIL**|Success|//成功
|**PARAM_ERROR**|Parameter error|  //参数错误
|**SIGN_ERROR**|Signature error|
|**DUPLICATE_DATA**|Signature error|
|**EMPTY_RECORD**|Empty record|
|**TOO_MANY_RECORDS**|Too many records|
|**REPEAT_MESSAGE**|Repeated message|  //重复的消息
|**USER_NOT_EXIST**|User not exist|
|**BROKER_ASSET_NOT_EXIST**|Broker assets not exist|
|**BROKER_ASSET_EXIST**|Broker asset exist|
|**SYMBOL_FORMAT_ERROR**|Symbol format error|
|**INVALID_SYMBOL**|Invalid symbol|
|**ORDER_CREATE_ERROR**|Invalid symbol|
|**ORDER_NOT_EXIST**|Order not exist|
|**ORDER_STATE_ERROR**|Order status error|
|**ORDER_HAD_CANCELLED**|Order cancelled|
|**ORDER_HAD_PROCESSING**|Order processing|
|**ORDER_HAD_TRADED**|Order has been traded|
|**NO_PERMISSION**|No permission|  //没有权限
|**BROKER_NOT_EXIST**|Broker not exist|
|**ADDRESS_ASSIGN_ERROR**|Address assign error|
|**MESSAGE_TO_MQ_FAIL**|Message to MQ failed|
|**ADDRESS_STATUS_ERROR**|Address status error|
|**ACCOUNT_STATUS_ERROR**|Account status error|
|**WITHDRAW_FEE_TOO_LOW**|Withdrawal fee is lower than fee|
|**WITHDRAW_TOO_LOW**|Withdrawal amount is less than fee|
|**COIN_ASSERT_LESS**|Coin asset is not enough|
|**COIN_LOCK_ASSERT_LESS**|Locked asset is not enough|
|**ADDRESS_DELETE_ERROR**|Address deletion error|
|**WITHDRAW_ORDER_STAUTS_ERROR**|Withdrawal order status error|
|**WITHDRAW_ORDER_STAUTS_UPDATE_ERROR**|Withdrawal order status update error|
|**DEPOSIT_ORDER_STAUTS_ERROR**|Deposit order status error|
|**DEPOSIT_ORDER_NOT_EXIST**|Deposit order not exist|
|**COIN_DEPOSIT_ADDRESS_INVALID**|Coin deposit address invalid|
|**DEPOSIT_ORDER_INSERT_ERROR**|Deposit order insert error|
|**DEPOSIT_ORDER_STAUTS_UPDATE_ERROR**|Deposit order status update error|
|**USER_TOTAL_LIMIT**|User number limit|
|**WITHDRAW_ASSETCODE_NOT_SUPPORT**|Withdrawal coin symbol not supported|
|**UPDATE_FINANCE_ERROR**|Asset update error|
|**BATCH_INSERT_FINANCEDETAIL_ERROR**|Asset batch update error|

# 5. Appendix

<a name="paths"></a>
## 5.1. PUBLIC

<a name="getdepthendpoint"></a>
### 5.1.1. Depth
```
GET `/trade/trade?symbol=`symbolCode
```

#### 5.1.1.1. Parameters

|Parameter name|   Parameter type|   Required| Description|
| :-----    | :-----   | :-----    | :-----   |
|symbolCode|String|Yes|Symbol (filled into the URL path)|


#### 5.1.1.2. Responses example

```
{
    "sell": [
        [
            0.00002736, 
            1071.36299794
        ], 
        [
            0.00002738, 
            0.19978522
        ], 
        [
            0.00002742, 
            75.9087355
        ]
    ], 
    "buy": [
        [
            0.00002618, 
            16.33033728
        ], 
        [
            0.00002611, 
            605.26813127
        ], 
        [
            0.0000261, 
            499.81630013
        ]
    ]
}
```

<a name="gettradedetail"></a>
### 5.1.2. HOURS
```
GET /trade/detail
```
   
#### 5.1.2.1. Responses example

```
{
  "BTC_TRX": {
    "24high": "",
    "24low": "",
    "24Total": "",
    "24Price": ""
  },
  "BTC_KCASH": {
    "24high": "",
    "24low": "",
    "24Total": "",
    "24Price": ""
  },
  "BTC_STORJ": {
    "24high": "0.00006868000000000000",
    "24low": "0.00006615000000000000",
    "24Total": "7046.20000000000000000000",
    "newPrice": 6.807e-05,
    "24Price": "0.00006766000000000000"
  }
}
```

<a name="gettradedendpoint"></a>
### 5.1.3. TRADED ORDER
```
GET /trade/info?symbol=BTC_EOS
```

#### 5.1.3.1. Parameters

|Parameter name|   Parameter type|   Required| Description|
| :-----    | :-----   | :-----    | :-----   |
|symbol|String|Yes|Symbol (filled into the URL path)
|

#### 5.1.3.2. Responses example

```
{
    "24high": "0.00129310000000000000", 
    "24low": "0.00087410000000000000", 
    "24Total": "95162.53042596000000000000", 
    "order": [
        {
            "time": "1523503566", 
            "type": "SELL", 
            "num": 9.15, 
            "price": 0.0012772
        }, 
        {
            "time": "1523503506", 
            "type": "BUY", 
            "num": 2.3165, 
            "price": 0.00128
        }
    ], 
    "24Price": "0.00087520000000000000"
}
```

<a name="paths"></a>
## 5.2. PRIVATE

<a name="getuseraccountassetsusingpost"></a>
### 5.2.1. User asset query (based on the symbol that the broker supports and assigns to user symbol list)
```
POST /v1/asset/accounts
```


#### 5.2.1.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**request**  <br>*required*|request|[BrokerAssetAccountRequest](#brokerassetaccountrequest)|


#### 5.2.1.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«List«AssetDto»»](#d26b592b71e05154ee6b33c6f7a261cc)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.1.3. Consumes

* `application/json`


#### 5.2.1.4. Produces

* `\*/*`


#### 5.2.1.5. Tags

* user-asset-controller


<a name="getcointransferinaddressusingpost"></a>
### 5.2.2. Get User deposit Address
```
POST /v1/coin-transfer/in-address-query
```


#### 5.2.2.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**assetRequest**  <br>*required*|assetRequest|[AssetRequest](#assetrequest)|


#### 5.2.2.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«List«TransferInAddressDto»»](#ed7ed4b8e03e4b9a2ee44094fecf6ffd)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.2.3. Consumes

* `application/json`


#### 5.2.2.4. Produces

* `\*/*`


#### 5.2.2.5. Tags

* coin-address-man-controller

<a name="depositCallBack"></a>
### 5.2.3. Deposit Callback

#### 5.2.3.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**DepositApiResponseDto**  <br>*required*|DepositApiResponseDto|[DepositApiResponseDto](#DepositApiResponseDto)|


#### 5.2.3.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|

#### 5.2.3.3. Consumes

* `application/json`


#### 5.2.3.4. Produces

* `\*/*`


#### 5.2.3.5. Tags

<a name="brokerassetlistusingpost"></a>
### 5.2.4. Broker Coin List Query (including Withdrawal Fee)
```
POST /v1/coin/broker-configAsset-list
```


#### 5.2.4.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**request**  <br>*required*|request|[BrokerAssetRequest](#brokerassetrequest)|


#### 5.2.4.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«List«BrokerConfigAssetDto»»](#29d3eb9515674d5e992cf7c3fcea8a5b)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.4.3. Consumes

* `application/json`


#### 5.2.4.4. Produces

* `\*/*`


#### 5.2.4.5. Tags

* asset-manager-controller


<a name="querybrokerfinanceusingpost"></a>
### 5.2.5. Broker Settlement Account Asset Query
```
POST /v1/coin/brokerAsset-query
```


#### 5.2.5.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**request**  <br>*required*|request|[PageRequest](#pagerequest)|


#### 5.2.5.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«BrokerPageModel«BrokerAssetDto»»](#3129640bc337647a01d923c78ac55f72)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.5.3. Consumes

* `application/json`


#### 5.2.5.4. Produces

* `\*/*`


#### 5.2.5.5. Tags

* asset-manager-controller


<a name="getklinepagesusingpost"></a>
### 5.2.6. Get K-line (Paged Query)
```
POST /v1/data/kline/kline-pages
```


#### 5.2.6.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**req**  <br>*required*|req|[KlineQueryReq](#klinequeryreq)|


#### 5.2.6.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«KlineQueryPages»](#8710d779824389ca515611e3c22f2f66)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.6.3. Consumes

* `application/json`


#### 5.2.6.4. Produces

* `\*/*`


#### 5.2.6.5. Tags

* kline-query-controller


<a name="getdepositcoinusingpost"></a>
### 5.2.7. Broker User Deposit Record Query
```
POST /v1/deposit/deposit-coin-details
```


#### 5.2.7.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**request**  <br>*required*|request|[DepositQueryRequest](#depositqueryrequest)|


#### 5.2.7.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«PageModel«DepositDetailDto»»](#82c577a03b8be584493954e6197f9b45)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.7.3. Consumes

* `application/json`


#### 5.2.7.4. Produces

* `\*/*`


#### 5.2.7.5. Tags

* deposit-coin-controller


<a name="cancelmatchorderusingpost"></a>
### 5.2.8. User Order Cancellation
```
POST /v1/match/match-order/cancel
```


#### 5.2.8.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**req**  <br>*required*|req|[CancelOrderReq](#cancelorderreq)|


#### 5.2.8.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«Void»](#196cc3be9a21471c8e871b4fb9019cae)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.8.3. Consumes

* `application/json`


#### 5.2.8.4. Produces

* `\*/*`


#### 5.2.8.5. Tags

* match-order-controller


<a name="getmatchorderdetailusingpost"></a>
### 5.2.9. User in-progress Order List Query
```
POST /v1/match/match-order/current
```


#### 5.2.9.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**req**  <br>*required*|req|[MatchOrderPageQueryReq](#matchorderpagequeryreq)|


#### 5.2.9.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«PageInfo«MatchOrderDetail»»](#af561c25b8a6a1a5325d4e5de5fcefa2)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.9.3. Consumes

* `application/json`


#### 5.2.9.4. Produces

* `\*/*`


#### 5.2.9.5. Tags

* match-order-controller


<a name="gethistorymatchorderusingpost"></a>
### 5.2.10. User Processed Order Status Query
```
POST /v1/match/match-order/history
```


#### 5.2.10.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**req**  <br>*required*|req|[MatchOrderPageQueryReq](#matchorderpagequeryreq)|


#### 5.2.10.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«PageInfo«MatchOrderDetail»»](#af561c25b8a6a1a5325d4e5de5fcefa2)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.10.3. Consumes

* `application/json`


#### 5.2.10.4. Produces

* `\*/*`


#### 5.2.10.5. Tags

* match-order-controller



<a name="matchorderusingpost"></a>
### 5.2.11. User Trade Ordering
```
POST /v1/match/order
```


#### 5.2.11.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**req**  <br>*required*|req|[MatchOrderReq](#matchorderreq)|


#### 5.2.11.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«Void»](#196cc3be9a21471c8e871b4fb9019cae)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.11.3. Consumes

* `application/json`


#### 5.2.11.4. Produces

* `\*/*`


#### 5.2.11.5. Tags

* match-order-controller


<a name="orderqueryusingpost"></a>
### 5.2.12. User Single Order Status Query
```
POST /v1/match/order-query
```


#### 5.2.12.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**req**  <br>*required*|req|[QueryOrderReq](#queryorderreq)|


#### 5.2.12.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[MatchOrderDetail](#matchorderdetail)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.12.3. Consumes

* `application/json`


#### 5.2.12.4. Produces

* `\*/*`


#### 5.2.12.5. Tags

* match-order-controller


<a name="querysettlerecordusingpost"></a>
### 5.2.13. Broker Settlement Record Query
```
POST /v1/settle/settle-record
```


#### 5.2.13.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**request**  <br>*required*|request|[SettleQueryRequest](#settlequeryrequest)|


#### 5.2.13.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«PageModel«SettleRecordDto»»](#29fbac2cdffd95d8715e7846d92debdd)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.13.3. Consumes

* `application/json`


#### 5.2.13.4. Produces

* `\*/*`


#### 5.2.13.5. Tags

* settle-manager-controller


<a name="getfeeusingpost"></a>

### 5.2.14. Single symbol Query
```
POST /v1/symbol/get-fee
```


#### 5.2.14.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**req**  <br>*required*|req|[SymbolFeeQueryReq](#symbolfeequeryreq)|


#### 5.2.14.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«BrokerSymbolFeeData»](#b51c21747b9194b617a696eca5e3e0b7)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.14.3. Consumes

* `application/json`


#### 5.2.14.4. Produces

* `\*/*`


#### 5.2.14.5. Tags

* symbol-controller


<a name="getfeeusingpost_1"></a>

### 5.2.15. Query all symbols List
```
POST /v1/symbol/get-fees
```


#### 5.2.15.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**req**  <br>*required*|req|[SymbolFeeListQueryReq](#symbolfeelistqueryreq)|


#### 5.2.15.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«List«BrokerSymbolFeeData»»](#eaeff6f989d4756651fba9d76ad90043)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.15.3. Consumes

* `application/json`


#### 5.2.15.4. Produces

* `\*/*`


#### 5.2.15.5. Tags

* symbol-controller


<a name="addfeeusingpost"></a>
### 5.2.16. Input Coil Pairs and Fees
```
POST /v1/symbol/save-update-fee
```


#### 5.2.16.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**req**  <br>*required*|req|[SymbolFeeAddReq](#symbolfeeaddreq)|


#### 5.2.16.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«BrokerSymbolFeeData»](#b51c21747b9194b617a696eca5e3e0b7)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.16.3. Consumes

* `application/json`


#### 5.2.16.4. Produces

* `\*/*`


#### 5.2.16.5. Tags

* symbol-controller


<a name="getsharingusingpost"></a>
### 5.2.17. Symbol Sharing Ratio Query
```
POST /v1/symbol/sharings
```


#### 5.2.17.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Query**|**nanoTime**  <br>*required*|Current Timestamp (nanoseconds)|integer (int64)|


#### 5.2.17.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«SymbolSharingData»](#ceae0169df711b82935661c7d4227567)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.17.3. Consumes

* `application/json`


#### 5.2.17.4. Produces

* `\*/*`


#### 5.2.17.5. Tags

* symbol-controller


<a name="getsymbolsbycoinusingpost"></a>
### 5.2.18. Symbol List Query by Coins
```
POST /v1/symbol/symbols/coin
```


#### 5.2.18.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**req**  <br>*required*|req|[SymbolQueryReq](#symbolqueryreq)|


#### 5.2.18.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«List«SymbolData»»](#b01ba55e3561c1ba9febd8ca5bc3539b)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.18.3. Consumes

* `application/json`


#### 5.2.18.4. Produces

* `\*/*`


#### 5.2.18.5. Tags

* symbol-controller


<a name="getusertraderecordusingpost"></a>
### 5.2.19. Broker User Trade Record Query
```
POST /v1/trade/userTradeRecord
```


#### 5.2.19.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**request**  <br>*required*|request|[TradeOrderQueryRequest](#tradeorderqueryrequest)|


#### 5.2.19.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«PageModel«TradeOrderDto»»](#fb7634128e52b8535dc169001707afec)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.19.3. Consumes

* `application/json`


#### 5.2.19.4. Produces

* `\*/*`


#### 5.2.19.5. Tags

* trade-manager-controller


<a name="createuserusingpost"></a>
### 5.2.20. Create User
```
POST /v1/user/create-user
```


#### 5.2.20.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**req**  <br>*required*|req|[CreateUserReq](#createuserreq)|


#### 5.2.20.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«UserData»](#7d001d219a176986c8b2752c3f4d05d3)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.20.3. Consumes

* `application/json`


#### 5.2.20.4. Produces

* `\*/*`


#### 5.2.20.5. Tags

* user-controller




<a name="modifywhitelistusingpost"></a>
### 5.2.21. Modify Whitelist User
```
POST /v1/user/modify-whitelist
```


#### 5.2.21.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**req**  <br>*required*|req|[ModifyWhitelistReq](#modifywhitelistreq)|


#### 5.2.21.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«Void»](#196cc3be9a21471c8e871b4fb9019cae)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.21.3. Consumes

* `application/json`


#### 5.2.21.4. Produces

* `\*/*`


#### 5.2.21.5. Tags

* user-controller


<a name="confirmusingpost"></a>
### 5.2.22. Broker User Coin Withdrawal Confirmation
```
POST /v1/withdraw/confirm
```


#### 5.2.22.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**request**  <br>*required*|request|[WithdrawConfirmRequest](#withdrawconfirmrequest)|


#### 5.2.22.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«Void»](#196cc3be9a21471c8e871b4fb9019cae)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.22.3. Consumes

* `application/json`


#### 5.2.22.4. Produces

* `\*/*`


#### 5.2.22.5. Tags

* withdraw-coin-controller


<a name="querybalanceusingpost"></a>
### 5.2.23. Query Balance to be Withdrawn
```
POST /v1/withdraw/query-balance
```


#### 5.2.23.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**assetRequest**  <br>*required*|assetRequest|[AssetRequest](#assetrequest)|


#### 5.2.23.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«bigdecimal»](#62e4a694d927f3a9133cf1942a9a9102)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.23.3. Consumes

* `application/json`


#### 5.2.23.4. Produces

* `\*/*`


#### 5.2.23.5. Tags

* withdraw-coin-controller


<a name="querywithdrawtotalusingpost"></a>
### 5.2.24. Total Withdrawals
```
POST /v1/withdraw/queryWithdrawTotal
```


#### 5.2.24.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**request**  <br>*required*|request|[WithdrawTotalAmountRequest](#withdrawtotalamountrequest)|


#### 5.2.24.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«Map«string,bigdecimal»»](#71933e463130fcc6486fb5fb5f34c23e)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.24.3. Consumes

* `application/json`


#### 5.2.24.4. Produces

* `\*/*`


#### 5.2.24.5. Tags

* withdraw-coin-controller


<a name="queryunverifiedcountusingpost"></a>
### 5.2.25. Single Coin Withdrawal Unverified

```
POST /v1/withdraw/unverifiedCount
```


#### 5.2.25.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**request**  <br>*required*|request|[UnVerifiedCountRequest](#unverifiedcountrequest)|


#### 5.2.25.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«Map«string,int»»](#3a2cb5618d3fe80bff232572e56c295a)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.25.3. Consumes

* `application/json`


#### 5.2.25.4. Produces

* `\*/*`


#### 5.2.25.5. Tags

* withdraw-coin-controller


<a name="brokerwithdrawcoinusingpost"></a>
### 5.2.26. Broker Assets Withdraw Application
```
POST /v1/withdraw/withdraw-coin-broker
```


#### 5.2.26.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**request**  <br>*required*|request|[BrokerWithdrawRequest](#brokerwithdrawrequest)|


#### 5.2.26.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«Void»](#196cc3be9a21471c8e871b4fb9019cae)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.26.3. Consumes

* `application/json`


#### 5.2.26.4. Produces

* `\*/*`


#### 5.2.26.5. Tags

* withdraw-coin-controller


<a name="getwithdrawcoinusingpost"></a>
### 5.2.27. Broker Withdraw Records
```
POST /v1/withdraw/withdraw-coin-details
```


#### 5.2.27.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**withdrawQueryRequest**  <br>*required*|withdrawQueryRequest|[WithdrawQueryRequest](#withdrawqueryrequest)|


#### 5.2.27.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«PageModel«WithdrawCoinDetailDto»»](#14dace88a1a7adb1791a784b47a8aef9)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.27.3. Consumes

* `application/json`


#### 5.2.27.4. Produces

* `\*/*`


#### 5.2.27.5. Tags

* withdraw-coin-controller


<a name="userwithdrawcoinusingpost"></a>
### 5.2.28. Broker User Coin Withdrawal Application
```
POST /v1/withdraw/withdraw-coin-user
```


#### 5.2.28.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**request**  <br>*required*|request|[WithdrawCoinRequest](#withdrawcoinrequest)|


#### 5.2.28.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|[ApiResponse«Void»](#196cc3be9a21471c8e871b4fb9019cae)|
|**201**|Created|No Content|
|**401**|Unauthorized|No Content|
|**403**|Forbidden|No Content|
|**404**|Not Found|No Content|


#### 5.2.28.3. Consumes

* `application/json`


#### 5.2.28.4. Produces

* `\*/*`


#### 5.2.28.5. Tags

* withdraw-coin-controller

<a name="withdrawCallBack"></a>
### 5.2.29. Withdrawal Callback

#### 5.2.29.1. Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**accessKey**  <br>*required*|Access Key|string|
|**Header**|**sign**  <br>*required*|Signature|string|
|**Body**|**WithdrawApiResponseDto**  <br>*required*|WithdrawApiResponseDto|[WithdrawApiResponseDto](#WithdrawApiResponseDto)|


#### 5.2.29.2. Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|

#### 5.2.29.3. Consumes

* `application/json`


#### 5.2.29.4. Produces

* `\*/*`


<a name="definitions"></a>
## 5.3. Definitions

<a name="3129640bc337647a01d923c78ac55f72"></a>
### 5.3.1. ApiResponse«BrokerPageModel«BrokerAssetDto»»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||[BrokerPageModel«BrokerAssetDto»](#488103a3791c82bc492f8243b6885fb0)|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="b51c21747b9194b617a696eca5e3e0b7"></a>
### 5.3.2. ApiResponse«BrokerSymbolFeeData»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||[BrokerSymbolFeeData](#brokersymbolfeedata)|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="8710d779824389ca515611e3c22f2f66"></a>
### 5.3.3. ApiResponse«KlineQueryPages»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||[KlineQueryPages](#klinequerypages)|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="d26b592b71e05154ee6b33c6f7a261cc"></a>
### 5.3.4. ApiResponse«List«AssetDto»»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||< [AssetDto](#assetdto) > array|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="29d3eb9515674d5e992cf7c3fcea8a5b"></a>
### 5.3.5. ApiResponse«List«BrokerConfigAssetDto»»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||< [BrokerConfigAssetDto](#brokerconfigassetdto) > array|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="eaeff6f989d4756651fba9d76ad90043"></a>
### 5.3.6. ApiResponse«List«BrokerSymbolFeeData»»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||< [BrokerSymbolFeeData](#brokersymbolfeedata) > array|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="b01ba55e3561c1ba9febd8ca5bc3539b"></a>
### 5.3.7. ApiResponse«List«SymbolData»»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||< [SymbolData](#symboldata) > array|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="ed7ed4b8e03e4b9a2ee44094fecf6ffd"></a>
### 5.3.8. ApiResponse«List«TransferInAddressDto»»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||< [TransferInAddressDto](#transferinaddressdto) > array|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="71933e463130fcc6486fb5fb5f34c23e"></a>
### 5.3.9. ApiResponse«Map«string,bigdecimal»»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||< string, number > map|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="3a2cb5618d3fe80bff232572e56c295a"></a>
### 5.3.10. ApiResponse«Map«string,int»»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||< string, integer (int32) > map|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="af561c25b8a6a1a5325d4e5de5fcefa2"></a>
### 5.3.11. ApiResponse«PageInfo«MatchOrderDetail»»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||[PageInfo«MatchOrderDetail»](#25f81bde9effd814e7bcf1ea7d73c4f7)|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="1a5f60cc3d37772c5c069b2403786fbf"></a>
### 5.3.12. ApiResponse«PageInfo«MatchRecordDto»»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||[PageInfo«MatchRecordDto»](#0cb0127a416ce5c26ac2ee156711aacd)|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="82c577a03b8be584493954e6197f9b45"></a>
### 5.3.13. ApiResponse«PageModel«DepositDetailDto»»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||[PageModel«DepositDetailDto»](#922592b0bd84c95143d881659b43f5b7)|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="29fbac2cdffd95d8715e7846d92debdd"></a>
### 5.3.14. ApiResponse«PageModel«SettleRecordDto»»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||[PageModel«SettleRecordDto»](#d8c97f7a9a191de856d9bfd7162c1b88)|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="fb7634128e52b8535dc169001707afec"></a>
### 5.3.15. ApiResponse«PageModel«TradeOrderDto»»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||[PageModel«TradeOrderDto»](#9832eb12068b6b1627b21ae6b1ac060c)|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="14dace88a1a7adb1791a784b47a8aef9"></a>
### 5.3.16. ApiResponse«PageModel«WithdrawCoinDetailDto»»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||[PageModel«WithdrawCoinDetailDto»](#63fc5848d93402e6be9ab0d7419be4ca)|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="ceae0169df711b82935661c7d4227567"></a>
### 5.3.17. ApiResponse«SymbolSharingData»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||[SymbolSharingData](#symbolsharingdata)|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="7d001d219a176986c8b2752c3f4d05d3"></a>
### 5.3.18. ApiResponse«UserData»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||[UserData](#userdata)|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="196cc3be9a21471c8e871b4fb9019cae"></a>
### 5.3.19. ApiResponse«Void»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="62e4a694d927f3a9133cf1942a9a9102"></a>
### 5.3.20. ApiResponse«bigdecimal»

|Name|Description|Schema|
|---|---|---|
|**code**  <br>*required*|Response Code|string|
|**data**  <br>*optional*||number|
|**msg**  <br>*required*|Response Message|string|
|**ret**  <br>*required*|Response success  <br>**Example** : `false`|boolean|


<a name="assetdto"></a>
### 5.3.21. AssetDto

|Name|Schema|
|---|---|
|**accountNo**  <br>*optional*|string|
|**amountAvailable**  <br>*optional*|number|
|**amountLock**  <br>*optional*|number|
|**assetCode**  <br>*optional*|string|
|**uid**  <br>*optional*|integer (int64)|


<a name="assetrequest"></a>
### 5.3.22. AssetRequest

|Name|Description|Schema|
|---|---|---|
|**assetCode**  <br>*optional*|Coin Type|string|
|**uid**  <br>*optional*|User ID|integer (int64)|


<a name="brokerassetaccountrequest"></a>
### 5.3.23. BrokerAssetAccountRequest

|Name|Description|Schema|
|---|---|---|
|**assetList**  <br>*optional*|List of broker’s Supported Coins|< string > array|
|**uid**  <br>*optional*|User ID|integer (int64)|


<a name="brokerassetdto"></a>
### 5.3.24. BrokerAssetDto

|Name|Schema|
|---|---|
|**amountAvailable**  <br>*optional*|number|
|**amountLock**  <br>*optional*|number|
|**assetCode**  <br>*optional*|string|


<a name="brokerassetrequest"></a>
### 5.3.25. BrokerAssetRequest

|Name|Description|Schema|
|---|---|---|
|**assetCode**  <br>*optional*|Coin Type|string|


<a name="brokerconfigassetdto"></a>
### 5.3.26. BrokerConfigAssetDto

|Name|Schema|
|---|---|
|**assetCode**  <br>*optional*|string|
|**createDate**  <br>*optional*|string (date-time)|
|**name**  <br>*optional*|string|
|**status**  <br>*optional*|enum (INIT, LISTED, DELISTED)|
|**withdrawFee**  <br>*optional*|number|


<a name="488103a3791c82bc492f8243b6885fb0"></a>
### 5.3.27. BrokerPageModel«BrokerAssetDto»

|Name|Schema|
|---|---|
|**assetCount**  <br>*optional*|integer (int64)|
|**brokerName**  <br>*optional*|string|
|**list**  <br>*optional*|< [BrokerAssetDto](#brokerassetdto) > array|
|**pageNo**  <br>*optional*|integer (int32)|
|**pageNum**  <br>*optional*|integer (int32)|
|**pageSize**  <br>*optional*|integer (int32)|
|**total**  <br>*optional*|integer (int64)|


<a name="brokersymbolfeedata"></a>
### 5.3.28. BrokerSymbolFeeData

|Name|Description|Schema|
|---|---|---|
|**brokerId**  <br>*optional*|Broker ID|string|
|**feeMin**  <br>*optional*|Minimum Fee|number|
|**makerFeeRatio**  <br>*optional*|MAKER Fee Ratio|number|
|**method**  <br>*optional*|Fee Type|string|
|**priceAsset**  <br>*optional*|Pricing Asset|string|
|**takerFeeRatio**  <br>*optional*|TAKER Fee Ratio|number|
|**tradeAsset**  <br>*optional*|Trade Asset|string|


<a name="brokerwithdrawrequest"></a>
### 5.3.29. BrokerWithdrawRequest

|Name|Description|Schema|
|---|---|---|
|**address**  <br>*optional*|Withdrawal Address|string|
|**amount**  <br>*optional*|Withdrawal Amount|number|
|**assetCode**  <br>*optional*|Coin Type|string|
|**clientOrderNo**  <br>*optional*|Client Order No.|string|
|**message**  <br>*optional*|Withdrawal Information|string|


<a name="cancelorderreq"></a>
### 5.3.30. CancelOrderReq

|Name|Description|Schema|
|---|---|---|
|**clientOrderNo**  <br>*required*|Broker Order No.|string|
|**nanoTime**  <br>*required*|Current Timestamp (nanoseconds)|integer (int64)|


<a name="createuserreq"></a>
### 5.3.31. CreateUserReq

|Name|Description|Schema|
|---|---|---|
|**birthday**  <br>*optional*|Birthday  <br>**Example** : `"2018-01-01"`|string|
|**brokerUid**  <br>*required*|Broker User ID|integer (int64)|
|**country**  <br>*optional*|Nationality|string|
|**email**  <br>*optional*|Broker User's Email|string|
|**gender**  <br>*optional*|Gender|string|
|**ip**  <br>*optional*|User Registration IP|string|
|**name**  <br>*optional*|User Name|string|
|**nanoTime**  <br>*required*|Current Timestamp (nanoseconds)|integer (int64)|
|**phone**  <br>*optional*|Phone No.|string|


<a name="depositdetaildto"></a>
### 5.3.32. DepositDetailDto

|Name|Schema|
|---|---|
|**account**  <br>*optional*|string|
|**address**  <br>*optional*|string|
|**amount**  <br>*optional*|number|
|**assetCode**  <br>*optional*|string|
|**brokerId**  <br>*optional*|string|
|**createDate**  <br>*optional*|string (date-time)|
|**msg**  <br>*optional*|string|
|**orderNo**  <br>*optional*|string|
|**outOrderNo**  <br>*optional*|string|
|**status**  <br>*optional*|enum (CONFIRM, SUCCESS, FAILURE)|
|**uid**  <br>*optional*|integer (int64)|
|**updateDate**  <br>*optional*|string (date-time)|


<a name="depositqueryrequest"></a>
### 5.3.33. DepositQueryRequest

|Name|Description|Schema|
|---|---|---|
|**address**  <br>*optional*|Wallet Address|string|
|**assetCode**  <br>*optional*|Coin Type|string|
|**endDate**  <br>*optional*|End Date|string (date-time)|
|**pageNo**  <br>*optional*|Pages|integer (int32)|
|**pageSize**  <br>*optional*|Page Size|integer (int32)|
|**startDate**  <br>*optional*|Start Date|string (date-time)|
|**status**  <br>*optional*|Deposit Status: CONFIRM, SUCCESS, FAILURE|enum (CONFIRM, SUCCESS, FAILURE)|
|**uid**  <br>*optional*|User ID|integer (int64)|


<a name="klinequerypages"></a>
### 5.3.34. KlineQueryPages

|Name|Schema|
|---|---|
|**pages**  <br>*optional*|[Pages«KlineRecord»](#349f6b917324f326c7b17859b3a4b408)|


<a name="klinequeryreq"></a>
### 5.3.35. KlineQueryReq

|Name|Description|Schema|
|---|---|---|
|**endTime**  <br>*required*|End Time (seconds)|integer (int64)|
|**kline**  <br>*required*|Type=1m, 5m, 15m, 30m ,1h, 1d|string|
|**nanoTime**  <br>*required*|Current Timestamp (nanoseconds)|integer (int64)|
|**pageNum**  <br>*required*|Pages=1|integer (int32)|
|**pageSize**  <br>*required*|Page Size|integer (int32)|
|**startTime**  <br>*required*|Start Time (seconds)|integer (int64)|
|**symbol**  <br>*required*|Symbol=tradeAsset_priceAsset|string|


<a name="klinerecord"></a>
### 5.3.36. KlineRecord

|Name|Description|Schema|
|---|---|---|
|**amount**  <br>*optional*|Trade Volume|number|
|**close**  <br>*optional*|Closing Price|number|
|**klineType**  <br>*optional*|K-line Type|string|
|**lowPrice**  <br>*optional*|Low Price|number|
|**maxPrice**  <br>*optional*|Max Price|number|
|**open**  <br>*optional*|Starting Price|number|
|**symbol**  <br>*optional*|Symbol|string|
|**time**  <br>*optional*|Time|integer (int64)|


<a name="4211319230c057cdf99d0e4473178bfb"></a>
### 5.3.37. Map«string,bigdecimal»
*Type* : < string, number > map


<a name="d764f4858e39dc9eee78f8c7d66455a6"></a>
### 5.3.38. Map«string,int»
*Type* : < string, [Integer](#integer) > map


<a name="matchorderdetail"></a>
### 5.3.39. MatchOrderDetail

|Name|Description|Schema|
|---|---|---|
|**clientOrderNo**  <br>*optional*|Broker Order No.|string|
|**createTime**  <br>*optional*|Order Creation Time|string (date-time)|
|**fee**  <br>*optional*|Broker User Fee Deduction|number|
|**feeAsset**  <br>*optional*|Fee Asset|string|
|**matchedMoney**  <br>*optional*|Filled Asset|number|
|**money**  <br>*optional*||number|
|**moneyOver**  <br>*optional*||number|
|**number**  <br>*optional*|Order Quantity|number|
|**numberOver**  <br>*optional*|Remaining Quantity|number|
|**orderState**  <br>*optional*|Trade Status|enum (WAITING, PROCESSING, SUCCESS, CANCEL, FAIL)|
|**orderType**  <br>*optional*|Order Types|enum (BUY, SELL)|
|**platformOrderNo**  <br>*optional*|Platform Order No.|string|
|**price**  <br>*optional*|Price|number|
|**priceAssert**  <br>*optional*|Pricing Asset|string|
|**tradeAssert**  <br>*optional*|Trading Asset |string|
|**tradeType**  <br>*optional*|Trade Type|enum (FIXED, MARKET)|
|**tradedNumber**  <br>*optional*|Match Number|number|


<a name="matchorderpagequeryreq"></a>
### 5.3.40. MatchOrderPageQueryReq

|Name|Description|Schema|
|---|---|---|
|**brokerUid**  <br>*required*|Broker User ID|integer (int64)|
|**endTime**  <br>*optional*|End Time  <br>**Example** : `"2018-01-01 23:59:59"`|string (date-time)|
|**nanoTime**  <br>*required*|Current Timestamp (nanoseconds)|integer (int64)|
|**orderType**  <br>*optional*|Order Type|enum (BUY, SELL)|
|**pageNo**  <br>*optional*|Page|integer (int32)|
|**pageSize**  <br>*optional*|Page size|integer (int32)|
|**priceAsset**  <br>*required*|Pricing Asset|string|
|**startTime**  <br>*optional*|Start Time   <br>**Example** : `"2018-01-01 00:00:00"`|string (date-time)|
|**tradeAsset**  <br>*required*|Trading Asset |string|


<a name="matchorderreq"></a>
### 5.3.41. MatchOrderReq

|Name|Description|Schema|
|---|---|---|
|**amount**  <br>*required*|Order Quantity|number|
|**brokerUid**  <br>*required*|Broker User ID|integer (int64)|
|**clientOrderNo**  <br>*required*|Broker Order No.|string|
|**nanoTime**  <br>*required*|Current Timestamp (nanoseconds)|integer (int64)|
|**orderType**  <br>*required*|Order Type|enum (BUY, SELL)|
|**price**  <br>*required*|Price|number|
|**priceAsset**  <br>*required*|Pricing Asset|string|
|**tradeAsset**  <br>*required*|Trading Asset |string|
|**tradeType**  <br>*required*|Trade Type|enum (FIXED, MARKET)|


<a name="matchrecorddto"></a>
### 5.3.42. MatchRecordDto

|Name|Description|Schema|
|---|---|---|
|**createTime**  <br>*optional*|Creation Time|string (date-time)|
|**num**  <br>*optional*|Filled Number|number|
|**price**  <br>*optional*|Price|number|


<a name="matchrecordpagequeryreq"></a>
### 5.3.43. MatchRecordPageQueryReq

|Name|Description|Schema|
|---|---|---|
|**brokerUid**  <br>*required*|Broker User ID|integer (int64)|
|**clientOrderNo**  <br>*required*|Broker Order No.|string|
|**nanoTime**  <br>*required*|Current Timestamp (nanoseconds)|integer (int64)|
|**pageNo**  <br>*optional*|Page|integer (int32)|
|**pageSize**  <br>*optional*|Size per Page|integer (int32)|
|**priceAsset**  <br>*optional*|Pricing Asset|string|
|**tradeAsset**  <br>*optional*|Trading Asset |string|


<a name="modifywhitelistreq"></a>
### 5.3.44. ModifyWhitelistReq

|Name|Description|Schema|
|---|---|---|
|**brokerUid**  <br>*required*|Broker User ID|integer (int64)|
|**nanoTime**  <br>*required*|Current Timestamp (nanoseconds)|integer (int64)|
|**whiteList**  <br>*required*|Whitelist or Not<br>**Example** : `false`|boolean|


<a name="25f81bde9effd814e7bcf1ea7d73c4f7"></a>
### 5.3.45. PageInfo«MatchOrderDetail»

|Name|Schema|
|---|---|
|**endRow**  <br>*optional*|integer (int32)|
|**firstPage**  <br>*optional*|integer (int32)|
|**hasNextPage**  <br>*optional*|boolean|
|**hasPreviousPage**  <br>*optional*|boolean|
|**isFirstPage**  <br>*optional*|boolean|
|**isLastPage**  <br>*optional*|boolean|
|**lastPage**  <br>*optional*|integer (int32)|
|**list**  <br>*optional*|< [MatchOrderDetail](#matchorderdetail) > array|
|**navigateFirstPage**  <br>*optional*|integer (int32)|
|**navigateLastPage**  <br>*optional*|integer (int32)|
|**navigatePages**  <br>*optional*|integer (int32)|
|**navigatepageNums**  <br>*optional*|< integer (int32) > array|
|**nextPage**  <br>*optional*|integer (int32)|
|**pageNum**  <br>*optional*|integer (int32)|
|**pageSize**  <br>*optional*|integer (int32)|
|**pages**  <br>*optional*|integer (int32)|
|**prePage**  <br>*optional*|integer (int32)|
|**size**  <br>*optional*|integer (int32)|
|**startRow**  <br>*optional*|integer (int32)|
|**total**  <br>*optional*|integer (int64)|


<a name="0cb0127a416ce5c26ac2ee156711aacd"></a>
### 5.3.46. PageInfo«MatchRecordDto»

|Name|Schema|
|---|---|
|**endRow**  <br>*optional*|integer (int32)|
|**firstPage**  <br>*optional*|integer (int32)|
|**hasNextPage**  <br>*optional*|boolean|
|**hasPreviousPage**  <br>*optional*|boolean|
|**isFirstPage**  <br>*optional*|boolean|
|**isLastPage**  <br>*optional*|boolean|
|**lastPage**  <br>*optional*|integer (int32)|
|**list**  <br>*optional*|< [MatchRecordDto](#matchrecorddto) > array|
|**navigateFirstPage**  <br>*optional*|integer (int32)|
|**navigateLastPage**  <br>*optional*|integer (int32)|
|**navigatePages**  <br>*optional*|integer (int32)|
|**navigatepageNums**  <br>*optional*|< integer (int32) > array|
|**nextPage**  <br>*optional*|integer (int32)|
|**pageNum**  <br>*optional*|integer (int32)|
|**pageSize**  <br>*optional*|integer (int32)|
|**pages**  <br>*optional*|integer (int32)|
|**prePage**  <br>*optional*|integer (int32)|
|**size**  <br>*optional*|integer (int32)|
|**startRow**  <br>*optional*|integer (int32)|
|**total**  <br>*optional*|integer (int64)|


<a name="922592b0bd84c95143d881659b43f5b7"></a>
### 5.3.47. PageModel«DepositDetailDto»

|Name|Schema|
|---|---|
|**list**  <br>*optional*|< [DepositDetailDto](#depositdetaildto) > array|
|**pageNo**  <br>*optional*|integer (int32)|
|**pageNum**  <br>*optional*|integer (int32)|
|**pageSize**  <br>*optional*|integer (int32)|
|**total**  <br>*optional*|integer (int64)|


<a name="d8c97f7a9a191de856d9bfd7162c1b88"></a>
### 5.3.48. PageModel«SettleRecordDto»

|Name|Schema|
|---|---|
|**list**  <br>*optional*|< [SettleRecordDto](#settlerecorddto) > array|
|**pageNo**  <br>*optional*|integer (int32)|
|**pageNum**  <br>*optional*|integer (int32)|
|**pageSize**  <br>*optional*|integer (int32)|
|**total**  <br>*optional*|integer (int64)|


<a name="9832eb12068b6b1627b21ae6b1ac060c"></a>
### 5.3.49. PageModel«TradeOrderDto»

|Name|Schema|
|---|---|
|**list**  <br>*optional*|< [TradeOrderDto](#tradeorderdto) > array|
|**pageNo**  <br>*optional*|integer (int32)|
|**pageNum**  <br>*optional*|integer (int32)|
|**pageSize**  <br>*optional*|integer (int32)|
|**total**  <br>*optional*|integer (int64)|


<a name="63fc5848d93402e6be9ab0d7419be4ca"></a>
### 5.3.50. PageModel«WithdrawCoinDetailDto»

|Name|Schema|
|---|---|
|**list**  <br>*optional*|< [WithdrawCoinDetailDto](#withdrawcoindetaildto) > array|
|**pageNo**  <br>*optional*|integer (int32)|
|**pageNum**  <br>*optional*|integer (int32)|
|**pageSize**  <br>*optional*|integer (int32)|
|**total**  <br>*optional*|integer (int64)|


<a name="pagerequest"></a>
### 5.3.51. PageRequest

|Name|Description|Schema|
|---|---|---|
|**pageNo**  <br>*optional*|Pages|integer (int32)|
|**pageSize**  <br>*optional*|Page Size|integer (int32)|


<a name="349f6b917324f326c7b17859b3a4b408"></a>
### 5.3.52. Pages«KlineRecord»

|Name|Schema|
|---|---|
|**list**  <br>*optional*|< [KlineRecord](#klinerecord) > array|
|**pageNum**  <br>*optional*|integer (int32)|
|**pageSize**  <br>*optional*|integer (int32)|
|**pages**  <br>*optional*|integer (int64)|
|**size**  <br>*optional*|integer (int32)|
|**startIndex**  <br>*optional*|integer (int32)|
|**total**  <br>*optional*|integer (int64)|


<a name="queryorderreq"></a>
### 5.3.53. QueryOrderReq

|Name|Description|Schema|
|---|---|---|
|**clientOrderNo**  <br>*required*|Broker Order No.|string|
|**nanoTime**  <br>*required*|Current Timestamp (nanoseconds)|integer (int64)|


<a name="settlequeryrequest"></a>
### 5.3.54. SettleQueryRequest

|Name|Description|Schema|
|---|---|---|
|**assetCode**  <br>*optional*|Coin Type|string|
|**pageNo**  <br>*optional*|Pages|integer (int32)|
|**pageSize**  <br>*optional*|Page Size|integer (int32)|
|**type**  <br>*optional*|Settlement Type: BROKER_FEE (trade fee), WITHDRAW_BROKER_FEE (withdrawal fee)|enum (BROKER_FEE, WITHDRAW_BROKER_FEE)|


<a name="settlerecorddto"></a>
### 5.3.55. SettleRecordDto

|Name|Schema|
|---|---|
|**amountAvailable**  <br>*optional*|number|
|**assetCode**  <br>*optional*|string|
|**brokerId**  <br>*optional*|string|
|**createDate**  <br>*optional*|string (date-time)|
|**requestNo**  <br>*optional*|string|
|**type**  <br>*optional*|enum (BROKER_FEE, WITHDRAW_BROKER_FEE)|


<a name="symbol"></a>
### 5.3.56. Symbol

|Name|Description|Schema|
|---|---|---|
|**priceAsset**  <br>*required*|Pricing Asset|string|
|**tradeAsset**  <br>*required*|Trading Asset |string|


<a name="symboldata"></a>
### 5.3.57. SymbolData

|Name|Description|Schema|
|---|---|---|
|**priceAsset**  <br>*optional*|Pricing Asset|string|
|**state**  <br>*optional*|Status：OPEN|string|
|**tradeAsset**  <br>*optional*|Trading Asset |string|


<a name="symbolfeeaddreq"></a>
### 5.3.58. SymbolFeeAddReq

|Name|Description|Schema|
|---|---|---|
|**feeMin**  <br>*required*|Minimum Fee: 0|string|
|**makerFeeRatio**  <br>*required*|MAKER Fee Ratio|string|
|**method**  <br>*required*|Method: RATIO|enum (RATIO)|
|**nanoTime**  <br>*required*|Current Timestamp (nanoseconds)|integer (int64)|
|**priceAsset**  <br>*required*|Pricing Asset|string|
|**takerFeeRatio**  <br>*required*|TAKER Fee Ratio|string|
|**tradeAsset**  <br>*required*|Trading Asset |string|


<a name="symbolfeelistqueryreq"></a>
### 5.3.59. SymbolFeeListQueryReq

|Name|Description|Schema|
|---|---|---|
|**nanoTime**  <br>*required*|Current Timestamp (nanoseconds)|integer (int64)|
|**symbolList**  <br>*optional*|Current Timestamp (nanoseconds)|< [Symbol](#symbol) > array|


<a name="symbolfeequeryreq"></a>
### 5.3.60. SymbolFeeQueryReq

|Name|Description|Schema|
|---|---|---|
|**nanoTime**  <br>*required*|Current Timestamp (nanoseconds)|integer (int64)|
|**priceAsset**  <br>*required*|Current Timestamp (nanoseconds)|string|
|**tradeAsset**  <br>*required*|Current Timestamp (nanoseconds)|string|


<a name="symbolqueryreq"></a>
### 5.3.61. SymbolQueryReq

|Name|Description|Schema|
|---|---|---|
|**coin**  <br>*required*|Coin Type|< string > array|
|**nanoTime**  <br>*required*|Current Timestamp (nanoseconds)|integer (int64)|


<a name="symbolsharingdata"></a>
### 5.3.62. SymbolSharingData

|Name|Description|Schema|
|---|---|---|
|**brokerId**  <br>*optional*|Broker ID|string|
|**brokerSharing**  <br>*optional*|Broker Sharing|number|
|**cloudSharing**  <br>*optional*|Cloud Sharing|number|
|**method**  <br>*optional*|Method: SHARING|string|
|**whitelistFee**  <br>*optional*|Whitelist Fee|number|


<a name="tradeorderdto"></a>
### 5.3.63. TradeOrderDto

|Name|Schema|
|---|---|
|**brokerFee**  <br>*optional*|number|
|**brokerId**  <br>*optional*|string|
|**brokerUid**  <br>*optional*|integer (int64)|
|**createDate**  <br>*optional*|string (date-time)|
|**fee**  <br>*optional*|number|
|**feeAsset**  <br>*optional*|string|
|**finishDate**  <br>*optional*|string (date-time)|
|**number**  <br>*optional*|number|
|**numberOver**  <br>*optional*|number|
|**price**  <br>*optional*|number|
|**requestNo**  <br>*optional*|string|
|**status**  <br>*optional*|enum (WAITING, PROCESSING, SUCCESS, CANCEL, FAIL)|
|**symbol**  <br>*optional*|string|
|**tradeFlag**  <br>*optional*|enum (BUY, SELL)|
|**tradeType**  <br>*optional*|enum (FIXED, MARKET)|
|**tradedMoney**  <br>*optional*|number|
|**tradedNumber**  <br>*optional*|number|


<a name="tradeorderqueryrequest"></a>
### 5.3.64. TradeOrderQueryRequest

|Name|Description|Schema|
|---|---|---|
|**beginTime**  <br>*optional*|Start Date|string (date-time)|
|**endTime**  <br>*optional*|End Date|string (date-time)|
|**orderType**  <br>*optional*|BUY, SELL|enum (BUY, SELL)|
|**pageNo**  <br>*optional*|Pages|integer (int32)|
|**pageSize**  <br>*optional*|Page Size|integer (int32)|
|**priceAsset**  <br>*optional*|Pricing Asset|string|
|**status**  <br>*optional*|Trade status: PROCESSING, SUCCESS, CANCEL, FAIL|enum (WAITING, PROCESSING, SUCCESS, CANCEL, FAIL)|
|**tradeAsset**  <br>*optional*|Trading Asset |string|
|**tradeFlag**  <br>*optional*|Order Type FIXED price, MARKET price|enum (FIXED, MARKET)|
|**uid**  <br>*optional*|User ID|integer (int64)|


<a name="transferinaddressdto"></a>
### 5.3.65. TransferInAddressDto

|Name|Schema|
|---|---|
|**address**  <br>*optional*|string|
|**addressid**  <br>*optional*|integer (int64)|
|**assetCode**  <br>*optional*|string|


<a name="unverifiedcountrequest"></a>
### 5.3.66. UnVerifiedCountRequest

|Name|Description|Schema|
|---|---|---|
|**assetCode**  <br>*optional*|Coin Type|string|
|**status**  <br>*optional*|Withdrawal Status: SUCCESS, PROCESSING, FAILURE, UNKNOWN, WAIT, REFUSE, CLOUD_REFUSE, SUSPEND|enum (SUCCESS, PROCESSING, FAILURE, UNKNOWN, WAIT, REFUSE, CLOUD_REFUSE, SUSPEND)|


<a name="userdata"></a>
### 5.3.67. UserData

|Name|Description|Schema|
|---|---|---|
|**birthday**  <br>*optional*|Birthday  <br>**Example** : `"2018-01-01"`|string|
|**brokerId**  <br>*optional*|Broker ID|string|
|**country**  <br>*optional*|Nationality|string|
|**email**  <br>*optional*|Email|string|
|**gender**  <br>*optional*|Gender|string|
|**ip**  <br>*optional*|User Registration IP|string|
|**isWhiteList**  <br>*optional*|Whitelist or Not   <br>**Example** : `false`|boolean|
|**name**  <br>*optional*|User Name|string|
|**phone**  <br>*optional*|Phone No.|string|
|**platId**  <br>*optional*|Platform User ID|string|
|**uid**  <br>*optional*|Broker User ID|integer (int64)|


<a name="withdrawcoindetaildto"></a>
### 5.3.68. WithdrawCoinDetailDto

|Name|Schema|
|---|---|
|**account**  <br>*optional*|string|
|**address**  <br>*optional*|string|
|**amount**  <br>*optional*|number|
|**assetCode**  <br>*optional*|string|
|**brokerFee**  <br>*optional*|number|
|**brokerId**  <br>*optional*|string|
|**clientOrderNo**  <br>*optional*|string|
|**createDate**  <br>*optional*|string (date-time)|
|**msg**  <br>*optional*|string|
|**number**  <br>*optional*|number|
|**platFee**  <br>*optional*|number|
|**status**  <br>*optional*|string|
|**uid**  <br>*optional*|integer (int64)|
|**updateDate**  <br>*optional*|string (date-time)|


<a name="withdrawcoinrequest"></a>
### 5.3.69. WithdrawCoinRequest

|Name|Description|Schema|
|---|---|---|
|**address**  <br>*optional*|Withdrawal Address|string|
|**amount**  <br>*optional*|Amount|number|
|**assetCode**  <br>*optional*|Coin Type|string|
|**clientOrderNo**  <br>*optional*|Client Order No.|string|
|**fee**  <br>*optional*|Fee|number|
|**message**  <br>*optional*|Withdrawal Information|string|
|**uid**  <br>*optional*|User ID|integer (int64)|


<a name="withdrawconfirmrequest"></a>
### 5.3.70. WithdrawConfirmRequest

|Name|Description|Schema|
|---|---|---|
|**clientOrderNo**  <br>*optional*|Client Order No.|string|
|**confirm**  <br>*optional*|Operation,  ADOPT, REFUSE|enum (ADOPT, REFUSE)|
|**refuseMs**  <br>*optional*|Refusal Reason|string|


<a name="withdrawqueryrequest"></a>
### 5.3.71. WithdrawQueryRequest

|Name|Description|Schema|
|---|---|---|
|**address**  <br>*optional*|Withdrawal Address|string|
|**assetCode**  <br>*optional*|Coin Type|string|
|**clientOrderNo**  <br>*optional*|Withdrawal Order No.|string|
|**email**  <br>*optional*|Email|string|
|**endDate**  <br>*optional*|End Date|string (date-time)|
|**pageNo**  <br>*optional*|Pages|integer (int32)|
|**pageSize**  <br>*optional*|Page Size|integer (int32)|
|**startDate**  <br>*optional*|Start Date|string (date-time)|
|**status**  <br>*optional*|Withdrawal Status: SUCCESS, PROCESSING, FAILURE, UNKNOWN, WAIT, REFUSE, CLOUD_REFUSE, SUSPEND|enum (SUCCESS, PROCESSING, FAILURE, UNKNOWN, WAIT, REFUSE, CLOUD_REFUSE, SUSPEND)|
|**uid**  <br>*optional*|User ID|integer (int64)|


<a name="withdrawtotalamountrequest"></a>
### 5.3.72. WithdrawTotalAmountRequest

|Name|Description|Schema|
|---|---|---|
|**assetCode**  <br>*optional*|Coin Type|string|
|**status**  <br>*optional*|Withdrawal Status: SUCCESS, PROCESSING, FAILURE, UNKNOWN, WAIT, REFUSE, CLOUD_REFUSE, SUSPEND|enum (SUCCESS, PROCESSING, FAILURE, UNKNOWN, WAIT, REFUSE, CLOUD_REFUSE, SUSPEND)|
|**uid**  <br>*optional*|User ID|integer (int64)|


<a name="DepositApiResponseDto"></a>
### 5.3.73. DepositApiResponseDto

|Name|Description|Schema|
|---|---|---|
|**date**  <br>*optional*||[DepositResponseData](#DepositResponseData)|
|**code**  <br>*optional*|Return Code 0000|String|
|**type**  <br>*optional*|Callback Type DEPOSIT_CONFIME(deposited)|enum (DEPOSIT_CONFIME,WITHDROW_REFUND,WITHDROW_CONFIME)|


<a name="DepositResponseData"></a>
### 5.3.74. DepositResponseData

|Name|Description|Schema|
|---|---|---|
|**brokerId**  <br>*optional*|Broker ID |String|
|**uid**  <br>*optional*|User ID|Long|
|**assetCode**  <br>*optional*|Coin Type|String|
|**toWallet**  <br>*optional*|deposit Address |String|
|**amount**  <br>*optional*|deposit Amount|BigDecimal|
|**status**  <br>*optional*|deposit Status|String|
|**message**  <br>*optional*|Message |String|
|**finishDate**  <br>*optional*|Time Received|Date|

<a name="WithdrawApiResponseDto"></a>
### 5.3.75. WithdrawApiResponseDto

|Name|Description|Schema|
|---|---|---|
|**date**  <br>*optional*| |[WithdrawResponseData](#WithdrawResponseData)|
|**code**  <br>*optional*|Return Code 0000(received)/9999(blocked)|String|
|**type**  <br>*optional*|Callback Type WITHDROW_REFUND(withdrawal blocked)、WITHDROW_CONFIME(withdrawal confirmed)|enum (DEPOSIT_CONFIME,WITHDROW_REFUND,WITHDROW_CONFIME)|


<a name="WithdrawResponseData"></a>
### 5.3.76. WithdrawResponseData

|Name|Description|Schema|
|---|---|---|
|**brokerId**  <br>*optional*|Broker ID |String|
|**uid**  <br>*optional*|User ID|Long|
|**assetCode**  <br>*optional*|Coin Type|String|
|**clientOrderNo**  <br>*optional*|Client Order No. |String|
|**coinAddress**  <br>*optional*|Withdrawal Address|String|
|**number**  <br>*optional*|Actual Amount Received|BigDecimal|
|**realNumber**  <br>*optional*|Client Order No. |BigDecimal|
|**fee**  <br>*optional*|Fee|BigDecimal|
|**status**  <br>*optional*|Withdrawal Status|String|
|**message**  <br>*optional*|Message |String|
|**createDate**  <br>*optional*|Withdrawal Time|Date|
|**finishDate**  <br>*optional*|Received Time|Date|
|**nanoTime**  <br>*optional*|Timestamp|Long|