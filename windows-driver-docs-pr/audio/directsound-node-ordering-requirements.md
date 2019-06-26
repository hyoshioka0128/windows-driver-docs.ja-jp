---
title: DirectSound のノードの順序付け要件
description: DirectSound のノードの順序付け要件
ms.assetid: baca55f5-c669-4bd2-82b5-3985030864f2
keywords:
- ハードウェア アクセラレータ WDK DirectSound、ノードの順序の要件
- WDK DirectSound ノード順序要件
- ノードがチェーン WDK DirectSound
- WDK DirectSound のノードを合計します。
- オーディオの WDK ミキシング 3D
- WDK のオーディオを混在させる 2D
- 3D 処理のソフトウェア エミュレーション WDK オーディオ
- supermixer ノード WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e719fd4a0a8e033b43db3f29233b074ea5195056
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360135"
---
# <a name="directsound-node-ordering-requirements"></a>DirectSound のノードの順序付け要件


## <span id="directsound_node_ordering_requirements"></span><span id="DIRECTSOUND_NODE_ORDERING_REQUIREMENTS"></span>


DirectSound 2D または 3D のミキサーの暗証番号 (pin) は、次の一連のノードを含むノードのチェーンが必要があります。

-   [ボリューム] ノード (を参照してください[ **KSNODETYPE\_ボリューム**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume))。

-   3D のノード (このノードは省略可能です。 参照してください[ **KSNODETYPE\_3D\_効果**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-3d-effects))。

-   Supermixer ノード (を参照してください[ **KSNODETYPE\_SUPERMIX**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-supermix))。

-   [ボリューム] ノード (の効果をパン)

-   SRC ノード (を参照してください[ **KSNODETYPE\_SRC**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-src))。

-   ノードの合計 (を参照してください[ **KSNODETYPE\_合計**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-sum))。

この一覧内のノードは、暗証番号 (pin) へのストリーミング データによって発生した順序で表示されます。 上記の順序が維持されることに、問題を発生させることがなくこれらのノード間では、他のノードをインタリーブできます。

2D の pin には、前のリストでは、省略可能な 3D のノードを除くすべてのノードが必要です。 3D の pin には、3 D のノードを含め、リスト内のすべてのノードが必要です。

SRC (サンプル レートの変換) ノードの合計ノード前にする必要があります。 Src 属性と合計のノードは、これは必須ではありませんが、通常、隣接するセルです。 **IDirectSoundBuffer::SetFrequency**メソッド (Microsoft Windows SDK のドキュメントを参照してください) 悪影響を与える場合、SRC ノードの再サンプリング レート。

Src 属性と合計のノードのみを含むミキサーは SWMidi Redbook などのシステム ドライバーによって管理されているストリームを混在させる場合のための十分な (を参照してください[SWMidi システム ドライバー](kernel-mode-wdm-audio-components.md#swmidi_system_driver)と[Redbook システム ドライバー](kernel-mode-wdm-audio-components.md#redbook_system_driver)) が、DirectSound は、さらに、ボリュームの 2 つのノードと supermixer ノードの合計ノードの前にする必要があります。 DirectSound は、ボリュームの変更の結果を送信**IDirectSoundBuffer::SetVolume**最初の [ボリューム] ノードとパンの効果をから送信する呼び出し**IDirectSoundBuffer::SetPan** 2 つ目の呼び出し[ボリューム] ノード。

DirectSound を使用して 2D の pin に 3D 効果を生成することができます、**とる**、 **SetPan**、および**SetFrequency**呼び出しボリュームと SRC ノードを制御します。

-   **とる**呼び出しはリスナーから音源の距離内の変更をシミュレートできます。

-   **SetPan**呼び出しは、基準、リスナーと音源の向きの変更をシミュレートできます。

-   **SetFrequency**ドップラー効果と HRTFs (頭部伝達関数) の呼び出しをシミュレートできます。

Supermixer ノードは、M 入力チャネルに接続する N 出力チャネル、N が、デバイスの最終的な出力ストリーム内のチャネルの数と等しくなりますクロスバー行列です。

ハードウェア アクセラレータを使用した 3D 効果を管理する、省略可能な 3D のノードが必要です (を参照してください[WDM オーディオでは 3D DirectSound アクセラレーションをサポートしている](supporting-3d-directsound-acceleration-in-wdm-audio.md))、3 D 処理のソフトウェアは必要ありませんが。 SRC ノードの前に、およびボリュームの最初のノードと、supermixer ノード間の 3D のノードを配置するほとんどの既存の実装が、その他の構成が可能です。

通常、3 D のノードに入力ストリームには、1 つのチャネルが含まれています。 DirectSound 8.0 以降では、mono PCM バッファーのみを 3D 効果を作成できます。 以前のバージョン、DirectSound が、mono とステレオの両方の入力ストリームと 3D のノードをサポートし、ドライバーは、古いアプリケーションとの互換性を確保する両方をサポートする必要があります。

 

 




