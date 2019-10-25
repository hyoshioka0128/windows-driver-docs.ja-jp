---
title: DSSPEAKER_SURROUND スピーカー構成
description: DSSPEAKER_SURROUND スピーカー構成
ms.assetid: de8f861b-f190-4915-b3f0-95d39965b612
keywords:
- DSSPEAKER_SURROUND スピーカーの構成 WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51594299afbd6dfb932e938903f38864e136957b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833409"
---
# <a name="dsspeaker_surround-speaker-configuration"></a>DSSPEAKER\_サラウンドスピーカー構成


## <span id="dsspeaker_surround_speaker_configuration"></span><span id="DSSPEAKER_SURROUND_SPEAKER_CONFIGURATION"></span>


この情報は、Windows XP およびそれ以前のオペレーティングシステムに適用**さ  ます**。 Windows Vista 以降では、 **Idirectsound:: GetSpeakerConfig**と**Idirectsound:: SetSpeakerConfig**は非推奨とされました。

 

アプリケーションプログラムでは、スピーカー構成パラメーターを DSSPEAKER\_サラウンドに設定して**Idirectsound:: SetSpeakerConfig**メソッドを呼び出すことにより、DirectSound スピーカー構成をサラウンドモードに変更できます。 これにより、チャンネルが左、右、中央、およびバックスピーカーにマップされる4チャネル PCM 形式が指定されます。

これが有効になると、DSSPEAKER\_サラウンドスピーカー構成設定がグローバルになり、オーディオデバイス全体に影響します。 その後に実行されるすべてのオーディオアプリケーションは、DirectSound によって設定が再度変更されるまで、新しい設定の対象になります。

DirectSound では、次のアルゴリズムを使用してサラウンドモード用にオーディオシステムを構成します。

1.  DirectSound は最初に、ドライバーの DAC ノード (DAC ノードがない場合は3D ノード) に[**Ksk プロパティ\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-channel-config)送信することによって、ドライバーがサラウンドスピーカーモードに入るように要求します。 (「 [**KSNODETYPE\_DAC**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-dac) and [**KSNODETYPE\_3d\_効果**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-3d-effects)」を参照してください)。このプロパティ要求に付随する[**Ksk audio\_CHANNEL\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_channel_config)構造体では、ksk オーディオ\_スピーカー\_サラウンドスピーカー構成を指定します。 要求が成功した場合、オーディオデバイスは4つのチャネルを、左右のスピーカーに直接接続されている4つのアナログ出力にルーティングします。

2.  これが失敗した場合、DirectSound は、デバイスをステレオスピーカーモードで構成し、 [**KSNODETYPE\_PROLOGIC\_ENCODER**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-prologic-encoder)ノード (ある場合) を有効にするようにドライバーに要求します。 これが成功した場合、デバイスは、アプリケーションからの4チャネルストリームを、デジタルまたはアナログの形式で出力するサラウンドエンコードされたステレオ信号に変換します。 (ハードウェアは、デバイスのさまざまなミキサーピンに流れるストリームをミキシングした後にエンコーディングを行う必要があります)。ユーザーは、デバイスのステレオ出力を外部デコーダーに接続して、エンコードされた信号を左、右、中央、およびバックスピーカーに出力する4つのチャネルに変換することができます。

3.  これが失敗した場合、DirectSound では KMixer の KSNODETYPE\_PROLOGIC\_ENCODER ノードが有効になります。 (デバイスは、前の手順で既にステレオモードになっています)。ここでも、デバイスによって出力されるステレオ信号を外部デコーダーに渡すことができます。

このアルゴリズムが成功した場合、アプリケーションは4つのチャネルの PCM バッファーを作成し、再生できます。 上記の1と2では、デバイスが読み取るハードウェアバッファーが4つのチャネルを使用しますが、ケース3の場合、ハードウェアバッファーはステレオ形式を使用します。 アプリケーションは、1と2のようにハードウェアバッファーに直接書き込むことができますが、場合によっては、3の場合は、ソフトウェアバッファーに書き込む必要があります。また、KMixer がアプリケーションの4チャネルストリームを、ハードウェアバッファーに必要なサラウンドエンコードステレオ形式に変換できるようにします。

上記の場合 (3)、アプリケーションは出力ストリームにハードウェアバッファーを使用しないようにする必要があります。 KMixer は、ミックスをエンコードしてサラウンドステレオストリームを生成する前に、すべての入力ストリームをミックスすることに注意してください。 ただし、ハードウェアミキサーピンを入力するすべてのストリームは、KMixer のエンコードされたステレオを持つハードウェアに混在しています。これにより、デコードされたサラウンドオーディオの品質が低下します。 アプリケーションでは、ソフトウェアバッファーのみを使用してこれを防ぐことができます。

KSNODETYPE\_PROLOGIC\_ENCODER ノードによってサラウンドエンコードされたステレオストリームは、 [**KSNODETYPE\_prologic\_デコーダ**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-prologic-decoder)ノードによって4つのチャネル (左、右、中央、および背面) にデコードできます。

 

 




