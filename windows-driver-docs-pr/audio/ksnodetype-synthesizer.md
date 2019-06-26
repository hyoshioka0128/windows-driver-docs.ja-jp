---
title: KSNODETYPE\_シンセサイザー
description: KSNODETYPE\_シンセサイザー
ms.assetid: ef5f5068-c312-4e14-905e-c815d6e9aac2
keywords:
- KSNODETYPE_SYNTHESIZER オーディオ デバイス
topic_type:
- apiref
api_name:
- KSNODETYPE_SYNTHESIZER
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6901d4a57865c3f073805affe790bb0a40ea769a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359009"
---
# <a name="ksnodetypesynthesizer"></a>KSNODETYPE\_シンセサイザー


## <span id="ddk_ksnodetype_synthesizer_ks"></span><span id="DDK_KSNODETYPE_SYNTHESIZER_KS"></span>


KSNODETYPE\_シンセサイザー ノードは、MIDI シンセサイザーを表します。 シンセサイザー ノード MIDI の入力ストリームとしては使用し、次のいずれかの出力します。

-   Wave ストリーム

-   アナログのオーディオ信号

-   生の MIDI

Microsoft Windows Driver Kit (WDK) でのドライバーの DMusUART オーディオ サンプルでは、生 MIDI に外部のシンセサイザーの出力を (その DirectMusic pin) のシンセサイザー ノードが含まれています、ミニポート ドライバーの例を示します。

シンセサイザー ノードには、次の必須プロパティをサポートする必要があります。

[**KSPROPERTY\_シンセサイザー\_キャップ**](https://docs.microsoft.com/previous-versions/ff537389(v=vs.85))

[**KSPROPERTY\_シンセサイザー\_PORTPARAMETERS**](https://docs.microsoft.com/previous-versions/ff537405(v=vs.85))

チャネルの複数のグループをサポートするシンセサイザー ノードには、次のプロパティもサポートする必要があります。

[**KSPROPERTY\_シンセサイザー\_CHANNELGROUPS**](https://docs.microsoft.com/previous-versions/ff537390(v=vs.85))

ノードがこのプロパティをサポートしていない場合は、チャネルのグループの数の既定値は 1 にします。

シンセサイザー ノードは、次のオプションもサポートできます[KSPROPSETID\_シンセサイザー](kspropsetid-synth.md)と[KSPROPSETID\_シンセサイザー\_Dls](kspropsetid-synth-dls.md)プロパティ。

[**KSPROPERTY\_シンセサイザー\_LATENCYCLOCK**](https://docs.microsoft.com/previous-versions/ff537402(v=vs.85))

[**KSPROPERTY\_シンセサイザー\_MASTERCLOCK**](https://docs.microsoft.com/previous-versions/ff537403(v=vs.85))

[**KSPROPERTY\_シンセサイザー\_RUNNINGSTATS**](https://docs.microsoft.com/previous-versions/ff537406(v=vs.85))

[**KSPROPERTY\_シンセサイザー\_VOICEPRIORITY**](https://docs.microsoft.com/previous-versions/ff537407(v=vs.85))

[**KSPROPERTY\_シンセサイザー\_ボリューム**](https://docs.microsoft.com/previous-versions/ff537409(v=vs.85))

[**KSPROPERTY\_シンセサイザー\_VOLUMEBOOST**](https://docs.microsoft.com/previous-versions/ff537410(v=vs.85))

[**KSPROPERTY\_シンセサイザー\_DLS\_追加**](https://docs.microsoft.com/previous-versions/ff537392(v=vs.85))

[**KSPROPERTY\_シンセサイザー\_DLS\_COMPACT**](https://docs.microsoft.com/previous-versions/ff537394(v=vs.85))

[**KSPROPERTY\_シンセサイザー\_DLS\_ダウンロード**](https://docs.microsoft.com/previous-versions/ff537396(v=vs.85))

[**KSPROPERTY\_シンセサイザー\_DLS\_アンロード**](https://docs.microsoft.com/previous-versions/ff537398(v=vs.85))

[**KSPROPERTY\_シンセサイザー\_DLS\_WAVEFORMAT**](https://docs.microsoft.com/previous-versions/ff537400(v=vs.85))

 

 





