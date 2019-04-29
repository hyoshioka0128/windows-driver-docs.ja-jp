---
title: 推奨される音声通信デバイス ID
description: 推奨される音声通信デバイス ID
ms.assetid: ed0fbba3-cc9e-48d6-9ab5-360f8aab3ed6
keywords:
- WDM オーディオ拡張 WDK、音声通信デバイス Id
- 音声通信デバイス Id の WDK オーディオ
- デバイス Id の WDK オーディオ
- オーディオ デバイスを識別します。
- 好みのデバイス Id の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fb5b8b04d2bf243e2d3b3b181e5d45b54d05b7a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328750"
---
# <a name="preferred-voice-communications-device-id"></a>推奨される音声通信デバイス ID


## <span id="preferred_voice_communications_device_id"></span><span id="PREFERRED_VOICE_COMMUNICATIONS_DEVICE_ID"></span>


Windows 2000 以降、Windows のマルチ メディア機能と Windows Me で**waveInMessage**と**waveOutMessage**音声通信には、好みのデバイスのデバイス ID を取得できます。 これら 2 つの関数優先の音声通信デバイスの Id の取得 wave 入力および wave 出力では、それぞれします。 各デバイス ID では、一般的な wave オーディオの使用状況に適した wave デバイスとは異なり、音声通信で具体的には推奨される wave デバイスを識別します。 一般的な wave オーディオは、好みのデバイスのデバイス ID を取得する方法の詳細については、次を参照してください。[優先のデバイス ID にアクセスする](accessing-the-preferred-device-id.md)します。

推奨される音声通信デバイスを知ることは、アプリケーション プログラムをたとえば、2 つまたは複数のデバイスの一覧から開くには、デバイスを選択するために役立ちます。 このようなアプリケーションは、通常、リスト内のデバイス間では、好みのデバイスを示す必要があります。

現在の推奨される音声通信デバイスのデバイス ID を取得するアプリケーションは、wave を呼び出す*Xxx*メッセージ パラメーターを定数に設定して関数をメッセージ[ **DRVM\_マッパー\_CONSOLEVOICECOM\_取得**](https://msdn.microsoft.com/library/windows/hardware/ff536361)します。

呼び出すときに、 **waveInMessage**または**waveOutMessage** 、DRVM で関数を\_マッパー\_CONSOLEVOICECOM\_メッセージ、デバイスの値を指定WAVE として処理\_マッパー HWAVEIN または HWAVEOUT 適切なハンドルの種類には、この値をキャストします。 Wave *Xxx*メッセージ関数は、有効なデバイス ハンドルの代わりにこの値を受け付けるようにするデバイスを開くことがなくアプリケーションの既定のデバイス ID のクエリを実行できます。 詳細については、wave *Xxx*メッセージ関数を参照してください[System-Intercepted デバイス メッセージ](system-intercepted-device-messages.md)します。

DRVM\_マッパー\_優先\_(waveIn または waveOut) は、対象デバイス マッパーによって GET メッセージをインターセプトします。 Wave デバイス マッパーの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

 




