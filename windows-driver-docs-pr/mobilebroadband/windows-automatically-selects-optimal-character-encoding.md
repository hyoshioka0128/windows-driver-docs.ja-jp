---
title: Windows で自動的に最適な文字エンコードを選択する
description: Windows で自動的に最適な文字エンコードを選択する
ms.assetid: 3fde6e89-c9ea-43d2-a999-506686b223f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2495041a5e4825c9a7c20af70004eaebc2f0810
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377626"
---
# <a name="windows-automatically-selects-optimal-character-encoding"></a>Windows で自動的に最適な文字エンコードを選択する


Windows 8、Windows 8.1、および Windows 10 は、メッセージの内容でサポートされている最も効率的なエンコーディングに基づいて、SMS メッセージを送信するときに使用するエンコーディングの最適な文字を選択します。 SMS は、ケース全体のメッセージが unicode でエンコードされた 1 つ以上の無効な文字が含まれている場合を除き、7 ビットの文字セットにエンコードされます。

**テキスト モード インターフェイスを使用して SMS メッセージを送信するための JavaScript コードの例**

``` syntax
try
{
    if (smsDevice != null)
    {
      // defines a text message
      var smsMessage = new Windows.Devices.Sms.SmsTextMessage();
      smsMessage.to = id("phoneNumber").value;
      smsMessage.body = id("messageText").value + "\n\nSent via Windows 8 SMS API";
      var sendSmsMessageOperation = smsDevice.sendMessageAsync(smsMessage);
      console.log("Sending message...");
      sendSmsMessageOperation.then(function (reply)
      {
        console.log("Text message sent.");
      });
    }
    else
    {
      console.log("No SMS device found");
    }
} catch (err) {
    console.log("SMS exception: " + err);
}
```

必要に応じて、最適なエンコーディング機能を無効にし、使用する文字セットを指定できます。

Windows 8、Windows 8.1、および Windows 10 のサポートの一般的な文字は、GSM (3 gpp) と CDMA (3GPP2) ネットワークと互換性のあるモバイル ブロード バンド ネットワーク アダプターを設定します。

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

 

GSM 文字セットが定義されている[3 gpp TS 23.038。「のアルファベットおよび言語固有の情報」](https://www.3gpp.org/DynaReport/23038.md)します。 CDMA 文字セットが定義されている[3GPP2 C.R1001-d](http://www.3gpp2.org/Public_html/specs/C.R1001-D_v1.0_110403.pdf)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[テキスト モード インターフェイスを使用して SMS を送信します。](send-sms-by-using-the-text-mode-interface.md)

 

 






