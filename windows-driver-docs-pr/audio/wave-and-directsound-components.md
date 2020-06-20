---
title: Wave と DirectSound コンポーネント
description: Wave と DirectSound コンポーネント
ms.assetid: df00fcaf-49b0-4af1-a12f-bd3fcb9e025d
keywords:
- wave コンポーネント WDK オーディオ
- wave ストリーム WDK オーディオ
- DirectSound WDK audio、コンポーネント
- ユーザーモードコンポーネント WDK オーディオ
- カーネルモードコンポーネント WDK オーディオ
- wave レンダリング WDK オーディオ
- WDK オーディオの wave キャプチャ
- コンポーネントのレンダリング WDK オーディオ
- コンポーネントのキャプチャ WDK オーディオ
- wave レンダリングアプリケーション WDK オーディオ
- アプリケーションの wave キャプチャの WDK オーディオ
- wave out アプリケーションの WDK オーディオ
- wave in アプリケーション WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccb8fed9d6ddd3404a5c21e7df10f25f801aa381
ms.sourcegitcommit: ea4043e93009835f115dce80909d5a039128464d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85102132"
---
# <a name="wave-and-directsound-components"></a>Wave と DirectSound コンポーネント


## <span id="wave_and_directsound_components"></span><span id="WAVE_AND_DIRECTSOUND_COMPONENTS"></span>


