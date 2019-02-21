---
title: PCM 以外のサポートの背景
description: PCM 以外のサポートの背景
ms.assetid: 4f0e1101-e4cc-4bde-a178-fb47fe24ae4d
keywords:
- 非 PCM オーディオの形式、WDK DirectSound
- 非 PCM オーディオ形式 WDK、waveOut
- waveOut PCM 非サポート WDK オーディオ
- DirectSound WDK オーディオ、PCM 非サポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e90b2b801c998e7bae90e4c438766ba88b39b2b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561001"
---
# <a name="background-of-non-pcm-support"></a>PCM 以外のサポートの背景


## <span id="background_of_non_pcm_support"></span><span id="BACKGROUND_OF_NON_PCM_SUPPORT"></span>


いくつかの問題では、Microsoft Windows の以前のバージョンが waveOut と DirectSound Api を介して非 PCM 形式をサポートできなくなります。 これらの問題と解決された方法を以下に示します。

### <a name="span-idwaveoutapispanspan-idwaveoutapispanspan-idwaveoutapispanwaveout-api"></a><span id="waveOut_API"></span><span id="waveout_api"></span><span id="WAVEOUT_API"></span>waveOut API

VxD wave ドライバーから waveOut アプリケーションを分離するソフトウェア層は比較的薄いです。 ドライバーとカスタム wave 形式をサポートするアプリケーションは、オペレーティング システムは、形式を解釈するかどうかに関係なく、その形式でデータをストリーミングできます。

ただし、Windows 2000 および Windows 98 では、WDM オーディオ framework 強制的に通過する waveOut API (および DirectShow の waveOut レンダラー) で処理されるすべてのオーディオ データ、 [KMixer システム ドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver) (Kmixer.sys)、これは、カーネルのオーディオ ミキサーします。 KMixer にドライバーが、形式をサポートするかどうかに関係なく、形式がサポートしている場合にのみ、waveOutOpen 呼び出しが成功します。

KMixer 処理 WAVE\_形式\_WDM のすべてのオペレーティング システムで PCM。 Windows 2000 以降と Windows 98 SE、拡張だけでなく WAVE をサポートするために KMixer\_形式\_IEEE\_も FLOAT [ **WAVEFORMATEXTENSIBLE** ](https://msdn.microsoft.com/library/windows/hardware/ff538802)のバリエーションPCM、IEEE 浮動小数点形式。 PCM 以外の形式をサポートしている KMixer はありません、ために非 PCM KMixer を使用してデータを渡そうとは失敗します。

Windows XP 以降では、および Windows Me、単に KMixer をバイパスするオーディオ データを非 PCM を許可することで PCM 以外の形式をサポートします。 具体的には、PortCls (または USBAudio) 直接には、最初 KMixer 経由ではなく waveOut PCM 以外のデータが送られます。 PCM 以外のデータが混在するは、ハードウェア、ac-3 または WMA Pro などの形式で PCM 以外のデータを使用して通常は必要ありません混在させることと、ドライバーは通常ハードウェアはその形式での混在をサポートしてアプリケーションで行う必要があります。

### <a name="span-iddirectsoundapispanspan-iddirectsoundapispanspan-iddirectsoundapispandirectsound-api"></a><span id="DirectSound_API"></span><span id="directsound_api"></span><span id="DIRECTSOUND_API"></span>DirectSound API

レガシ waveOut および VxD ドライバー、DirectSound サポート[ **WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff538799) (がない WAVEFORMATEXTENSIBLE) PCM が 1 つのサンプルでは、あたり 8 または 16 ビットで、プライマリとセカンダリの両方のバッファー形式または2 つのチャネルと 100 Hz と 100 kHz のサンプリング レート。 VxD ドライバーが DSSCL に協調レベルが設定されている場合は、プライマリ バッファーの許可されている形式をさらに制限\_WRITEPRIMARY (の説明を参照して、 **IDirectSoundBuffer::SetFormat** DirectX SDK のメソッド)。 Windows XP または Windows Me では、これらの制限は変更されていません。

WDM ドライバーでは、WAVEFORMATEX と WAVEFORMATEXTENSIBLE の両方の形式で、PCM の形式をサポートできます。 Windows 2000 以降、Windows Me では、および Windows 98 SE、ドライバー、WAVE にもサポートできます\_形式\_IEEE\_FLOAT 形式のプライマリとセカンダリの両方の DSBCAPS\_両方で LOCSOFTWARE バッファー (KMixer で混在)WAVEFORMATEX WAVEFORMATEXTENSIBLE 形式。

呼び出す**SetFormat**プライマリ バッファーの形式が、サウンド カードが選択した最終的な混合形式に間接的な影響のみを持つデータを指定します。 プライマリ バッファー オブジェクトの使用を取得、 **IDirectSound3DListener**インターフェイスし、デバイスのグローバル ボリューム、パンを設定するには、単一の出力からのストリームを表しますが、サウンド カードです。 KMixer がいくつか DSSCL を許可するにはプライマリ バッファーのデータを合成する代わりに、\_WRITEPRIMARY DirectSound クライアントに同時に実行します。

Windows 2000 および Windows 98 では、DirectSound は、PCM のデータのみをサポートします。 (同じ、directshow、DirectSound のレンダラーを使用する場合は true)。呼び出し**CreateSoundBuffer**非 pcm により形式常に失敗すると、ドライバーには、形式がサポートしている場合でもです。 2 つの理由、エラーが発生します。 最初に、DirectSound は、KS 暗証番号 (pin) を作成するたびに自動的に指定 KSDATAFORMAT\_サブタイプ\_PCM からのサブタイプではなく、 **wFormatTag**ある WAVEFORMATEX 構造体のメンバー作成するために使用、 **IDirectSoundBuffer**オブジェクト。 第 2 に、DirectSound がすべてのデータ パスのボリュームと SRC (サンプル レートの変換) ノードを用意する必要があります ([**KSNODETYPE\_ボリューム**](https://msdn.microsoft.com/library/windows/hardware/ff537208)と[ **KSNODETYPE\_SRC**](https://msdn.microsoft.com/library/windows/hardware/ff537190)) クライアントが、DirectSound のバッファーでのパン、ボリューム、または頻度のコントロールを要求するかどうかに関係なく、します。 データ KMixer を通過するか、デバイス ハードウェアの混在を実行する場合、この要件は満たされます。 ただし、非 PCM 形式の場合、KMixer が、データ パスに存在しないと、ドライバー自体が失敗するは通常ハードウェアの混在を実行するように求められたら。

Windows XP 以降では、および Windows Me、DirectSound PCM 以外の形式を使用してアプリケーションを禁止する制限を削除します。 DirectSound 8 (およびそれ以降のバージョン) は、正しい形式のサブタイプを使用し、ボリュームとすべてのデータ パス内の SRC ノードを自動的に行われなくが必要です。

 

 




