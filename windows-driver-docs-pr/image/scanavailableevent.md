---
title: Scanのイベント要素
description: 必要な Scan使用イベント要素は、サブスクライブされているスキャンデバイスがジョブをスキャンする準備ができていることをクライアントに通知します。
ms.assetid: 82ebfa36-60df-44dd-a928-e751deeea5b0
keywords:
- Scanているイベント要素のイメージングデバイス
topic_type:
- apiref
api_name:
- wscn ScanAvailableEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b01802172f27f6d614954004f5e26b37a9079f05
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652948"
---
# <a name="scanavailableevent-element"></a>Scanのイベント要素


必要な**Scan使用イベント**要素は、サブスクライブされているスキャンデバイスがジョブをスキャンする準備ができていることをクライアントに通知します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScanAvailableEvent>
  child elements
</wscn:ScanAvailableEvent>
```

<a name="attributes"></a>属性
----------

属性はありません。

## <a name="child-elements"></a>子要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="clientcontext.md" data-raw-source="[&lt;strong&gt;ClientContext&lt;/strong&gt;](clientcontext.md)"><strong>ClientContext</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanidentifier.md" data-raw-source="[&lt;strong&gt;ScanIdentifier&lt;/strong&gt;](scanidentifier.md)"><strong>ScanIdentifier</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

WSD Scan サービスは、ユーザーがスキャン先を選択し、スキャンデバイスでスキャンを開始したときに、登録されているクライアントに**scanているイベント**要素を送信します。

クライアントは、スキャンが利用できる**イベント**イベントを受け取るために、WSD Scan サービスを使用してサブスクリプションを作成する必要があります。 クライアントは、 **&lt;wse: Subscribe&gt;** request 操作要素を介してスキャンサービスに要求メッセージを送信することで、サブスクリプションを作成します。

Subscribe 要求には、 [**scandestinations**](scandestinations.md)要素に1つ以上の送信先が含まれています。 スキャンが利用できる**イベント**通知が送信されるたびに、スキャンサービスはこれらの変換先を使用して、1つのクライアントにフィルターを適用します。 このフィルターは、ユーザーが [スキャン] ボタンをクリックしたときに、スキャンサービスがすべてのクライアントに通知しないようにします。 拡張要素は、WSD Scan サービス名前空間で定義され、 **&lt;wse: Subscribe&gt;** 要求本文に追加されます。

WSD スキャンサービスがクライアントのサブスクリプション作成要求を受け入れる場合、サービスは **&lt;wse: SubscribeResponse&gt;** response operation 要素を使用して応答する必要があります。 Subscribe response には、 [**destinationresponses**](destinationresponses.md) extension 要素に1つ以上の宛先応答が含まれています。これにより、サブスクリプションを受け入れたスキャンデバイスにサブスクリプションを接続できます。

**&lt;wse: Subscribe&gt;** と **&lt;wse: SubscribeResponse&gt;** 要素については、仕様で説明されています。

<a name="examples"></a>例
--------

次のコード例は、スキャンが利用できるイベントイベントを WSD Scan サービスから受信するためにクライアントがサブスクライブする方法を示しています。

```xml
<soap:Envelope
    xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
    xmlns:wsa="https://schemas.xmlsoap.org/ws/2004/08/addressing"
    xmlns:wse="https://schemas.xmlsoap.org/ws/2004/08/eventing"
    xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan>
    soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >
  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
      <wsa:Action>
         https://schemas.xmlsoap.org/ws/2004/08/eventing/Subscribe
      </wsa:Action>
      <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
      <wsa:ReplyTo>
        <wsa:Address>https://www.example.com/MyEventSink</wsa:Address>
      </wsa:ReplyTo>
  </soap:Header>
  <soap:Body>
    <wse:Subscribe>
      <wse:Delivery>
        <wse:NotifyTo>
          <wsa:Address>
            https://www.example.com/MyEventSink/OnScanAvailableForMe
          </wsa:Address>
        </wse:NotifyTo>
      </wse:Delivery>
      <wse:Expires>P0Y0M0DT30H0M0S</wse:Expires>
      <wse:Filter xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan">
        ScanAvailableEvent
      </wse:Filter>
      <wscn:ScanDestinations>
        <wscn:ScanDestination>
          <wscn:ClientDisplayString>Den Computer</wscn:ClientDisplayString>
          <wscn:ClientContext>App1ScanID2345</wscn:ClientContext>
        </wscn:ScanDestination>
      </wscn:ScanDestinations>
    </wse:Subscribe>
    </soap:Body
</soap:Envelope>
```

次のコード例では、クライアントのサブスクリプション要求に対する WSD Scan サービスの応答を示します。

```xml
<soap:Envelope
    xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
    xmlns:wsa="https://schemas.xmlsoap.org/ws/2004/08/addressing"
    xmlns:wse="https://schemas.xmlsoap.org/ws/2004/08/eventing"
    xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan">
    soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >
  <soap:Header>
    <wsa:To>https://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous</wsa:To>
    <wsa:Action>
      https://schemas.xmlsoap.org/ws/2004/08/eventing/SubscribeResponse
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheSubscribe</wsa:RelatesTo>
  </soap:Header>
  <soap:Body>
    <wse:SubscribeResponse>
        <wse:SubscriptionManager>
             <!-- Elements removed for clarity  -->
        </wse:SubscriptionManager>
        <wse:Expires>P0Y0M0DT30H0M0S</wse:Expires>
        <wscn:DestinationResponses>
          <wscn:DestinationResponse>
            <wscn:ClientContext>App1ScanID2345</wscn:ClientContext>
            <wscn:DestinationToken>Client3478</wscn:DestinationToken>
          </wscn:DestinationResponse>
        </wscn:DestinationResponses>
      </wse:SubscribeResponse>
    </soap:Body
</soap:Envelope>
```

次のコード例では、WSD Scan サービスが Scan使用イベントをクライアントに送信する方法を示します。

```xml
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2004/08/addressing"
  xmlns:wse="https://schemas.xmlsoap.org/ws/2004/08/eventing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding'>

  <soap:Header>
    <wsa:To>AddressofEventSink</wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/ScanAvailableEvent
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:ScanAvailableEvent>
      <wscn:ClientContext>App1ScanID2345</wscn:ClientContext>
      <wscn:ScanIdentifier>AnyUniqueIdentifierSuchAsAGUID</wscn:ScanIdentifier>
    </wscn:ScanAvailableEvent>
  </soap:Body
</soap:Envelope>
```

## <a name="see-also"></a>「


[**ClientContext**](clientcontext.md)

[**DestinationResponses**](destinationresponses.md)

[**スキャン先**](scandestinations.md)

[**ScanIdentifier**](scanidentifier.md)

 

 