アプリケーションプログラムは、ユーザーモードとカーネルモードのコンポーネントを組み合わせて使用して、wave ストリームをキャプチャ (入力) およびレンダリング (出力) します。 Wave ストリームは、データ形式が[**WAVEFORMATEX**](https://docs.microsoft.com/windows/win32/api/mmeapi/ns-mmeapi-waveformatex)または[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)構造体で記述されているデジタルオーディオストリームです。

アプリケーションでは、次のいずれかのソフトウェアインターフェイスを使用して wave のレンダリングとキャプチャを行うことができます。

-   Microsoft Windows マルチメディア waveOut*Xxx*および waveIn*xxx*関数

-   DirectSound と DirectSoundCapture Api

WaveOut*xxx*関数と waveIn*xxx*関数の動作は、レガシ wave ドライバーとデバイスの機能に基づいています。 Windows 98 以降、 [WDMAud システムドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)は、これらの関数の呼び出しを、WDM オーディオドライバーへのコマンドに変換します。 ただし、以前のソフトウェアやハードウェアの動作をエミュレートすることにより、waveOut*Xxx*関数は、DirectSound API を介して使用できるようになった3-d サウンド効果とハードウェアアクセラレーションを犠牲にします。 DirectSound および Windows マルチメディア wave 関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

DirectSound および Windows マルチメディア wave 関数は、wave および DirectSound ストリームを処理するオーディオフィルターグラフを構築する[sysaudio システムドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)のクライアントです。 グラフの作成は、これらのソフトウェアインターフェイスを使用するアプリケーションに対して透過的です。

### <a name="span-idwave_componentsspanspan-idwave_componentsspanspan-idwave_componentsspanwave-components"></a><span id="Wave_Components"></span><span id="wave_components"></span><span id="WAVE_COMPONENTS"></span>Wave コンポーネント

次の図は、wave PCM データで構成されるデジタルオーディオストリームのレンダリングまたはキャプチャに wave アプリケーションで使用されるユーザーモードとカーネルモードのコンポーネントを示しています。

![wave レンダリングとキャプチャのコンポーネントを示す図](images/wavecomp.png)

前の図の左側にレンダリングコンポーネントが表示され、キャプチャコンポーネントが右側に表示されます。 Wave ミニポートドライバーを表すボックスは、ベンダーが提供するコンポーネントであることを示すために、暗くなっています。 図のその他のコンポーネントはシステムによって提供されます。

図の左上で、wave レンダリング (または "wave out") アプリケーションは、ユーザーモードの[winmm.dll システムコンポーネント](user-mode-wdm-audio-components.md#winmm_system_component)で実装されている waveOut*Xxx*関数を介して、WDM オーディオドライバーにインターフェイスします。これは、Winmm.dll です。 アプリケーションは、wave オーディオサンプルのブロックをファイルから読み取り、 [**waveOutWrite**](https://docs.microsoft.com/previous-versions/dd743876(v=vs.85))関数を呼び出してそれらを表示します。

WDMAud は、ユーザーモードとカーネルモードの両方のコンポーネント (Wdmaud と Wdmaud.sys) で構成され、 [**waveOutWrite**](https://docs.microsoft.com/previous-versions/dd743876(v=vs.85))呼び出しからのウェーブデータをバッファーに出力して、図の WDMAud の下にある[KMixer システムドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)に wave ストリームを出力します。

KMixer は、1つ以上のソースから wave PCM ストリームを受信し、それらを組み合わせて1つの出力ストリームを形成するシステムコンポーネントです。これは、wave PCM 形式でもあります。

KMixer は、WaveCyclic または WavePci デバイスに wave ストリームを出力します。このデバイスのポートとミニポートドライバーは、前の図の左側にある KMixer の下に表示されます。 ミニポートドライバー自体がポートドライバーにバインドされ、基になるオーディオレンダリングデバイスを表す wave フィルターが形成されます。 一般的なレンダリングデバイスは、一連のスピーカーまたは外部オーディオユニットを駆動するアナログ信号を出力します。 レンダリングデバイスは、S/PDIF コネクタを使用してデジタルオーディオを出力する場合もあります。 WaveCyclic と WavePci の詳細については、「 [Wave Filters](wave-filters.md)」を参照してください。

また、KMixer は、WaveCyclic または WavePci デバイスではなく、 [usbaudio クラスシステムドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver) (図には示されていません) によって制御される USB オーディオデバイスに出力ストリームを渡すことができます。

アダプタドライバは、WaveCyclic または WavePci port ドライバのインスタンスを作成します。これは、それぞれ GUID 値が**clsid \_ PortWaveCyclic**または**Clsid \_ PortWavePci**の[**pcnewport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)を呼び出すことによって行います。

上の図の右側には、wave データをファイルにキャプチャするアプリケーションをサポートするために必要なコンポーネントが示されています。 Wave キャプチャ (または "wave in") アプリケーションは、Winmm.dll システムコンポーネントに実装されている waveIn*Xxx*関数を介して、WDM オーディオドライバーと通信します。

図の右下隅にある wave キャプチャデバイスは、wave ミニポートとポートドライバーによって制御されます。 WaveCyclic または WavePci の種類のポートとミニポートドライバーを結合して、キャプチャデバイスを表す wave フィルターを形成します。 通常、このデバイスはマイクまたはその他のオーディオソースからアナログ信号をキャプチャし、wave PCM ストリームに変換します。 デバイスは、S/PDIF コネクタを介してデジタルオーディオストリームを入力する場合もあります。

Wave ポートドライバーは、wave ストリームを KMixer または WDMAud に直接出力します。 ストリームは KMixer を通過する必要がある場合は、WDMAud が受信する前にサンプリングレートで変換する必要があります。 オーディオストリームのレンダリングとキャプチャを同時に実行するシステムでは、図に示すように、KMixer の2つのインスタンスが必要になる場合があります。 必要に応じて、SysAudio によってこれらのインスタンスが自動的に作成されることに注意してください。

また、キャプチャした wave ストリームのソースは、WaveCyclic または WavePci デバイスではなく、USB オーディオデバイスにすることもできます。 この場合、USBAudio ドライバー (図には示されていません) は、ストリームを KMixer に渡します。

Wave ストリームが USB デバイスによってキャプチャされるか、または WaveCyclic または WavePci デバイスによってキャプチャされるかにかかわらず、KMixer は必要に応じてストリームでサンプルレート変換を実行しますが、他のストリームとは混合しません。 KMixer は、結果として得られるストリームを、WDMAud システムドライバーのカーネルモードの半分である Wdmaud.sys に出力します。 ユーザーモードの半分 (Wdmaud) は、Winmm.dll で実装されている waveIn*Xxx*関数を使用して、wave ストリームをアプリケーションプログラムに出力します。 最後に、図の上部にある wave キャプチャアプリケーションは、wave データをファイルに書き込みます。

Wave キャプチャアプリケーションは、キャプチャストリームを開くために[**waveInOpen**](https://docs.microsoft.com/previous-versions/dd743847(v=vs.85))関数を呼び出した時点で、コールバックルーチンへのポインターを渡します。 Wave キャプチャイベントが発生すると、オペレーティングシステムは、キャプチャデバイスからの次のウェーブサンプルブロックを含むバッファーを使用してコールバックルーチンを呼び出します。 アプリケーションは、コールバックに応答して、次のウェーブデータブロックをファイルに書き込みます。

### <a name="span-iddirectsound_componentsspanspan-iddirectsound_componentsspanspan-iddirectsound_componentsspandirectsound-components"></a><span id="DirectSound_Components"></span><span id="directsound_components"></span><span id="DIRECTSOUND_COMPONENTS"></span>DirectSound コンポーネント

次の図は、wave データを表示またはキャプチャする DirectSound アプリケーションプログラムによって使用されるユーザーモードとカーネルモードのコンポーネントを示しています。

![directsound のレンダリングとキャプチャのコンポーネントを示す図](images/dscomp.png)

レンダリングコンポーネントは、前の図の左半分に表示され、キャプチャコンポーネントは右側に表示されます。 Wave ミニポートドライバーは、ベンダーが提供するコンポーネントであることを示すために、暗いボックスとして表示されます。 図のその他のコンポーネントはシステムによって提供されます。

図の左上にある DirectSound アプリケーションは、ユーザーモードの[directsound システムコンポーネント](user-mode-wdm-audio-components.md#directsound_system_component)(Dsound.dll) が管理するサウンドバッファーに、ファイルから wave データを読み込みます。 このコンポーネントは、WaveCyclic または WavePci デバイスに wave ストリームを送信します。このデバイスは、ポートとミニポートドライバーが図の左下に表示されます。 デバイスでハードウェアミキサーピンが使用可能な場合、ストリームは KMixer をバイパスして、wave ポートドライバーに直接渡されます。 それ以外の場合、ストリームは最初に KMixer をパススルーし、その他の同時再生ストリームとミキシングします。 KMixer は、混合ストリームをポートドライバーに出力します。

以前と同様に、ミニポートドライバー自体がポートドライバーにバインドされ、基になるオーディオレンダリングデバイスを表す wave フィルターが形成されます。 このデバイスは、たとえば、一連のスピーカーでストリームを再生する場合があります。

また、WaveCyclic または WavePci デバイスではなく、USB オーディオデバイスで wave ストリームをレンダリングすることもできます。 この場合、ストリームは KMixer をバイパスできません。USBAudio クラスシステムドライバー (図には示されていません) は、常にストリームを KMixer に渡します。

前の図の右側は、DirectSoundCapture アプリケーションをサポートするコンポーネントを示しています。 アプリケーションは、WaveCyclic または WavePci キャプチャデバイスから受信する wave データを記録します。 このデバイスは、たとえばマイクからのアナログ信号を wave ストリームに変換します。 デバイスの wave ポートとミニポートドライバーは、図の右下隅に表示されます。 図に示すように、ポートドライバーはミニポートドライバーからストリームを入力として受信し、ユーザーモードの DirectSound コンポーネント、Dsound.dll、または KMixer 経由で間接的に出力します。 これは、キャプチャデバイスからハードウェアキャプチャピンが使用可能かどうかによって異なります。

または、キャプチャした wave ストリームのソースを USB オーディオデバイスにすることもできます。 この場合、ストリームは KMixer をバイパスできません。USBAudio ドライバー (図には示されていません) は、常にストリームを KMixer に渡します。

KMixer がキャプチャストリームのパスに挿入されると、必要に応じてストリームでサンプルレート変換が実行されますが、他のストリームとの混合は行われません。

上の図の右上隅にあるアプリケーションは、DirectSoundCapture バッファーから wave データを読み取り、ファイルに書き込みます。

 

 




