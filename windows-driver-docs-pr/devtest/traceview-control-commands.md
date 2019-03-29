---
title: TraceView の制御コマンド
description: Traceview でコントロールのコマンドを使用すると、トレース セッションを管理できます。
ms.assetid: 3ebfb728-7ca7-473d-b4bb-a62d1704aed6
keywords:
- Traceview でコントロールは、ドライバーの開発ツールをコマンドします。
topic_type:
- apiref
api_name:
- TraceView Control Commands
api_type:
- NA
ms.date: 12/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 13aea23c888d1fa5b0802861affe5fe2a07b01ec
ms.sourcegitcommit: 132f0c2d827982b808053ecd3b4d137a2883cca1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "56582851"
---
# <a name="traceview-control-commands"></a>TraceView の制御コマンド

> [!NOTE]
> Traceview でコマンド ライン オプションは非推奨とされます。 Tracepdb.exe と tracefmt.exe TMF ファイルおよび解析の .etl ファイルをテキストに Pdb に解析を使用して respectively.content

Traceview でコントロールのコマンドを使用すると、トレース セッションを開始およびセッションの停止を有効にしてプロバイダーを無効にすると、トレース セッションのプロパティの更新やトレース バッファーのフラッシュなどを管理できます。

```command
    traceview {-start | -stop | -update | -enable | -disable | -flush | -q} SessionName [Parameters]
```

```command
    traceview {-enumguid | -l | -h | -x}
```

## <a name="command-parameters"></a>コマンドのパラメーター

### <a name="actions"></a>Actions

|操作|説明|
|----|----|
|**-開始**|指定されたトレース セッションを開始します。|
|**-stop**|指定されたトレース セッションを停止します。|
|**-更新**|指定されたトレース セッションのプロパティを更新します。|
|**-有効にします。**|プロバイダーは、指定されたトレース セッション向けにできます。|
|**-を無効にします。**|指定したセッションのプロバイダーを無効にします。|
|**-フラッシュ**|指定されたトレース セッションのアクティブなバッファーをフラッシュします。 強制的な書き込みこれは、バッファーがいっぱいになったとき、およびトレース セッションを停止するときに発生する自動フラッシュです。|
|**-q**|指定されたトレース セッションの状態を照会します。|
|**-enumguid**|システム上のプロバイダーを一覧表示[登録](registered-provider.md)を Event Tracing for Windows (ETW)。|
|**-l**|コンピューターで実行されているすべてのトレース セッションの一覧を表示します。|
|**-x**|すべてのトレース セッションを停止します。|

### <a name="span-idparametersspanspan-idparametersspanparameters"></a><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター

<span id="_______SessionName______"></span><span id="_______sessionname______"></span><span id="_______SESSIONNAME______"></span> *SessionName*   
使用すると **-開始**、 *SessionName*トレース セッションを表すために選択した名前を指定します。 その他のすべてのコマンドを*SessionName*トレース セッションを識別します。

<span id="_______-f___LogFile_"></span><span id="_______-f___logfile_"></span><span id="_______-F___LOGFILE_"></span> **-f** \[*LogFile*\]  
使用すると **-開始**、 **-f**トレース ログ セッションを開始します。 *ログ ファイル*イベント トレース ログ (.etl) ファイルのファイル名とパス (省略可能) を指定します。 既定値は c:\\LogFile.etl します。

使用すると **-更新**、 **-f**のみを指定したすべての新しいトレース メッセージを送信[トレース ログ](trace-log.md)します。 このパラメーターを使用して、リアルタイムのトレース セッションをトレース ログのセッションに変換するか、既存のトレース ログ セッションの新しいトレース ログを開始します。 リアルタイムのトレース コンシューマーへとトレース ログにトレース メッセージを送信するには、両方を使用、 **-rt**と **-f**内のパラメーター、 **-更新**コマンド。

<span id="_______-rt______"></span><span id="_______-RT______"></span> **-rt**   
使用すると **-開始**、 **-rt**リアルタイム トレース セッションを開始 (トレース ログ セッション (**-f**) 既定値です)。使用する場合 **-rt**と **-f**で、 **-開始**コマンド、およびイベント トレース ログ ファイルにトレース コンシューマーにトレース メッセージが送信されます。

使用すると **-更新**、 **-rt**トレースのログ セッションをリアルタイムでのメッセージ配信を追加します。 すべての新しいトレース メッセージは、他に、(リアルタイム トレース セッションの場合) のようにトレース コンシューマーに直接送信されます、[トレース ログ](trace-log.md)します。

