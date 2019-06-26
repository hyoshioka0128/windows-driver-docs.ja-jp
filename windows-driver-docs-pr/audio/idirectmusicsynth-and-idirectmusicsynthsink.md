---
title: IDirectMusicSynth と IDirectMusicSynthSink
description: IDirectMusicSynth と IDirectMusicSynthSink
ms.assetid: ce9a353b-9e4b-402b-92bb-948200e3c2ef
keywords:
- IDirectMusicSynth インターフェイス
- IDirectMusicSynthSink インターフェイス
- ユーザー モードの WDK オーディオでは、カスタム レンダリング インターフェイスします。
- ユーザー モード シンセサイザー WDK のオーディオ、インターフェイス
- カスタム wave シンク WDK オーディオ
- wave シンク WDK オーディオ、ユーザー モード
- WDK オーディオ、シンセサイザーの待機時間
- マスターの WDK オーディオ、シンセサイザーをクロックします。
- WDK のオーディオ、シンセサイザーをクロックします。
- シンセサイザー WDK のオーディオ、インターフェイス
- カスタムのシンセサイザー WDK のオーディオ、インターフェイス
- DirectMusic カスタム レンダリング WDK のオーディオ、シンセサイザー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6473e987c649664bd8f1c29de1fdd4e19ebf43d7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359954"
---
# <a name="idirectmusicsynth-and-idirectmusicsynthsink"></a>IDirectMusicSynth と IDirectMusicSynthSink


## <span id="idirectmusicsynth_and_idirectmusicsynthsink"></span><span id="IDIRECTMUSICSYNTH_AND_IDIRECTMUSICSYNTHSINK"></span>


」の説明に従って[シンセサイザーと Wave シンク](synthesizers-and-wave-sinks.md)カスタム ソフトウェア シンセサイザーを実装する、または wave シンク ユーザー モードで実行していると DirectMusic と通信します。 シンセサイザー オブジェクトには、 [IDirectMusicSynth](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynth)インターフェイス。 Wave シンク オブジェクトには、 [IDirectMusicSynthSink](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynthsink)インターフェイス。

DirectMusic を通じてシンセサイザー ソフトウェアと通信してその**IDirectMusicSynth**インターフェイス。 DirectMusic は、DirectX 6.1 以降は、このインターフェイスをサポートしています。 **IDirectMusicSynth**メソッドの機能グループに編成は、次の表に示されているメソッドをサポートしています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">グループ</th>
<th align="left">メソッド名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ライセンス認証</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-activate" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Activate&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-activate)"><strong>IDirectMusicSynth::Activate</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>チャネル</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getchannelpriority" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetChannelPriority&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getchannelpriority)"><strong>IDirectMusicSynth::GetChannelPriority</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setchannelpriority" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::SetChannelPriority&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setchannelpriority)"><strong>IDirectMusicSynth::SetChannelPriority</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Instruments</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-download" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Download&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-download)"><strong>IDirectMusicSynth::Download</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-unload" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Unload&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-unload)"><strong>IDirectMusicSynth::Unload</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>情報</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getappend" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetAppend&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getappend)"><strong>IDirectMusicSynth::GetAppend</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getformat" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetFormat&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getformat)"><strong>IDirectMusicSynth::GetFormat</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getlatencyclock" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetLatencyClock&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getlatencyclock)"><strong>IDirectMusicSynth::GetLatencyClock</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getportcaps" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetPortCaps&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getportcaps)"><strong>IDirectMusicSynth::GetPortCaps</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getrunningstats" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetRunningStats&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getrunningstats)"><strong>IDirectMusicSynth::GetRunningStats</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>再生</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-playbuffer" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::PlayBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-playbuffer)"><strong>IDirectMusicSynth::PlayBuffer</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-render" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Render&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-render)"><strong>IDirectMusicSynth::Render</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ポート</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-open" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Open&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-open)"><strong>IDirectMusicSynth::Open</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-close" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Close&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-close)"><strong>IDirectMusicSynth::Close</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setnumchannelgroups" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::SetNumChannelGroups&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setnumchannelgroups)"><strong>IDirectMusicSynth::SetNumChannelGroups</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>その他のパラメーター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setmasterclock" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::SetMasterClock&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setmasterclock)"><strong>IDirectMusicSynth::SetMasterClock</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setsynthsink" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::SetSynthSink&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setsynthsink)"><strong>IDirectMusicSynth::SetSynthSink</strong></a></p></td>
</tr>
</tbody>
</table>

 

ほとんどのアプリケーションは、メソッドを呼び出す必要はありません、 **IDirectMusicSynth**インターフェイスを直接; DirectMusic ポートは、通常、シンセサイザーを管理します。 ただし、アプリケーションの開発およびテスト中にシンセサイザーに直接インターフェイスことができます。

シンセサイザーがせず、オブジェクトとして表される wave シンクへの接続を完了していない、 **IDirectMusicSynthSink**インターフェイス。 Wave シンク シンセサイザーのオーディオ出力ストリームを DirectSound、DirectShow、または Windows のマルチ メディアなど、オーディオのレンダリング モジュールに接続する**waveOut** API。

