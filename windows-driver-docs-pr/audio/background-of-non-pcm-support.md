---
title: PCM 以外のサポートの背景
description: PCM 以外のサポートの背景
ms.assetid: 4f0e1101-e4cc-4bde-a178-fb47fe24ae4d
keywords:
- PCM 以外のオーディオ形式 WDK、DirectSound
- PCM 以外のオーディオ形式 WDK、waveOut
- waveOut 以外の PCM が WDK オーディオをサポートする
- DirectSound WDK audio、PCM 以外のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69e3060ebb5dd22ae80003d6c9723458f565555f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831274"
---
# <a name="background-of-non-pcm-support"></a>PCM 以外のサポートの背景


## <span id="background_of_non_pcm_support"></span><span id="BACKGROUND_OF_NON_PCM_SUPPORT"></span>


いくつかの問題により、以前のバージョンの Microsoft Windows では、waveOut および DirectSound Api を使用して PCM 以外の形式をサポートできませんでした。 これらの問題とその解決方法については、以下で説明します。

### <a name="span-idwaveout_apispanspan-idwaveout_apispanspan-idwaveout_apispanwaveout-api"></a><span id="waveOut_API"></span><span id="waveout_api"></span><span id="WAVEOUT_API"></span>waveOut API

WaveOut アプリケーションを VxD wave ドライバーから分離するソフトウェアレイヤーは、かなり薄くなっています。 カスタムの wave 形式をサポートするドライバーとアプリケーションは、オペレーティングシステムが形式を認識しているかどうかに関係なく、その形式のデータをストリーミングできます。

ただし、Windows 2000 および Windows 98 では、WDM オーディオフレームワークによって、waveOut API (および DirectShow の waveOut レンダラー) によって処理されるすべてのオーディオデータが、カーネルオーディオミキサーである[KMixer システムドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver) (KMixer) を通過するように強制されます。 WaveOutOpen の呼び出しは、ドライバーが形式をサポートしているかどうかに関係なく、KMixer が形式をサポートしている場合にのみ成功します。

KMixer は、すべての WDM オペレーティングシステム上の WAVE\_形式\_PCM を処理します。 Windows 2000 以降および Windows 98 SE では、KMixer を拡張して、IEEE\_FLOAT\_の WAVE\_形式だけでなく、PCM と IEEE-float 形式[**のバリアントも**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)サポートします。 KMixer は PCM 以外の形式をサポートしていないため、KMixer を介して PCM 以外のデータを渡そうとしても失敗します。

Windows XP 以降、および Windows Me では、pcm 以外のオーディオデータが単に KMixer をバイパスできるようにすることで、PCM 以外の形式をサポートしています。 具体的には、waveOut 以外の PCM データは、最初に KMixer を通過するのではなく、直接 PortCls (または USBAudio) に送られます。 PCM 以外のデータの混在はハードウェアで行う必要がありますが、AC-3 や WMA Pro などの形式で PCM データ以外のデータを使用するアプリケーションは、通常、混在させる必要がありません。また、ドライバーは通常、その形式でのハードウェアの混在をサポートしていません。

### <a name="span-iddirectsound_apispanspan-iddirectsound_apispanspan-iddirectsound_apispandirectsound-api"></a><span id="DirectSound_API"></span><span id="directsound_api"></span><span id="DIRECTSOUND_API"></span>DirectSound API

レガシ waveOut ドライバーおよび VxD ドライバーでは、DirectSound はプライマリバッファーとセカンダリバッファーの両方に対して[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex) (WAVEFORMATEXTENSIBLE ではなく) PCM 形式をサポートしています。サンプルあたり8ビットまたは16ビット、1つまたは2つのチャネル、および 100 Hz と 100 kHz のサンプリングレートがあります. VxD ドライバーは、協調的レベルが DSSCL\_WRITEPRIMARY に設定されている場合に、プライマリバッファーに許可される形式をさらに制限できます (DirectX SDK の**Idirectsoundbuffer:: SetFormat**メソッドの説明を参照してください)。 これらの制限は、Windows Me または Windows XP では変更されていません。

WDM ドライバーでは、WAVEFORMATEX と WAVEFORMATEXTENSIBLE の両方の形式で PCM 形式をサポートできます。 Windows 2000 以降、Windows Me、および Windows 98 SE の場合、ドライバーは、WAVEFORMATEX と KMixer の両方で、プライマリとセカンダリの両方の DSBCAPS\_LOCSOFTWARE buffer (mixed by) の両方について、IEEE\_FLOAT 形式の WAVE\_\_形式をサポートすることもできます。WAVEFORMATEXTENSIBLE フォーム。

プライマリバッファーのデータ形式を指定するために**Setformat**を呼び出すと、サウンドカードによって選択された最終混合形式に間接的に影響します。 プライマリバッファーオブジェクトは、 **IDirectSound3DListener**インターフェイスを取得し、デバイスのグローバルボリュームとパンを設定するために使用されますが、サウンドカードからの1つの出力ストリームを表しているわけではありません。 代わりに、KMixer は、複数の DSSCL\_WRITEPRIMARY DirectSound クライアントを同時に実行できるようにするために、プライマリバッファーデータをミックスします。

Windows 2000 および Windows 98 では、DirectSound は PCM データのみをサポートしています。 (これは、DirectSound のレンダラーを使用する DirectShow にも当てはまります)。PCM 形式以外の**CreateSoundBuffer**への呼び出しは、ドライバーが形式をサポートしている場合でも、常に失敗します。 エラーは、次の2つの理由で発生します。 まず、DirectSound によって KS ピンが作成されるたびに、KSDATAFORMAT\_サブタイプ\_PCM が自動的に指定されます。これは、WAVEFORMATEX 構造体の**wFormatTag**メンバーからサブタイプを派生するのではなく、 **IDirectSoundBuffer**オブジェクト。 2つ目の方法では、クライアントがパン、ボリューム、または頻度のコントロールを要求しているかどうかに関係なく、ボリュームおよび SRC (サンプルレートの変換) ノード ([**KSNODETYPE\_volume**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)と[**KSNODETYPE\_src**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-src)) を持つすべてのデータパスが必要です。DirectSound バッファー。 この要件は、データが KMixer を通過するか、デバイスがハードウェアミックスを実行する場合に満たされます。 ただし、PCM 以外の形式の場合、KMixer はデータパスには存在せず、ドライバー自体は通常、ハードウェアミックスの実行を求められたときに失敗します。

Windows XP 以降および Windows Me では、DirectSound アプリケーションが PCM 以外の形式を使用できないようにする制限を削除します。 DirectSound 8 (およびそれ以降のバージョン) では正しい形式のサブタイプが使用され、すべてのデータパスにボリュームおよび SRC ノードが自動的に要求されることはなくなりました。

 

 




