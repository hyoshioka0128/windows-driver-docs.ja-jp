---
title: GetActiveJobsRequest 要素
description: 必要な GetActiveJobsRequest 要素は、デバイスのスキャンで現在アクティブなすべてのジョブの概要を要求します。
ms.assetid: 4dc7bc64-b62f-4634-8f0e-64039b9f8609
keywords:
- GetActiveJobsRequest 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn GetActiveJobsRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34af8b8822b279e7e3b31e1f2b2685b17dd0b266
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357534"
---
# <a name="getactivejobsrequest-element"></a>GetActiveJobsRequest 要素


必要な**GetActiveJobsRequest**要素は、デバイスのスキャンで現在アクティブなすべてのジョブの概要を要求します。

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

<a name="remarks"></a>コメント
-------

WSD スキャン サービスをサポートする必要があります、 **GetActiveJobsRequest**操作。

クライアントが呼び出す**GetActiveJobsRequest**現在アクティブなスキャンのすべてのジョブのジョブに関連する変数の要約を含む一覧を取得します。 WSD スキャン サービスの応答でなければなりません、 [ **GetActiveJobsResponse** ](getactivejobsresponse.md)のよく寄せられるクライアント情報を格納する要素または適切なエラー コード。

この操作は、のすべてを返すことができます、 [ **WSD スキャン サービス操作の一般的なエラー コード**](common-wsd-scan-service-operation-error-codes.md)します。 エラーを報告する方法の詳細については、次を参照してください。 [WSD スキャン サービス操作エラー報告](wsd-scan-service-operation-error-reporting.md)します。

<a name="examples"></a>使用例
--------

次のコード例では、すべてのアクティブなスキャン ジョブの要求を示します。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetActiveJobs
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:GetActiveJobsRequest />
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>関連項目


[**GetActiveJobsResponse**](getactivejobsresponse.md)

 

 






