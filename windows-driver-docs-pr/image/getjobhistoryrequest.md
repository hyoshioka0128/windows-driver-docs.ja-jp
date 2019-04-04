---
title: GetJobHistoryRequest element
description: 必要な GetJobHistoryRequest 要素は、以前に完了したジョブのジョブに関連する変数の概要を要求します。
ms.assetid: 679a2256-2b3f-4a54-be06-8b414acab679
keywords:
- GetJobHistoryRequest element Imaging Devices
topic_type:
- apiref
api_name:
- wscn GetJobHistoryRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d76f49c102a7756f109d077fb517d6182712d33d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530697"
---
# <a name="getjobhistoryrequest-element"></a>GetJobHistoryRequest element


必要な**GetJobHistoryRequest**要素は、以前に完了したジョブのジョブに関連する変数の概要を要求します。

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

WSD スキャン サービスをサポートする必要があります、 **GetJobHistoryRequest**操作の要素。

クライアントが呼び出すことができます**GetJobHistoryRequest**前に完了したジョブのジョブに関連する変数の要約を含む一覧を取得します。 WSD スキャン サービスの応答でなければなりません、 [ **GetJobHistoryResponse** ](getjobhistoryresponse.md)クライアントが要求した情報が含まれる操作の要素または適切なエラー コード。

WSD スキャン サービスがジョブ履歴の量は、実装に固有です。

この操作は、のすべてを返すことができます、 [ **WSD スキャン サービス操作の一般的なエラー コード**](common-wsd-scan-service-operation-error-codes.md)します。 エラーを報告する方法の詳細については、[WSD スキャン サービス操作エラー報告](wsd-scan-service-operation-error-reporting.md)を参照してください。

<a name="examples"></a>例
--------

次のコード例には、ジョブ履歴の要求が含まれています。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobHistory
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:GetJobHistoryRequest />
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>関連項目


[**GetJobHistoryResponse**](getjobhistoryresponse.md)

 

 






