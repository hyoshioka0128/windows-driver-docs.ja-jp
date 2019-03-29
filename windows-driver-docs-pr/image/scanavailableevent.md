---
title: ScanAvailableEvent 要素
description: 必要な ScanAvailableEvent 要素は、クライアントがサブスクライブしているデバイスのスキャンがジョブをスキャンする準備がクライアントに通知します。
ms.assetid: 82ebfa36-60df-44dd-a928-e751deeea5b0
keywords:
- ScanAvailableEvent 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScanAvailableEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2fa10ab3ecc8d0929617ca0648d89c0cd941c2a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570400"
---
# <a name="scanavailableevent-element"></a>ScanAvailableEvent 要素


必要な**ScanAvailableEvent**要素は、クライアントがサブスクライブしているデバイスのスキャンがジョブをスキャンする準備が、クライアントを通知します。

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

<a name="remarks"></a>コメント
-------

WSD スキャン サービスの送信、 **ScanAvailableEvent**要素をユーザーがスキャンの変換先を選択し、デバイスのスキャンでスキャンが開始したときに、登録されているクライアント。

クライアントは WSD スキャン サービスが受信すると、サブスクリプションを作成する必要があります**ScanAvailableEvent**イベント。 クライアントによってスキャン サービスに要求メッセージを送信することによって、サブスクリプションを作成します、  **&lt;wse: サブスクライブ&gt;** 要求操作の要素。

サブスクライブ要求には 1 つまたは複数の変換先が含まれています、 [ **ScanDestinations** ](scandestinations.md)拡張機能の要素。 スキャン サービスは、単一のクライアントに送信するたびにフィルター処理するこれらの変換先を使用する**ScanAvailableEvent**通知します。 このフィルターは、スキャン サービスがスキャン ボタンを押した場合に、すべてのクライアントを通知することを防ぎます。 拡張機能の要素の WSD スキャン サービスの名前空間で定義されているし、に追加し、  **&lt;wse: サブスクライブ&gt;** 要求本文。

WSD スキャン サービスがサブスクリプションを作成するクライアントの要求を受け入れる場合、サービスがで応答する必要があります、 **&lt;wse:SubscribeResponse&gt;** 応答操作の要素。 購読の応答にはで 1 つまたは複数の送信先の応答が含まれています、 [ **DestinationResponses** ](destinationresponses.md)拡張要素のするのに役立ちますが、使用できるデバイスのスキャンにサブスクリプションを接続します。

 **&lt;Wse: サブスクライブ&gt;** と**&lt;wse:SubscribeResponse&gt;** 要素は、仕様で説明します。

<a name="examples"></a>使用例
--------

次のコード例では、WSD スキャン サービスから ScanAvailableEvent イベントを受信するクライアントがサブスクライブする方法を示します。

```xml
<soap:Envelope
    xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
    xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
    xmlns:wse="http://schemas.xmlsoap.org/ws/2004/08/eventing"
    xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan>
    soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >
  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
      <wsa:Action>
         http://schemas.xmlsoap.org/ws/2004/08/eventing/Subscribe
      </wsa:Action>
      <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
      <wsa:ReplyTo>
        <wsa:Address>http://www.example.com/MyEventSink</wsa:Address>
      </wsa:ReplyTo>
  </soap:Header>
  <soap:Body>
    <wse:Subscribe>
      <wse:Delivery>
        <wse:NotifyTo>
          <wsa:Address>
            http://www.example.com/MyEventSink/OnScanAvailableForMe
          </wsa:Address>
        </wse:NotifyTo>
      </wse:Delivery>
      <wse:Expires>P0Y0M0DT30H0M0S</wse:Expires>
      <wse:Filter xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan">
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

次のコード例では、クライアントのサブスクリプション要求 WSD スキャン サービスの応答を示します。

```xml
<soap:Envelope
    xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
    xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
    xmlns:wse="http://schemas.xmlsoap.org/ws/2004/08/eventing"
    xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan">
    soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >
  <soap:Header>
    <wsa:To>http://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous</wsa:To>
    <wsa:Action>
      http://schemas.xmlsoap.org/ws/2004/08/eventing/SubscribeResponse
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

次のコード例では、WSD スキャン サービスが、ScanAvailableEvent をクライアントに送信する方法を示します。

```xml
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
  xmlns:wse="http://schemas.xmlsoap.org/ws/2004/08/eventing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding'>

  <soap:Header>
    <wsa:To>AddressofEventSink</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/ScanAvailableEvent
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

## <a name="see-also"></a>関連項目


[**ClientContext**](clientcontext.md)

[**DestinationResponses**](destinationresponses.md)

[**ScanDestinations**](scandestinations.md)

[**ScanIdentifier**](scanidentifier.md)

 

 