<span id="_______-guid___GUID___GUIDFile_"></span><span id="_______-guid___guid___guidfile_"></span><span id="_______-GUID___GUID___GUIDFILE_"></span> **-guid** {**\#**<em>GUID</em> | *GUIDFile*}  
1 つまたは複数のトレース プロバイダーを指定します。 使用して **-開始**トレース セッションのプロバイダーを有効にします。 使用して **-有効にする**プロバイダーを有効にする、または変更する、 **-フラグ**または **-レベル**値。 使用して **-を無効にする**を無効にするプロバイダーを指定します。

*GUID*いずれかを指定できます[コントロール GUID](control-guid.md) (先頭に番号記号 (**\#**)) パス (省略可能) や、コントロールの GUID (.ctl) ファイルなどのテキスト ファイルのファイル名をコントロール 1 つまたは複数のトレース プロバイダーの Guid にはが含まれています。

省略した場合、 **- guid**からパラメーターを **-開始**コマンド、traceview で開始、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)します。

Traceview では、次のサブパラ メーターの値を指定したプロバイダーに渡します。

<table>
<thead>
<tr>
<th>パラメーター</th>
<th>説明</th>
</tr>
<tbody>
<tr>
<td><em>SessionName</em></td>
<td>使用すると<strong>-開始</strong>、 <em>SessionName</em>トレース セッションを表すために選択した名前を指定します。 その他のすべてのコマンドを<em>SessionName</em>トレース セッションを識別します。</td>
</tr>
<tr>
<td><strong>-f</strong> \[<em>LogFile</em>\]</td>
<td><p>使用すると<strong>-開始</strong>、 <strong>-f</strong>トレース ログ セッションを開始します。 <em>ログ ファイル</em>イベント トレース ログ (.etl) ファイルのファイル名とパス (省略可能) を指定します。 既定値は c:\\LogFile.etl します。</p>
<p>使用すると<strong>-更新</strong>、 <strong>-f</strong>のみを指定したすべての新しいトレース メッセージを送信[トレース ログ](trace-log.md)します。 このパラメーターを使用して、リアルタイムのトレース セッションをトレース ログのセッションに変換するか、既存のトレース ログ セッションの新しいトレース ログを開始します。 リアルタイムのトレース コンシューマーへとトレース ログにトレース メッセージを送信するには、両方を使用、 <strong>-rt</strong>と<strong>-f</strong>内のパラメーター、 <strong>-更新</strong>コマンド。</p>
</td>
</tr>
<tr>
<td><strong>-rt</strong></td>
<td><p>使用すると<strong>-開始</strong>、 <strong>-rt</strong>リアルタイム トレース セッションを開始 (トレース ログ セッション (<strong>-f</strong>) 既定値です)。使用する場合<strong>-rt</strong>と<strong>-f</strong>で、 <strong>-開始</strong>コマンド、およびイベント トレース ログ ファイルにトレース コンシューマーにトレース メッセージが送信されます。</p>
<p>使用すると<strong>-更新</strong>、 <strong>-rt</strong>トレースのログ セッションをリアルタイムでのメッセージ配信を追加します。 すべての新しいトレース メッセージは、他に、(リアルタイム トレース セッションの場合) のようにトレース コンシューマーに直接送信されます、[トレース ログ](trace-log.md)します。</p>
</td>
</tr>
<tr>
<td><strong>-guid</strong> {<strong>\#</strong><em>GUID</em> | <em>GUIDFile</em>}</td>
<td><p>1 つまたは複数のトレース プロバイダーを指定します。 使用して<strong>-開始</strong>トレース セッションのプロバイダーを有効にします。 使用して<strong>-有効にする</strong>プロバイダーを有効にする、または変更する、 <strong>-フラグ</strong>または<strong>-レベル</strong>値。 使用して<strong>-を無効にする</strong>を無効にするプロバイダーを指定します。</p>
<p><em>GUID</em>いずれかを指定できます[コントロール GUID](control-guid.md) (先頭に番号記号 (<strong>\#</strong>)) パス (省略可能) や、コントロールの GUID (.ctl) ファイルなどのテキスト ファイルのファイル名をコントロール 1 つまたは複数のトレース プロバイダーの Guid にはが含まれています。</p>
<p>省略した場合、 <strong>- guid</strong>からパラメーターを<strong>-開始</strong>コマンド、traceview で開始、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)します。</p>
</td>
</tr>
</tbody>
</table>

Traceview では、次のサブパラ メーターの値が指定されたプロバイダーに渡します。

<table>
<thead>
<tr>
<th>-Guid のサブパラ メーター</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr>
<td><p><strong>-フラグ</strong><em>フラグ</em></p></td>

<span id="_______-b_______BufferSize______"></span><span id="_______-b_______buffersize______"></span><span id="_______-B_______BUFFERSIZE______"></span> **-b** *BufferSize*   
サポート技術情報、トレース セッションに割り当てられた各バッファーのサイズを指定します。 のみ使用して **-開始**します。

既定値は、プロセッサ、物理メモリの量と使用のオペレーティング システムの数によって決まります。

<span id="_______-min_______NumberOfBuffers______"></span><span id="_______-min_______numberofbuffers______"></span><span id="_______-MIN_______NUMBEROFBUFFERS______"></span> **最小** *NumberOfBuffers*   
トレース メッセージを格納するために最初に割り当てられたバッファーの数を指定します。 のみ使用して **-開始**します。

既定値は、プロセッサ、物理メモリの量と使用のオペレーティング システムの数によって決まります。

<span id="_______-max_______NumberOfBuffers______"></span><span id="_______-max_______numberofbuffers______"></span><span id="_______-MAX_______NUMBEROFBUFFERS______"></span> **-max** *NumberOfBuffers*   
使用すると **-開始**、 **-最大**トレース セッションに割り当てられたバッファーの最大数を指定します。 既定値は、プロセッサ、物理メモリの量と使用のオペレーティング システムの数によって決まります。

使用すると **-更新**、 **-最大**トレース セッションに割り当てられたバッファーの最大数を変更します。

<span id="_______-ft_______FlushTime______"></span><span id="_______-ft_______flushtime______"></span><span id="_______-FT_______FLUSHTIME______"></span> **-ft** *FlushTime*   
使用すると **-開始**、 **-ft** 、どのくらいの頻度 (秒単位)、トレース メッセージ バッファーがフラッシュされるを指定します。 使用すると **-更新**、 **-ft**フラッシュ時刻を指定した時間に変更します。

フラッシュ時間の最小値は、1 秒です。 既定値は 0 (フラッシュを強制しないです)。

強制的な書き込みこれはトレース セッションを停止すると、トレース メッセージのバッファーがいっぱいのときに自動的に行われるフラッシュです。

参照してください: **-フラッシュ**します。

<span id="_______-paged______"></span><span id="_______-PAGED______"></span> **-paged**   
トレースのメッセージ バッファーのページング可能なメモリを使用します。 既定では、イベントのトレースは、バッファーの非ページ メモリを使用します。 のみ使用して **-開始**します。

プロバイダーがディスパッチより大きい IRQL でトレース メッセージを生成するドライバーの場合に、このパラメーターを使用しない\_レベル。

このパラメーターは、Windows 2000 ではサポートされていません。

<span id="_______-seq_______MaxFileSize______"></span><span id="_______-seq_______maxfilesize______"></span><span id="_______-SEQ_______MAXFILESIZE______"></span> **-seq** *MaxFileSize*   
イベント トレース ログ (.etl) ファイルに (ファイルの終わりに、イベントの記録の停止) の連続したログ記録を指定します。 のみ使用して **-開始**します。

*MaxFileSize*ファイルの最大サイズを mb 単位で指定します。 なし、 *MaxFileSize*値、このパラメーターは無視されます。

シーケンシャルなログ記録は、既定では、ですが、このパラメーターを使用するには、ファイルの最大サイズを設定するかを使用して **- prealloc**します。 このパラメーターがない場合は、ファイル サイズの上限はありません。

<span id="_______-cir_______MaxFileSize______"></span><span id="_______-cir_______maxfilesize______"></span><span id="_______-CIR_______MAXFILESIZE______"></span> **-cir** *MaxFileSize*   
循環ログ (最も古いメッセージ経由で新しいメッセージをファイルの終わりのレコード) で、イベント トレース ログ (.etl) ファイルを指定します。 のみ使用して **-開始**します。

*MaxFileSize*ファイルの最大サイズを mb 単位で指定します。 なし、 *MaxFileSize*値、このパラメーターは無視されます。

既定値はシーケンシャル ファイルのサイズ制限なしでログに記録します。

<span id="_______-prealloc______"></span><span id="_______-PREALLOC______"></span> **-prealloc**   
割り当てる前に、イベント トレース ログ (.etl) ファイルの領域を予約します。 のみ使用して **-開始**します。

このパラメーターが必要です **-seq**または **-cir**で*MaxFileSize*します。 無効な **- newfile**します。

<p><em>フラグ</em>10 進数または 16 進数形式で、トレース プロバイダーで定義されているフラグの値を表します。 既定値は 0 です。 0xFF000000 を通じて 0x01000000 からの値は、将来使用するために予約されています。</p>

<p>フラグの意味は、各トレース プロバイダーによって個別に定義されます。 通常、フラグは、しだいに詳細レポートのレベルを表します。</p>

<p><strong>-開始</strong>コマンド、フラグの値が、トレース セッションですべてのトレース プロバイダーに適用されます。 トレース プロバイダーごとにさまざまなフラグを設定する個別を使用して、 <strong>-有効にする</strong>トレース プロバイダーごとにコマンド。</p>
</td>
</tr>

<tr>
<td>
<p><strong>-レベル</strong><em>レベル</em></p>
</td>
<td>
<p>指定します、<a href="trace-level.md" data-raw-source="[trace level](trace-level.md)">トレース レベル</a>トレース セッションでプロバイダー。 レベルは、トレース プロバイダーが生成されるイベントを決定します。</p>

<p><em>レベル</em>レベルの 10 進数または 16 進数形式で値を表します。 既定値は 0 です。</p>

<p>レベル値の意味は、各トレース プロバイダーによって個別に定義されます。 通常、トレース レベルは、(情報、警告、またはエラー)、イベントの重大度を表します。</p>

<p><strong>-開始</strong>コマンド、レベルの値は、トレース セッションで、すべてのトレース プロバイダーに適用されます。 トレース プロバイダーごとにさまざまなレベルを設定するには、個別を使用<strong>-有効にする</strong>トレース プロバイダーごとにコマンド。</p>
</td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>パラメーター</tr>
<tr>説明</tr>
</thead>
<tbody>
<tr>
<td><strong>-b</strong> <em>BufferSize</em></td>
<td>サポート技術情報、トレース セッションに割り当てられた各バッファーのサイズを指定します。 のみ使用して<strong>-開始</strong>します。
<p>既定値は、プロセッサ、物理メモリの量と使用のオペレーティング システムの数によって決まります。</p></td>
</tr>
<tr>
<td><strong>最小</strong> <em>NumberOfBuffers</em></td>
<td>トレース メッセージを格納するために最初に割り当てられたバッファーの数を指定します。 のみ使用して<strong>-開始</strong>します。
<p>既定値は、プロセッサ、物理メモリの量と使用のオペレーティング システムの数によって決まります。</p></td>
</tr>
<tr>
<td><strong>-max</strong> <em>NumberOfBuffers</em></td>
<td>使用すると<strong>-開始</strong>、 <strong>-最大</strong>トレース セッションに割り当てられたバッファーの最大数を指定します。 既定値は、プロセッサ、物理メモリの量と使用のオペレーティング システムの数によって決まります。
<p>使用すると<strong>-更新</strong>、 <strong>-最大</strong>トレース セッションに割り当てられたバッファーの最大数を変更します。</p></td>
</tr>
<tr>
<td><strong>-ft</strong> <em>FlushTime</em></td>
<td>使用すると<strong>-開始</strong>、 <strong>-ft</strong> 、どのくらいの頻度 (秒単位)、トレース メッセージ バッファーがフラッシュされるを指定します。 使用すると<strong>-更新</strong>、 <strong>-ft</strong>フラッシュ時刻を指定した時間に変更します。
<p>フラッシュ時間の最小値は、1 秒です。 既定値は 0 (フラッシュを強制しないです)。</p>
<p>強制的な書き込みこれはトレース セッションを停止すると、トレース メッセージのバッファーがいっぱいのときに自動的に行われるフラッシュです。</p>
<p>参照してください: <strong>-フラッシュ</strong>します。</p></td>
</tr>
<tr>
<td><strong>-age</strong> <em>AgeLimit</em></td>
<td>使用すると<strong>-開始</strong>、 <strong>-年齢<strong>(分単位) を使用していないトレース バッファーが保持される期間解放される前に指定します。 使用すると<strong>-更新<strong>、 <strong>-年齢<strong>経過時間制限を指定した値に変更します。
<p><em>制限の期間を表す</em>(分単位) を使用していないトレース バッファーが保持される期間解放される前に指定します。 既定値は 15 分です。</p>
<p>このパラメーターは、Windows 2000 でのみ有効です。</p></td>
</tr>
<tr>
<td><strong>-paged</strong></td>
<td>トレースのメッセージ バッファーのページング可能なメモリを使用します。 既定では、イベントのトレースは、バッファーの非ページ メモリを使用します。 のみ使用して<strong>-開始</strong>します。
<p>プロバイダーがディスパッチより大きい IRQL でトレース メッセージを生成するドライバーの場合に、このパラメーターを使用しない\_レベル。</p>
<p>このパラメーターは、Windows 2000 ではサポートされていません。</p></td>
</tr>
<tr>
<td><strong>-seq</strong> <em>MaxFileSize</em></td>
<td>イベント トレース ログ (.etl) ファイルに (ファイルの終わりに、イベントの記録の停止) の連続したログ記録を指定します。 のみ使用して<strong>-開始</strong>します。
<p><em>MaxFileSize</em>ファイルの最大サイズを mb 単位で指定します。 なし、 <em>MaxFileSize</em>値、このパラメーターは無視されます。</p>
<p>シーケンシャルなログ記録は、既定では、ですが、このパラメーターを使用するには、ファイルの最大サイズを設定するかを使用して<strong>- prealloc</strong>します。 このパラメーターがない場合は、ファイル サイズの上限はありません。</p></td>
</tr>
<tr>
<td><strong>-cir</strong> <em>MaxFileSize</em></td>
<td>循環ログ (最も古いメッセージ経由で新しいメッセージをファイルの終わりのレコード) で、イベント トレース ログ (.etl) ファイルを指定します。 のみ使用して<strong>-開始</strong>します。
<p><em>MaxFileSize</em>ファイルの最大サイズを mb 単位で指定します。 なし、 <em>MaxFileSize</em>値、このパラメーターは無視されます。</p>
<p>既定値はシーケンシャル ファイルのサイズ制限なしでログに記録します。</p></td>
</tr>
<tr>
<td><strong>-prealloc</strong></td>
<td>割り当てる前に、イベント トレース ログ (.etl) ファイルの領域を予約します。 のみ使用して<strong>-開始</strong>します。
<p>このパラメーターが必要です<strong>-seq</strong>または<strong>-cir</strong>で<em>MaxFileSize</em>します。 無効な<strong>- newfile</strong>します。</p>
<p>Windows XP およびそれ以降のシステムでは、システムを作成、イベント トレース ログ (.etl) ファイル サイズと等しく、 <em>MaxFileSize</em>を使用して指定された値、 <strong>-seq</strong>または<strong>-cir</strong>パラメーター。 セッションを停止すると、その内容のサイズにログ ファイルが減少します。</p></td>
</tr>
<tr>
<td><strong>-newfile</strong> <em>MaxFileSize</em></td>
<td>既存のファイルに達するたびに、新しいイベント トレース ログ (.etl) ファイルを作成します<em>MaxFileSize</em>します。 のみ使用して<strong>-開始</strong>します。
<p><em>MaxFileSize</em>各ログ ファイルの最大サイズを mb 単位で指定します。 なし、 <em>MaxFileSize</em>値、このパラメーターは無視されます。</p>
<p>使用する場合<strong>- newfile</strong>、使用することも必要があります、 <strong>-f</strong> <em>ログ ファイル</em>パラメーターと値の<em>LogFile</em>を含む名前にする必要があります、文字<strong>%d</strong> decimal パターン - trace%d.etl などを指定します。 コマンドがエラーで失敗するそれ以外の場合、\_無効な\_名。 Windows では、新しいファイルを作成するたびにファイル名の 10 進値をインクリメントします。</p>
<p>このパラメーターは、事前割り当てに無効な (<strong>- prealloc</strong>ログ記録 (<strong>-cir</strong>)、NT Kernel Logger セッション、またはプライベートのトレース セッションのです。 Windows 2000 ではサポートされません。</p></td>
</tr>
<tr>
<td><strong>-追加</strong></td>
<td>既存のイベント トレース ログ (.etl) ファイルにトレース メッセージを追加します。 既定では、新しいファイルを作成します。 のみ使用して<strong>-開始</strong>します。
<p>シーケンシャル ファイルでのみこのパラメーターは有効な<strong>-f</strong>使用と<strong>-rt</strong>は使用されません。 Windows 2000 ではサポートされません。</p></td>
</tr>
<tr>
<td><strong>-kd</strong></td>
<td>KD または Windbg、トレース メッセージをリダイレクトする方がアタッチされています。 このパラメーターもトレース バッファーのサイズをデバッガーの最大バッファー サイズは 3 KB に設定し、いずれかを無視します<strong>-b</strong>コマンドのパラメーター。 のみ使用して<strong>-開始</strong>します。</td>
</tr>
</tbody>
</table>

### <a name="comments"></a>コメント

A **traceview で**パラメーターなしでコマンドが traceview でウィンドウを開きます。

Traceview でを使用するを起動するコマンドを開始、[グローバル ロガー トレース セッション](global-logger-trace-session.md)。 これを行うには、次のコマンド形式を使用します。 その他のコマンドとは異なりコマンド形式では、"GlobalLogger"という単語が大文字小文字を区別します。

```command
traceview -start GlobalLogger [parameters]
```
