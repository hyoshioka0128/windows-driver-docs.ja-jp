---
title: DSSPEAKER_SURROUND スピーカーの構成
description: DSSPEAKER_SURROUND スピーカーの構成
ms.assetid: de8f861b-f190-4915-b3f0-95d39965b612
keywords:
- DSSPEAKER_SURROUND スピーカー構成 WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0859387180b6abd258c5a61b4fad154c84c584ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557230"
---
# <a name="dsspeakersurround-speaker-configuration"></a>DSSPEAKER\_サラウンド スピーカーの構成


## <span id="dsspeaker_surround_speaker_configuration"></span><span id="DSSPEAKER_SURROUND_SPEAKER_CONFIGURATION"></span>


**注**  この情報は、Windows XP およびそれ以前のオペレーティング システムに適用されます。 以降、Windows Vista で**IDirectSound::GetSpeakerConfig**と**IDirectSound::SetSpeakerConfig**非推奨とされました。

 

アプリケーション プログラムは DirectSound スピーカーの構成を呼び出すことによってサラウンド モードを変更できます、 **IDirectSound::SetSpeakerConfig** DSSPEAKER にスピーカー構成パラメーターを持つメソッドが設定\_ブロックの挿入します。 これには、左、右、センター、およびスピーカーをバックアップに、チャネルがマップされる 4 チャネル PCM 形式を指定します。

有効、DSSPEAKER と\_サラウンド スピーカー構成設定はグローバルとオーディオ デバイス全体に影響を与えます。 以降を実行しているすべてのオーディオ アプリケーションは、DirectSound の設定が変更されるまで、新しい設定の対象がもう一度です。

DirectSound は、ブロックの挿入モードのオーディオ システムを構成するのに、次のアルゴリズムを使用します。

1.  DirectSound は最初に、サラウンド スピーカー モードに移動して、送信することで、ドライバー、 [ **KSPROPERTY\_オーディオ\_チャネル\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff537250)への要求のプロパティの設定、ドライバーの DAC のノード (または 3D ノード DAC のノードが存在しない場合)。 (を参照してください[ **KSNODETYPE\_DAC** ](https://msdn.microsoft.com/library/windows/hardware/ff537158)と[ **KSNODETYPE\_3D\_効果**](https://msdn.microsoft.com/library/windows/hardware/ff537148))。[ **KSAUDIO\_チャネル\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff537083)このプロパティの要求に付属している構造体の指定、KSAUDIO\_スピーカー\_ブロックの挿入スピーカーの構成。 要求が成功すると、オーディオ デバイスは、次の 4 つアナログ出力に直接接続されている左、右、センター、およびスピーカーをバックアップする 4 つのチャンネルをルーティングします。

2.  失敗したかどうか、DirectSound は、ドライバーを求めるステレオのスピーカー モードでデバイスの構成を有効にするその[ **KSNODETYPE\_PROLOGIC\_エンコーダー** ](https://msdn.microsoft.com/library/windows/hardware/ff537187)ノードである場合。 これが成功すると、デバイスはサラウンドでエンコードされたステレオ信号がアナログまたはデジタルのいずれかの形式で出力がアプリケーションから 4 チャネル ストリームを変換します。 (ハードウェア行う必要があります、デバイスのさまざまなミキサー ピンに入れられるストリームを混在させる後エンコードします。)ユーザーは、外部のデコーダーを 4 つのチャネルに出力されるエンコードされたシグナル left、right に変換しますが、中央し、スピーカーのバックアップに、デバイスのステレオの出力を接続できます。

3.  DirectSound により、KSNODETYPE、失敗した場合、\_PROLOGIC\_KMixer エンコーダー ノード。 (デバイスは既に、前の手順からステレオ モードで) です。ここでも、デバイスから出力されるステレオの信号は、外部のデコーダーを取り込むことができます。

このアルゴリズムが成功すると、アプリケーションは作成し、4 チャネル PCM バッファーを再生できます。 1 と 2 が上記の場合から、デバイスを読み取りハードウェア バッファーを使用して、4 つのチャンネルがハードウェアのバッファーを 3 の場合に、ステレオの形式を使用しています。 アプリケーションが 1 と 2 の場合、ハードウェアのバッファーに直接書き込むことができますが、場合 3 ソフトウェアに書き込むことが必要がありますバッファー ハードウェア バッファーに必要なサラウンドでエンコードされたステレオ形式にアプリケーションの 4 つのチャネルのストリームを変換する KMixer を許可します。

上記の場合 (3) で、出力ストリームのいずれかのハードウェアのバッファーを使用して、アプリケーションを避ける必要があります。 KMixer がサラウンド ステレオ ストリームを生成するために、ミックスをエンコードする前に、すべての入力ストリームを混合することに注意してください。 ただし、ハードウェア ミキサー pin を入力するすべてのストリームはエンコードされたステレオのハードウェアで KMixer、デコード時にブロックの挿入のオーディオの品質の低下から混合します。 アプリケーションは、ソフトウェア バッファーのみを使用してこれを防ぐことができます。

によって、KSNODETYPE サラウンド エンコードされたステレオ ストリーム\_PROLOGIC\_で (左、右、センター、およびバックアップ) の 4 つのチャンネルにエンコーダーのノードをデコードできます、 [ **KSNODETYPE\_PROLOGIC\_デコーダー** ](https://msdn.microsoft.com/library/windows/hardware/ff537185)ノード。

 

 




