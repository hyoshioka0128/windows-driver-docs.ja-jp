---
title: Getjobhistory Request 要素
description: 必須の Getjobhistory Request 要素は、以前に完了したジョブのジョブ関連変数の概要を要求します。
ms.assetid: 679a2256-2b3f-4a54-be06-8b414acab679
keywords:
- Getjobhistory 要求要素のイメージングデバイス
topic_type:
- apiref
api_name:
- wscn GetJobHistoryRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbf8e434786b3917bf67f17f87d4247d7b3dab1e
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652974"
---
# <a name="getjobhistoryrequest-element"></a>Getjobhistory Request 要素


必須の**Getjobhistory request**要素は、以前に完了したジョブのジョブ関連変数の概要を要求します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:GetJobHistoryRequest/>
```

<a name="attributes"></a>属性
----------

属性はありません。

## <a name="child-elements"></a>子要素


子要素はありません。

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

WSD Scan サービスは、 **Getjobhistory request** operation 要素をサポートしている必要があります。

クライアントは、 **Getjobhistory 要求**を呼び出して、以前に完了したジョブのジョブ関連変数の概要を含むリストを取得できます。 WSD Scan サービスは、クライアントが要求した情報または適切なエラーコードを含む[**Getjobhistory response**](getjobhistoryresponse.md) operation 要素を使用して応答する必要があります。

WSD Scan サービスが保持するジョブ履歴の量は、実装に固有です。

この操作は、[**一般的な WSD Scan サービス操作のエラーコード**](common-wsd-scan-service-operation-error-codes.md)をすべて返すことができます。 エラーを報告する方法の詳細については、「 [WSD Scan サービス操作のエラー報告](wsd-scan-service-operation-error-reporting.md)」を参照してください。

<a name="examples"></a>例
--------

次のコード例には、ジョブ履歴の要求が含まれています。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobHistory
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:GetJobHistoryRequest />
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>「


[**Getjobhistory 応答**](getjobhistoryresponse.md)

 

 






