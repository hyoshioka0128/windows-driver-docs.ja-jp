---
title: Wave と DirectSound コンポーネント
description: Wave と DirectSound コンポーネント
ms.assetid: df00fcaf-49b0-4af1-a12f-bd3fcb9e025d
keywords:
- wave コンポーネント WDK オーディオ
- wave ストリーム WDK オーディオ
- DirectSound WDK オーディオ、コンポーネント
- ユーザー モード コンポーネント WDK オーディオ
- カーネル モード コンポーネント WDK オーディオ
- wave WDK オーディオのレンダリング
- wave キャプチャ WDK オーディオ
- コンポーネントの WDK オーディオをレンダリングします。
- コンポーネントの WDK オーディオをキャプチャします。
- wave レンダリング アプリケーション WDK オーディオ
- wave キャプチャ アプリケーション WDK オーディオ
- wave アウト アプリケーション WDK オーディオ
- アプリケーションでは、wave WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2acbfc84da63ea183c31742ee8a0a3b108824356
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328510"
---
# <a name="wave-and-directsound-components"></a>Wave と DirectSound コンポーネント


## <span id="wave_and_directsound_components"></span><span id="WAVE_AND_DIRECTSOUND_COMPONENTS"></span>


アプリケーション プログラムは、(入力) をキャプチャし、(出力) wave ストリームを表示するユーザー モードとカーネル モードのコンポーネントの組み合わせに依存します。 Wave ストリームがデータ形式はデジタル オーディオ ストリーム、 [ **WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff538799)または[ **WAVEFORMATEXTENSIBLE** ](https://msdn.microsoft.com/library/windows/hardware/ff538802)構造体。

アプリケーションは、次のいずれかを使用できますの波のレンダリングやキャプチャ ソフトウェア インターフェイス。

-   Microsoft Windows のマルチ メディア waveOut*Xxx*と waveIn*Xxx*関数

-   DirectSound と DirectSoundCapture Api

WaveOut の動作*Xxx*と waveIn*Xxx*関数はレガシ wave ドライバーとデバイスの機能に基づいています。 Windows 98 以降、 [WDMAud システム ドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver) WDM オーディオ ドライバーをコマンドにこれらの関数の呼び出しを変換します。 古いバージョンのソフトウェアとハードウェア、waveOut の動作をエミュレートすることにより、*Xxx*関数犠牲に 3d のサウンド効果とハードウェアの高速化、DirectSound API から使用可能なようになりました。 DirectSound と Windows のマルチ メディア wave 関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

DirectSound と Windows のマルチ メディア wave 関数は、クライアントの[SysAudio システム ドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)wave と DirectSound ストリームを処理できるオーディオ フィルター グラフをビルドします。 グラフの構築は、これらのソフトウェアのインターフェイスを使用するアプリケーションに対して透過的です。

### <a name="span-idwavecomponentsspanspan-idwavecomponentsspanspan-idwavecomponentsspanwave-components"></a><span id="Wave_Components"></span><span id="wave_components"></span><span id="WAVE_COMPONENTS"></span>Wave コンポーネント

次の図は、wave アプリケーションはレンダリングまたは wave PCM データで構成されるデジタル オーディオ ストリームをキャプチャを使用してユーザー モードとカーネル モード コンポーネントを示しています。

![wave レンダリングとキャプチャのコンポーネントを示す図](images/wavecomp.png)

上記の図の左側にある表示コンポーネントが表示され、キャプチャ コンポーネントは、右側に表示されます。 これらは、ベンダーから提供されたコンポーネントであることを示すためには、wave ミニポート ドライバーを表すボックスが暗くなります。 他のコンポーネントの図には、システムが提供します。

左上の図、wave レンダリング (または「wave アウト」) のアプリケーション インターフェイスを通じて、waveOut WDM オーディオ ドライバーに*Xxx*関数、ユーザー モードで実装される[WinMM システム コンポーネント](user-mode-wdm-audio-components.md#winmm_system_component)、Winmm.dll します。 アプリケーションは、ファイルと呼び出しから wave のブロックにオーディオ サンプルを読み取り、 [ **waveOutWrite** ](https://msdn.microsoft.com/library/windows/desktop/dd743876)それらをレンダリングする関数。

ユーザー モードとカーネル モードの両方のコンポーネント (Wdmaud.drv と Wdmaud.sys) から成るの波形データをバッファーには、WDMAud、 [ **waveOutWrite** ](https://msdn.microsoft.com/library/windows/desktop/dd743876)呼び出しを wave のストリームを出力、 [KMixer システム ドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)WDMAud の下の図に表示されます。

KMixer は、wave PCM 1 つまたは複数のソースからストリームし、wave PCM 形式でも、単一出力ストリームを形成する合成を受信するシステム コンポーネントです。

KMixer は、wave ポートおよびミニポート ドライバーが前の図の左側にある KMixer 下に表示されます、WaveCyclic または WavePci デバイスにストリームを出力します。 ミニポート ドライバーでは、基になるオーディオのレンダリング デバイスを表す wave フィルターを形成するポート ドライバーに自体をバインドします。 一般的なレンダリング デバイスは、一連のスピーカーまたは外部のオーディオ ユニットを駆動するアナログ信号を出力します。 レンダリング デバイスには、S/PDIF コネクタ経由のデジタル オーディオ出力も可能性があります。 WaveCyclic と WavePci の詳細については、次を参照してください。 [Wave フィルター](wave-filters.md)します。

または、KMixer はによって制御される、USB オーディオ デバイスにその出力ストリームを渡すことができます、 [USBAudio クラスのシステム ドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver) (非表示の図)、WaveCyclic または WavePci デバイスではなく。

アダプタのドライバを呼び出して WaveCyclic または WavePci ポート ドライバーのインスタンスを作成します[ **PcNewPort** ](https://msdn.microsoft.com/library/windows/hardware/ff537715)の GUID 値を持つ**CLSID\_PortWaveCyclic**または**CLSID\_PortWavePci**、それぞれします。

上記の図の右側にあるは、波形データをファイルをキャプチャするアプリケーションをサポートするために必要なコンポーネントを示します。 "Wave in"は wave キャプチャ (または) のアプリケーションは、waveIn を通じて WDM オーディオ ドライバーと通信*Xxx*関数で、WinMM システム コンポーネントで実装されます。

図の右上隅にある wave キャプチャ デバイスは、wave ミニポートとポートのドライバーによって制御されます。 できますが、型 WaveCyclic または WavePci のポートおよびミニポート ドライバーは、フォーム キャプチャ デバイスを表す wave フィルターをまとめてバインドします。 通常、このデバイスは、マイクやその他の音源からアナログ信号をキャプチャし、wave PCM ストリームに変換します。 デバイスは、S/PDIF コネクタ経由のデジタル オーディオ ストリームの入力も可能性があります。

Wave ポート ドライバーでは、直接、wave ストリーム KMixer または WDMAud のいずれかを出力します。 ストリームは、サンプル速度 WDMAud が受信する前に変換する必要がある場合、KMixer を通過する必要があります。 図に示すように、同時にレンダリングとオーディオ ストリームのキャプチャを実行するシステムは KMixer、2 つのインスタンスを必要があります。 必要とされるため、SysAudio がそのこれらのインスタンスを自動的に作成されるに注意してください。

または、キャプチャされた wave ストリームのソースを WaveCyclic ではなく、USB オーディオ デバイスまたは WavePci デバイスを指定できます。 この場合、(の図に示されていません) USBAudio ドライバーは、ストリームを KMixer に渡します。

かどうかで USB デバイスまたは WaveCyclic または WavePci デバイスで wave ストリームをキャプチャしたらに関係なく KMixer は他のストリームとの混合は行われませんが、必要である場合、ストリームのサンプル レートの変換を実行します。 KMixer は、WDMAud システム ドライバーの半分 Wdmaud.sys、カーネル モードの結果として得られるストリームを出力します。 Wdmaud.drv が、waveIn によるアプリケーション プログラムを wave ストリームを出力する半分に、ユーザー モード*Xxx*関数で、Winmm.dll で実装されます。 最後に、図の上部にある、wave キャプチャ アプリケーション、wave データを書き込むファイル。

Wave キャプチャ アプリケーションの呼び出し時に、 [ **waveInOpen** ](https://msdn.microsoft.com/library/windows/desktop/dd743847)キャプチャ ストリームを開く関数をそのコールバック ルーチンへのポインターを渡します。 Wave キャプチャ イベントが発生したときに、オペレーティング システムは、キャプチャ デバイスから wave サンプルの次のブロックを格納するバッファーをコールバック ルーチンを呼び出します。 コールバックに応答してでは、アプリケーションは、ファイルに次のウェーブ データ ブロックを書き込みます。

### <a name="span-iddirectsoundcomponentsspanspan-iddirectsoundcomponentsspanspan-iddirectsoundcomponentsspandirectsound-components"></a><span id="DirectSound_Components"></span><span id="directsound_components"></span><span id="DIRECTSOUND_COMPONENTS"></span>DirectSound コンポーネント

次の図は、波形データをキャプチャを表示したり、DirectSound アプリケーション プログラムで使用されるユーザー モードとカーネル モード コンポーネントを示します。

![directsound レンダリングとキャプチャのコンポーネントを示す図](images/dscomp.png)

表示コンポーネントは、上記の図の左半分で表示され、キャプチャ コンポーネントが右側に表示します。 Wave ミニポート ドライバーは、コンポーネントのベンダーから提供されたことを示すために暗いボックスとして表示されます。 他のコンポーネントの図には、システムが提供します。

図の左上で、DirectSound アプリケーション負荷 wave データ ファイルからサウンドをバッファーするユーザー モード[DirectSound システム コンポーネント](user-mode-wdm-audio-components.md#directsound_system_component)(Dsound.dll) を管理します。 このコンポーネントは、図の左下に表示されるポートおよびミニポート ドライバーが、WaveCyclic または WavePci デバイスに wave ストリームを送信します。 デバイスのハードウェア ミキサー暗証番号 (pin) がある場合、ストリームは KMixer をバイパスして、wave ポート ドライバーに直接渡します。 それ以外の場合、ストリームは、KMixer で、他の再生中に同時にストリームと合成することを最初に通過します。 KMixer は、ポート ドライバーの混在のストリームを出力します。

としてする前に、ミニポート ドライバー自体にバインド ポート ドライバーは、基になるオーディオのレンダリング デバイスを表す wave フィルターを形成します。 このデバイスでは、たとえば、一連のスピーカー、ストリームを再生可能性があります。

または、wave ストリームは、WaveCyclic ではなく、USB オーディオ デバイスまたは WavePci デバイスで表示できます。 この場合、ストリームが KMixer; をバイパスできません。(図に示されていません) USBAudio クラスのシステム ドライバー KMixer ストリームを常に渡します。

上記の図の右側にあるは、DirectSoundCapture アプリケーションをサポートするコンポーネントを示しています。 WaveCyclic または WavePci キャプチャ デバイスからはアプリケーション レコード wave のデータを受信します。 このデバイスに変換しますアナログ信号、マイク、たとえば、wave ストリーム。 図の右上隅にあるデバイスの波のポートおよびミニポートのドライバーが表示されます。 図に示すようにポート ドライバーはミニポート ドライバーからの入力として、ストリームを受信し、Dsound.dll、ユーザー モード DirectSound コンポーネントに直接または間接的に KMixer を出力します。 これは、ハードウェア キャプチャ暗証番号 (pin) がキャプチャ デバイスから使用できるかどうかによって異なります。

または、キャプチャされた wave ストリームのソースでは、USB オーディオ デバイスを指定できます。 この場合、ストリームが KMixer; をバイパスできません。(図に示されていません) USBAudio ドライバー KMixer ストリームを常に渡します。

KMixer がキャプチャ ストリームのパスに挿入される場合は、必要な場合に、ストリームでサンプル レートの変換を実行しますが、他のストリームとの混合は行われません。

上記の図の右上隅にあるアプリケーションは DirectSoundCapture バッファーから wave データを読み取るし、ファイルに書き込みます。

 

 




