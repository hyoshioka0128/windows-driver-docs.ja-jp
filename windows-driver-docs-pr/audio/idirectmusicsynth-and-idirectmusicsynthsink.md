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
ms.openlocfilehash: e2043c16e2122b9607499bf21e29b48c272614e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553327"
---
# <a name="idirectmusicsynth-and-idirectmusicsynthsink"></a>IDirectMusicSynth と IDirectMusicSynthSink


## <span id="idirectmusicsynth_and_idirectmusicsynthsink"></span><span id="IDIRECTMUSICSYNTH_AND_IDIRECTMUSICSYNTHSINK"></span>


」の説明に従って[シンセサイザーと Wave シンク](synthesizers-and-wave-sinks.md)カスタム ソフトウェア シンセサイザーを実装する、または wave シンク ユーザー モードで実行していると DirectMusic と通信します。 シンセサイザー オブジェクトには、 [IDirectMusicSynth](https://msdn.microsoft.com/library/windows/hardware/ff536519)インターフェイス。 Wave シンク オブジェクトには、 [IDirectMusicSynthSink](https://msdn.microsoft.com/library/windows/hardware/ff536520)インターフェイス。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536529" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Activate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536529)"><strong>IDirectMusicSynth::Activate</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>チャネル</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536534" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetChannelPriority&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536534)"><strong>IDirectMusicSynth::GetChannelPriority</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536542" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::SetChannelPriority&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536542)"><strong>IDirectMusicSynth::SetChannelPriority</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Instruments</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536532" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Download&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536532)"><strong>IDirectMusicSynth::Download</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536546" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Unload&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536546)"><strong>IDirectMusicSynth::Unload</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>情報</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536533" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetAppend&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536533)"><strong>IDirectMusicSynth::GetAppend</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536535" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetFormat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536535)"><strong>IDirectMusicSynth::GetFormat</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536536" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetLatencyClock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536536)"><strong>IDirectMusicSynth::GetLatencyClock</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536537" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetPortCaps&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536537)"><strong>IDirectMusicSynth::GetPortCaps</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536538" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetRunningStats&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536538)"><strong>IDirectMusicSynth::GetRunningStats</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>再生</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536540" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::PlayBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536540)"><strong>IDirectMusicSynth::PlayBuffer</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536541" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Render&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536541)"><strong>IDirectMusicSynth::Render</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ポート</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536539" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Open&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536539)"><strong>IDirectMusicSynth::Open</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536531" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Close&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536531)"><strong>IDirectMusicSynth::Close</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536544" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::SetNumChannelGroups&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536544)"><strong>IDirectMusicSynth::SetNumChannelGroups</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>その他のパラメーター</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536543" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::SetMasterClock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536543)"><strong>IDirectMusicSynth::SetMasterClock</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536545" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::SetSynthSink&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536545)"><strong>IDirectMusicSynth::SetSynthSink</strong></a></p></td>
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536521" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::Activate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536521)"><strong>IDirectMusicSynthSink::Activate</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536522" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::GetDesiredBufferSize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536522)"><strong>IDirectMusicSynthSink::GetDesiredBufferSize</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536524" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::Init&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536524)"><strong>IDirectMusicSynthSink::Init</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536527" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::SetDirectSound&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536527)"><strong>IDirectMusicSynthSink::SetDirectSound</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>タイミング</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536523" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::GetLatencyClock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536523)"><strong>IDirectMusicSynthSink::GetLatencyClock</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536525" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::RefTimeToSample&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536525)"><strong>IDirectMusicSynthSink::RefTimeToSample</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536526" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::SampleToRefTime&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536526)"><strong>IDirectMusicSynthSink::SampleToRefTime</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536528" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::SetMasterClock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536528)"><strong>IDirectMusicSynthSink::SetMasterClock</strong></a></p></td>
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

シンセサイザーのソフトウェアを最初に開いたとき DirectMusic は、シンセサイザー、DMU\_サンプル レートとオーディオ出力ストリームのチャネルの数を指定する PORTPARAMS 構造 (Microsoft Windows SDK のドキュメントで説明)。 シンセサイザーこれらの標準に変換し、 [ **WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff538799) wave シンクの呼び出し時に、wave シンクに渡される構造体、 **IDirectMusicSynth::GetFormat**メソッド。

詳細については、の説明を参照してください、 **IDirectMusic**と**IDirectMusicPort** Windows SDK のドキュメント内のインターフェイス。

 

 