DirectMusic は既定では、その内部で使用**IDirectMusicSynthSink**シンセサイザー ソフトウェアによって生成される wave データを処理する実装。 この wave シンクは、DirectSound にデータをフィードします。

Wave シンクの最初に作成し、呼び出しにシンセサイザーに接続されている、シンセサイザーをアクティブ化する前に**IDirectMusicSynth::SetSynthSink**します。 これは、ため、シンセサイザーの作成後に非常に最初の呼び出しがありますなど、タイミングに関係の呼び出しの多く**IDirectMusicSynth::GetLatencyClock**と**IDirectMusicSynth::SetMasterClock**、実際に渡されます等価な呼び出し**IDirectMusicSynthSink**します。

DirectX 6.1 と DirectX 7 サポートとカスタムのユーザー モード wave シンクの実装のみを**IDirectMusicSynthSink**インターフェイス。 **IDirectMusicSynthSink**メソッドの機能グループに編成は、次の表に示されているメソッドをサポートしています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">グループ</th>
<th align="left">メソッド名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>初期化</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-activate" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::Activate&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-activate)"><strong>IDirectMusicSynthSink::Activate</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-getdesiredbuffersize" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::GetDesiredBufferSize&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-getdesiredbuffersize)"><strong>IDirectMusicSynthSink::GetDesiredBufferSize</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-init" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::Init&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-init)"><strong>IDirectMusicSynthSink::Init</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-setdirectsound" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::SetDirectSound&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-setdirectsound)"><strong>IDirectMusicSynthSink::SetDirectSound</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>タイミング</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-getlatencyclock" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::GetLatencyClock&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-getlatencyclock)"><strong>IDirectMusicSynthSink::GetLatencyClock</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-reftimetosample" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::RefTimeToSample&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-reftimetosample)"><strong>IDirectMusicSynthSink::RefTimeToSample</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-sampletoreftime" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::SampleToRefTime&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-sampletoreftime)"><strong>IDirectMusicSynthSink::SampleToRefTime</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-setmasterclock" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::SetMasterClock&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-setmasterclock)"><strong>IDirectMusicSynthSink::SetMasterClock</strong></a></p></td>
</tr>
</tbody>
</table>

 

DirectX 8 以降では、DirectMusic は常にユーザー モード シンセサイザーとその内部 wave シンクを使用します。 以降のバージョンの DirectMusic はのカスタム実装をサポートしていません**IDirectMusicSynthSink**します。

DirectX 6.1 と DirectX 7 では、ただしは、独自に実装するために無料**IDirectMusicSynthSink**オブジェクトを使用して、希望どおりのシンセサイザーのオーディオ出力ストリームを管理します。 たとえば、DirectShow に wave データをフィードする可能性がありますまたは**waveOut** API。 Wave ストリーム オブジェクトを作成する場合があります、 **IDirectMusicSynthSink**にプラグインのインターフェイス、 **IDirectMusicSynth**オブジェクト。

Wave ストリームを管理するには、だけでなく、wave シンクはシンセサイザーのタイミングを制御する責任を負います。 Wave シンクへの呼び出しによって、マスターのクロックを受信する**IDirectMusicSynth::SetMasterClock**、に対するのと同じ呼び出しで時刻のマスター ソースを渡す**IDirectMusicSynthSink::SetMasterClock**します。 マスターのクロックは、wave ストリームとして同じ crystal から生成されていない、ため wave シンクをクロックのずれを補正することによって同期に保持する必要があります。

シンセサイザーの追跡できる時間適切に、ようにさらに、バックアップ時間をサンプリングするマスターのクロック時間から変換する 2 つの呼び出しを提供します。

-   **IDirectMusicSynthSink::RefTimeToSample**

-   **IDirectMusicSynthSink::SampleToRefTime**

Wave シンクでは、サンプルを取得への呼び出しによって書き込まれる時間を実際に管理するため、待機時間の時計が生成されます**IDirectMusicSynth::Render**します。 DirectMusic を呼び出すと**IDirectMusicSynth::GetLatencyClock** DirectMusic ポートでは、単に立ち止まって振り返るし呼び出します**IDirectMusicSynthSink::GetLatencyClock**します。

シンセサイザーのソフトウェアを最初に開いたとき DirectMusic は、シンセサイザー、DMU\_サンプル レートとオーディオ出力ストリームのチャネルの数を指定する PORTPARAMS 構造 (Microsoft Windows SDK のドキュメントで説明)。 シンセサイザーこれらの標準に変換し、 [ **WAVEFORMATEX** ](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex) wave シンクの呼び出し時に、wave シンクに渡される構造体、 **IDirectMusicSynth::GetFormat**メソッド。

詳細については、の説明を参照してください、 **IDirectMusic**と**IDirectMusicPort** Windows SDK のドキュメント内のインターフェイス。

 

 




