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
ms.openlocfilehash: 3de630d5da533fa661c0b927b3c00535cf8424bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551410"
---
# <a name="ksnodetypesynthesizer"></a>KSNODETYPE\_シンセサイザー


## <span id="ddk_ksnodetype_synthesizer_ks"></span><span id="DDK_KSNODETYPE_SYNTHESIZER_KS"></span>


KSNODETYPE\_シンセサイザー ノードは、MIDI シンセサイザーを表します。 シンセサイザー ノード MIDI の入力ストリームとしては使用し、次のいずれかの出力します。

-   Wave ストリーム

-   アナログのオーディオ信号

-   生の MIDI

Microsoft Windows Driver Kit (WDK) でのドライバーの DMusUART オーディオ サンプルでは、生 MIDI に外部のシンセサイザーの出力を (その DirectMusic pin) のシンセサイザー ノードが含まれています、ミニポート ドライバーの例を示します。

シンセサイザー ノードには、次の必須プロパティをサポートする必要があります。

[**KSPROPERTY\_シンセサイザー\_キャップ**](https://msdn.microsoft.com/library/windows/hardware/ff537389)

[**KSPROPERTY\_シンセサイザー\_PORTPARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff537405)

チャネルの複数のグループをサポートするシンセサイザー ノードには、次のプロパティもサポートする必要があります。

[**KSPROPERTY\_シンセサイザー\_CHANNELGROUPS**](https://msdn.microsoft.com/library/windows/hardware/ff537390)

ノードがこのプロパティをサポートしていない場合は、チャネルのグループの数の既定値は 1 にします。

シンセサイザー ノードは、次のオプションもサポートできます[KSPROPSETID\_シンセサイザー](kspropsetid-synth.md)と[KSPROPSETID\_シンセサイザー\_Dls](kspropsetid-synth-dls.md)プロパティ。

[**KSPROPERTY\_シンセサイザー\_LATENCYCLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff537402)

[**KSPROPERTY\_シンセサイザー\_MASTERCLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff537403)

[**KSPROPERTY\_シンセサイザー\_RUNNINGSTATS**](https://msdn.microsoft.com/library/windows/hardware/ff537406)

[**KSPROPERTY\_シンセサイザー\_VOICEPRIORITY**](https://msdn.microsoft.com/library/windows/hardware/ff537407)

[**KSPROPERTY\_シンセサイザー\_ボリューム**](https://msdn.microsoft.com/library/windows/hardware/ff537409)

[**KSPROPERTY\_シンセサイザー\_VOLUMEBOOST**](https://msdn.microsoft.com/library/windows/hardware/ff537410)

[**KSPROPERTY\_シンセサイザー\_DLS\_追加**](https://msdn.microsoft.com/library/windows/hardware/ff537392)

[**KSPROPERTY\_シンセサイザー\_DLS\_COMPACT**](https://msdn.microsoft.com/library/windows/hardware/ff537394)

[**KSPROPERTY\_シンセサイザー\_DLS\_ダウンロード**](https://msdn.microsoft.com/library/windows/hardware/ff537396)

[**KSPROPERTY\_シンセサイザー\_DLS\_アンロード**](https://msdn.microsoft.com/library/windows/hardware/ff537398)

[**KSPROPERTY\_シンセサイザー\_DLS\_WAVEFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff537400)

 

 





