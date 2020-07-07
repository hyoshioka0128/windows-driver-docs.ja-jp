---
title: Getjobhistory Response 要素
description: 必須の Getjobhistory Response 要素は、完了したジョブの概要を返します。
ms.assetid: 85c9edb4-fe6c-49a7-899a-71ce65e38852
keywords:
- Getjobhistory Response 要素のイメージングデバイス
topic_type:
- apiref
api_name:
- wscn GetJobHistoryResponse
api_type:
- Schema
ms.date: 07/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: fb0423ff4198ead5198f18f8274e680ca67f224a
ms.sourcegitcommit: 40d7d538756767d26bbda636589f614f85a6fab3
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86020069"
---
# <a name="getjobhistoryresponse-element"></a>Getjobhistory Response 要素

必須の**Getjobhistory response**要素は、完了したジョブの概要を返します。

## <a name="usage"></a>使用

```xml
<wscn:GetJobHistoryResponse>
  child elements
</wscn:GetJobHistoryResponse>
```

## <a name="attributes"></a>属性

属性はありません。

## <a name="child-elements"></a>子要素

| 要素 |
|--|
| [**JobHistory**](jobhistory.md) |

## <a name="parent-elements"></a>親要素

親要素はありません。

## <a name="remarks"></a>注釈

WSD Scan サービスは、 **Getjobhistory response** operation 要素をサポートしている必要があります。

クライアントは、 [**Getjobhistory 要求**](getjobhistoryrequest.md)を呼び出して、以前に完了したジョブのジョブ関連の変数の値を確認できます。 WSD Scan サービスは、クライアントが要求した情報または適切なエラーコードを含む**Getjobhistory response** operation 要素を使用して応答する必要があります。

WSD Scan サービスによって管理されるジョブ履歴の量は、実装に固有のものです。

## <a name="examples"></a>例

次のコード例では、ジョブ履歴に対するクライアントの要求に応答して、ジョブ履歴が返されないようにする方法を示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      https://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobHistory
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetJobHistoryRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:GetJobHistoryResponse>
      <wscn:JobHistory />
    </wscn:GetJobHistoryResponse >
  </soap:Body>
</soap:Envelope>
```

次のコード例では、最後の2つの完了したジョブのジョブと関連データの一覧を返します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      https://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobHistory
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetJobHistoryRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:GetJobHistoryResponse>
      <wscn:JobHistory>
        <wscn:JobSummary>
          <wscn:JobId>1</wscn:JobId>
          <wscn:JobName>SampleJob 1</wscn:JobName>
          <wscn:JobOriginatingUserName>Joe.Smith</wscn:JobOriginatingUserName>
          <wscn:JobState>Completed</wscn:JobState>
          <wscn:JobStateReasons>
            <wscn:JobStateReason>None</wscn:JobStateReason>
          </wscn:JobStateReasons>
          <wscn:ScansCompleted>4</wscn:ScansCompleted>
        </wscn:JobSummary>
        <wscn:JobSummary>
          <wscn:JobId>2</wscn:JobId>
          <wscn:JobName>Sample Job 2</wscn:JobName>
          <wscn:JobOriginatingUserName>JaneRogers</wscn:JobOriginatingUserName>
          <wscn:JobState>Canceled</wscn:JobState>
          <wscn:JobStateReasons>
            <wscn:JobStateReason>JobCanceledAtDevice</wscn:JobStateReason>
          </wscn:JobStateReasons>
          <wscn:ScansCompleted>1</wscn:ScansCompleted>
        </wscn:JobSummary>
      </wscn:JobHistory>
    </wscn:GetJobHistoryResponse >
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>こちらもご覧ください

[**GetJobHistoryRequest**](getjobhistoryrequest.md)

[**JobHistory**](jobhistory.md)
