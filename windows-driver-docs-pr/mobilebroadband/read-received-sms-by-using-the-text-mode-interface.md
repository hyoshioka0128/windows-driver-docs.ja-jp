---
title: テキスト モード インターフェイスを使用して受信した SMS を読み込む
description: テキスト モード インターフェイスを使用して受信した SMS を読み込む
ms.assetid: 5e095fc0-59bf-4ec4-96a3-efe6f4ae054f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 640cafd6eecf72b8d19e1380389ed1f7a6bce780
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578889"
---
# <a name="read-received-sms-by-using-the-text-mode-interface"></a>テキスト モード インターフェイスを使用して受信した SMS を読み込む


テキスト モードのインターフェイスで、SMS メッセージの単純なプレーン テキストに適していますが、読み取りまたは PDU モード読み取りは、SMS メッセージをデコードの高度なコントロールの適切なインターフェイス間を使用して選択できます。

受信したメッセージは、モバイル ブロード バンド デバイス上でエンコードされた形式で格納されます。 モバイル ブロード バンド SMS プラットフォームでは、プレーン テキストを受信したメッセージのデコードをサポートします。 受信したメッセージのデコードがサポートされている文字セットでは、送信されたメッセージのエンコードのサポートされている文字セットと同じです。

次の表では、テキスト モード API でサポートされている文字エン コードを示します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>ネットワークの種類</th>
<th>文字セット</th>
<th>1 つの SMS セグメントの文字制限</th>
<th>マルチパートの SMS セグメントの文字制限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>GSM</p></td>
<td><p>GSM 7 ビットの既定のアルファベットと、GSM 7 ビットの既定のアルファベット拡張テーブル</p></td>
<td><p>160</p></td>
<td><p>142</p></td>
</tr>
<tr class="even">
<td><p>CDMA</p></td>
<td><p>7 ビット ASCII</p></td>
<td><p>160 (ネットワークによって異なることができます)</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>CDMA</p></td>
<td><p>Unicode</p></td>
<td><p>70 (ネットワークによって異なることができます)</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>

 

**読み取り用の JavaScript コードの例は、テキスト モード インターフェイスを使用して SMS メッセージを受信しました。**

``` syntax
try
{
  if (smsDevice!= null)
  {
    var messageStore = smsDevice.messageStore;
    var messageID = id('whichMessage').value;

    var getSmsMessageOperation = messageStore.getMessageAsync(messageID);

    getSmsMessageOperation.operation.completed = function ()
    {
      result = getSmsMessageOperation.operation.getResults();
      var readableMessage = new Windows.Devices.Sms.SmsTextMessage.fromBinaryMessage(result);
      id('fromWho').innerHTML = readableMessage.from;
      id('fromMessageBody').innerHTML = readableMessage.body;
      console.log("Successfully retrieved message " + messageID + " from message store.");
    }
    getSmsMessageOperation.operation.start();
  }
  else 
  {
    console.log("No SMS Device Found");
  }
}
catch (err) 
{
  console.log("SMS did not set up: " + err);
}
```

**注**   SMS クライアント アプリは、長期にわたる複数のセグメントがメッセージし、メッセージ全体を再構築は、連結する Windows によって提供されるデコードされたセグメント化情報を使用できます。 セグメント化された SMS メッセージの詳細については、次を参照してください。 [Windows が自動的に時間の長いメッセージをセグメント](windows-automatically-segments-long-messages.md)します。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[SMS のアプリの開発](developing-sms-apps.md)

 

 






