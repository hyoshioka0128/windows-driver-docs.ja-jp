---
title: 下書き SMS の文字とセグメントを計算する
description: 下書き SMS の文字とセグメントを計算する
ms.assetid: abbec0b0-dfa8-43e9-8b48-e99680d56b42
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4d1966765bfc301892594d3f87ea859f8ba894d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392981"
---
# <a name="calculate-characters-and-segments-of-a-draft-sms"></a>下書き SMS の文字とセグメントを計算する


モバイル ブロード バンド SMS プラットフォームでは、SMS メッセージの構成時に、残りの文字の数と (マルチパート メッセージの場合) で使用されるセグメントの数を推定する関数を提供します。

**注**  各セグメントの文字数は定数ではなく、メッセージ本文とネットワークの種類のテキスト文字列に基づいて変化します。 GSM ネットワークで 1 つの SMS メッセージを 7 ビットの 160 文字、または 70 の 16 ビット文字までサポートします。 複数のセグメントをまたがるメッセージでは、追加ヘッダー情報のためには、各セグメントに 142 7 ビットの文字をサポートします。

 

SMS メッセージを作成するときに使用されるセグメントの数に正確な見積もりを提供するため、ユーザーが送信される SMS メッセージごとに請求される通常ユーザーの信頼度を昇格させます。

**JavaScript コードの例**

``` syntax
var smsMessage = new Windows.Devices.Sms.SmsTextMessage();
smsMessage.body = id('messageText').value;  // Set message body text to text of messageText HTML element
var messageLength = smsDevice.calculateLength(smsMessage);
id('remainingCharsCount').innerText = messageLength.charactersPerSegment - messageLength.characterCountLastSegment;
id('messageSegmentsCount').innerText = messageLength.segmentCount;
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[テキスト モード インターフェイスを使用して SMS を送信します。](send-sms-by-using-the-text-mode-interface.md)

 

 






