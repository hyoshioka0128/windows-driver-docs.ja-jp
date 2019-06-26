---
title: 推奨されるデバイス ID へのアクセス
description: 推奨されるデバイス ID へのアクセス
ms.assetid: ef964ce5-8bcc-4ab0-9522-b05a8a6bdf74
keywords:
- 好みのデバイス Id の WDK オーディオ
- WDM オーディオ拡張 WDK、好みのデバイス Id
- デバイス Id の WDK オーディオ
- オーディオ デバイスを識別します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29f7414ea424b6e5245fb07c275111741719657b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355783"
---
# <a name="accessing-the-preferred-device-id"></a>推奨されるデバイス ID へのアクセス


## <span id="accessing_the_preferred_device_id"></span><span id="ACCESSING_THE_PREFERRED_DEVICE_ID"></span>


Windows 2000 以降、Windows のマルチ メディア機能と Windows Me で**waveInMessage**、 **waveOutMessage**、および**midiOutMessage**のデバイス ID を取得することができます、好みのデバイス。 これら 3 つの関数は、それぞれ wave 入力、wave 出力、および MIDI 出力では、好みのデバイス Id を取得します。 この情報は、アプリケーション プログラムが、たとえば、2 つまたは複数のデバイスの一覧から開くには、デバイスを選択するために役立ちます。 このようなアプリケーションは、通常、リスト内のデバイス間では、好みのデバイスを示す必要があります。

好みのデバイスは、マルチ メディアのコントロール パネルからユーザーが選択したデバイス mmsys.cpl します。 Windows のマルチ メディアまたは DirectSound アプリケーションを明示的を指定しない場合、デバイス、好みのデバイスは既定で選択されます。

アプリケーションを呼び出して、現在優先するオーディオ デバイスのデバイス ID を取得する、 *xxx * * * メッセージ** メッセージ パラメーターを定数に設定して関数[ **DRVM\_マッパー\_優先\_取得**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536362(v=vs.85))します。

呼び出すときに、 **waveInMessage**、 **waveOutMessage**、または**midiOutMessage** 、DRVM で関数を\_マッパー\_優先\_メッセージを取得、WAVE としてデバイス ハンドルの値を指定\_マッパー (の**waveInMessage**または**waveOutMessage**) または MIDI\_マッパー (の**midiOutMessage**)、この値を適切なハンドル型にキャストします。HWAVEIN、HWAVEOUT、または HMIDIOUT します。 *Xxx * * * メッセージ** 関数は、有効なデバイス ハンドルの代わりにこの値を受け付けるようにするデバイスを開くことがなくアプリケーションの既定のデバイス ID のクエリを実行できます。 詳細については、 *xxx * * * メッセージ** 関数を参照してください[System-Intercepted デバイス メッセージ](system-intercepted-device-messages.md)します。

DRVM\_マッパー\_優先\_(waveIn、waveOut、または midiOut) は、対象デバイス マッパーによって GET メッセージをインターセプトします。 マッパー wave および MIDI デバイスの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

 




