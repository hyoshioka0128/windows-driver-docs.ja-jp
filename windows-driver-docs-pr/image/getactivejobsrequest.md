---
title: GetActiveJobsRequest 要素
description: Required GetActiveJobsRequest 要素は、スキャンデバイスで現在アクティブなすべてのジョブの概要を要求します。
ms.assetid: 4dc7bc64-b62f-4634-8f0e-64039b9f8609
keywords:
- GetActiveJobsRequest 要素イメージングデバイス
topic_type:
- apiref
api_name:
- wscn GetActiveJobsRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 419f9d963aa39267089a641ef3f073b5ed1bc1c0
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652980"
---
# <a name="getactivejobsrequest-element"></a>GetActiveJobsRequest 要素


Required **GetActiveJobsRequest**要素は、スキャンデバイスで現在アクティブなすべてのジョブの概要を要求します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:GetActiveJobsRequest/>
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

WSD Scan サービスは、 **GetActiveJobsRequest**操作をサポートしている必要があります。

クライアントは、 **GetActiveJobsRequest**を呼び出して、現在アクティブなすべてのスキャンジョブのジョブ関連変数の概要を含むリストを取得します。 WSD Scan サービスは、クライアントが要求した情報または適切なエラーコードを含む[**GetActiveJobsResponse**](getactivejobsresponse.md)要素で応答する必要があります。

この操作は、[**一般的な WSD Scan サービス操作のエラーコード**](common-wsd-scan-service-operation-error-codes.md)をすべて返すことができます。 エラーを報告する方法の詳細については、「 [WSD Scan サービス操作のエラー報告](wsd-scan-service-operation-error-reporting.md)」を参照してください。

<a name="examples"></a>例
--------

次のコード例は、すべてのアクティブなスキャンジョブの要求を示しています。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetActiveJobs
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:GetActiveJobsRequest />
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>「


[**GetActiveJobsResponse**](getactivejobsresponse.md)

 

 






