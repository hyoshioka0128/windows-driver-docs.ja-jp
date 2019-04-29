---
title: グローバル ロガー トレース セッション
description: グローバル ロガー トレース セッション
ms.assetid: d78ce5d8-a9f3-47d6-be7a-eeaeacd7b872
keywords:
- セッション WDK、グローバルのロガーをトレースします。
- グローバル ロガー トレース セッション WDK、ロガーがグローバル セッションについて
- グローバルなロガー トレース セッション WDK、レジストリ エントリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c256324de636d8cb467d88b02b89972da967a1a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329696"
---
# <a name="global-logger-trace-session"></a>グローバル ロガー トレース セッション

A*グローバル ロガー トレース セッション*システムがデバイス ドライバーによって生成されたイベントなど、完全に動作する前に、ブート プロセス中に発生するイベントを記録します。 Windows に組み込まれている予約済みのトレース セッションです。

グローバル ロガー トレース セッションを常には、メッセージをトレース ログに書き込みます。 グローバル ロガーはリアルタイムのトレース セッションをサポートしていないか、トレース セッション バッファーに格納します。

グローバルのロガーは、オペレーティング システムのブート プロセスの早い段階で使用できないする必要があります、ためは、起動し、レジストリ エントリを使用して構成には (で、 **HKLM\\システム\\CurrentControlSet\\コントロール\\WMI\\GlobalLogger**サブキー)、関数呼び出しではなく。 開始した後、グローバルのロガーは、通常のイベント トレース セッションのように動作します。

グローバル ロガーのトレース セッションは、予約済みのセッション名を"GlobalLogger" [コントロール GUID](control-guid.md) 、定数で表される**GlobalLoggerGuid**します。 グローバル ロガー トレース セッションを作成し、トレース セッションを開始するコンピューターを再起動します。 1 つだけのグローバル ログ トレース セッションは、一度にコンピューターで実行できます。

グローバル ロガー トレース セッションを作成するには使用[Tracelog](tracelog.md)します。 自動的に、レジストリ サブキーとトレース セッションのオプションを格納するエントリを作成します。 グローバルのロガーのトレース セッションは、コンピューターを再起動するときに起動します。 詳細については、次を参照してください。 [ **Tracelog コマンド構文**](tracelog-command-syntax.md)します。

グローバルのロガーのトレース セッションからのトレース メッセージの書式設定、使用[Tracefmt](tracefmt.md) system.tmf で、[トレース メッセージのフォーマット ファイル](trace-message-format-file.md)WDK に含まれます。

レジストリ エントリでグローバル ロガー セッションがトリガーされるため、レジストリにエントリが表示されるたびを実行します。 ロガーがグローバル セッションが、システムが起動するたびに開始しないように、設定の値、**開始**0 エントリまたはすべてのレジストリ エントリを削除します。

グローバルのロガーのトレース セッションは、これにより、ブート プロセス中に、カーネルをトレース NT Kernel Logger トレース セッションに変換できます。 詳しくは、次を参照してください[起動時のロガーのグローバルなセッション。](boot-time-global-logger-session.md)

[トレース プロバイダー](trace-provider.md)、カーネル モード ドライバーとユーザー モード アプリケーションがグローバルのロガーのトレース セッションにログインできるようします。 これにより、システムの起動中にドライバーやその他のトレース プロバイダーをトレースすることができます。 詳しくは、次を参照してください[ロガーのグローバルなセッションへのログ記録。](logging-to-the-global-logger-session.md)

## <a name="limitations-of-the-global-logger-trace-session"></a>グローバルのロガーのトレース セッションの制限事項

グローバル ロガーのトレース セッションは非常に便利ですが、制限事項ののでご注意ください。

一度に 1 つだけのグローバル ログ セッションを実行できます。

セッションが送信しないグローバル ロガーは、プロバイダーへの通知を有効にします。

グローバルのロガーのレジストリ エントリがレジストリに保持され、リセットまたは、手動で削除するかを使用するまでは、有効、 **tracelog-削除**コマンド。 それらをリセットするまで、システムを起動するたびにグローバル ロガー セッションが開始します。

Windows ACPI ロガーは無期限にグローバル ロガー トレース セッションで有効にします。 トレース ログにこのロガーからのトレース メッセージが表示されます。

標準のトレース セッションでは、ドライバーがグローバルのロガーのセッションにログ記録中を起動する場合、ドライバーはスイッチし、標準のトレース セッションにログ記録を開始します。

## <a name="global-logger-registry-entries"></a>グローバルのロガーのレジストリ エントリ

次の表では、グローバル ロガー セッションを構成するレジストリ エントリを示します。 これらのエントリは、 **HKLM\\システム\\CurrentControlSet\\コントロール\\WMI\\GlobalLogger**サブキー。 のみ、**開始**エントリが必要です。

に加えて、このテーブルのレジストリ エントリを追加することも、 **ControlGUID**サブキーの下、 **GlobalLogger**を表すグローバル ロガーは、トレース ログに記録すると、ドライバーなどのトレース プロバイダーのサブキーセッションです。 詳しくは、次を参照してください。[ロガーのグローバルなセッションへのログ記録](logging-to-the-global-logger-session.md)します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">入力</th>
<th align="left">データ型</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>スタート</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>設定すると<strong>1</strong>グローバル ロガー セッションが、次回システム起動時を開始する (オン)。</p>
<p><strong>0</strong> = オフ、 <strong>1</strong>= on</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>BufferSize</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>(KB) 内の各バッファーのサイズを指定します。 既定値は、0x40 (64 KB) です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ClockType</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>トレース メッセージのタイムスタンプを使用するタイマーを指定します。</p>
<p>Windows Vista 以降、既定値は<strong>1</strong>します。 既定値は、Windows Vista より前のオペレーティング システムで<strong>2</strong>します。</p>
<p><strong>1</strong>パフォーマンス カウンターの値 (高解像度) を =</p>
<p><strong>2</strong>システム タイマーを =</p>
<p><strong>3</strong> CPU サイクルのクロックを =</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>EnableKernelFlags</strong></p></td>
<td align="left"><p>REG_BINARY</p></td>
<td align="left"><p>NT Kernel Logger のトレース セッションをグローバル ロガー セッションに変換し、カーネル トレースに含まれるイベントを指定します。</p>
<p>詳しくは、次を参照してください。<a href="boot-time-global-logger-session.md" data-raw-source="[Boot-time Global Logger Session](boot-time-global-logger-session.md)">起動時のグローバルなロガー セッション</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileCounter</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>ロガーがグローバル セッションによって生成されたイベント トレース ログ ファイルの数を格納します。</p>
<p>値に達するまで、システムがこの値をインクリメント<strong>FileMax</strong>します。 次に、値を 0 にリセットされます。</p>
<p>このカウンターは、システムがグローバル ロガー トレース ログ ファイルを上書きすることを防ぎます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileMax</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>システムで許可されているイベント トレース ログ ファイルの最大数を指定します。</p>
<p>トレース ログの数には、指定した最大値に達すると、システムは、以降で、最も古いログは、上書きを開始します。</p>
<p>既定値は 0、最大値がないことを意味します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileName</strong></p></td>
<td align="left"><p>REG_SZ</p></td>
<td align="left"><p>パス (省略可能) とイベントのトレース ログ ファイルのファイル名。 既定では %systemroot%\system32\logfiles\wmi\trace.log します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FlushTimer</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>バッファーが強制的にフラッシュされるトレースをどのくらいの頻度 (秒) を指定します。 強制的な書き込みこれは、自動的にフラッシュ バッファーがいっぱいのときに、トレース セッションを停止したときに発生します。</p>
<p>既定値は 0 です。 既定では、いっぱいになった場合にのみ、バッファーがフラッシュされます。</p>
<p>フラッシュ時間の最小値は、1 秒です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>LogFileMode</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>ログ セッション オプションを指定します。</p>
<p>Windows Vista と Windows の以降のバージョンでのみサポートされています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MaximumBuffers</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>セッションに割り当てられるバッファーの最大数を指定します。 既定値は、0x19 (25 です)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>理由により</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>イベントのトレース ログ ファイルの最大サイズを指定します。 既定では、ファイルの最大サイズはありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MinimumBuffers</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>セッションの開始時に割り当てられたバッファーの数を指定します。 既定値は、0x3 です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ステータス</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>グローバル ロガー トレース セッションを開始しようとするからのリターン コードを格納します。</p>
<p>開始するセッションが失敗した場合、Win32 エラー コードは、このエントリの値。 セッションが開始されている場合、このエントリの値は ERROR_SUCCESS が。</p></td>
</tr>
</tbody>
</table>

 

作成したこれらのレジストリ エントリはレジストリに保持され、それらを削除するか、その値を変更するまでは、有効。 したがって、グローバル ロガー セッションが実行すると、使用、 **tracelog-GlobalLogger を削除**の値を設定するコマンド、**開始**エントリを 0 に他のグローバル ロガーのレジストリ エントリを削除します。 それ以外の場合、グローバル ロガー セッションでは、コンピューターを再起動することと、生成されたログ ファイルは非常に大きくなることができますに毎回が実行されます。

## <a name="logging-mode-constants"></a>ログ記録モード定数

次の表に、有効な値、 **LogFileMode**レジストリ エントリ、 **HKLM\\システム\\CurrentControlSet\\コントロール\\WMI\\GlobalLogger**サブキー。 このエントリは、リアルタイムのトレース セッション、プライベートのトレース セッション、循環ログ記録、および (ログなし) のバッファリング用も含む、グローバルのロガーのトレース セッションのオプションの設定に使用されます。 このレジストリ エントリは、Windows Vista および Windows の以降のバージョンでのみサポートされます。

このレジストリ エントリに対応して、 **LogFileMode**イベント メンバー\_トレース\_プロパティ構造体。 その値は、ログ記録モードの定数に対応します。 イベント\_トレース\_プロパティ構造とログ記録モードの定数は、Microsoft Windows SDK ドキュメントで説明します。

このテーブルは、定数の 16 進数の値を表示するのには、ここに表示されます。 これらの値またはこれらの値の合計に定数を表すを使用して、 **LogFileMode**レジストリ エントリ。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">定数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>EVENT_TRACE_FILE_MODE_NONE</p></td>
<td align="left"><p>イベント トレース ログ ファイルは作成されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>EVENT_TRACE_FILE_MODE_SEQUENTIAL</p></td>
<td align="left"><p>イベント トレース ログ ファイルは順次です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>EVENT_TRACE_FILE_MODE_CIRCULAR</p></td>
<td align="left"><p>イベント トレース ログ ファイルが循環します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>EVENT_TRACE_FILE_MODE_APPEND</p></td>
<td align="left"><p>既存のログ ファイルにトレース メッセージを追加します。 このモードはシーケンシャル ファイルでのみ有効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>EVENT_TRACE_FILE_MODE_NEWFILE</p></td>
<td align="left"><p>既存のファイルがの値に達するたびに新しいイベント トレース ログ ファイルを作成、<strong>理由により</strong>エントリ (上の表を参照してください)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20</p></td>
<td align="left"><p>EVENT_TRACE_FILE_MODE_PREALLOCATE</p></td>
<td align="left"><p>イベントのトレース ログ ファイルの領域を予約します。</p>
<p>EVENT_TRACE_FILE_MODE_SEQUENTIAL または EVENT_TRACE_FILE_MODE_CIRCULAR でのみ有効ですし EVENT_TRACE_FILE_MODE_NEWFILE とが無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40</p></td>
<td align="left"><p>EVENT_TRACE_NONSTOPPABLE_MODE</p></td>
<td align="left"><p>呼び出し<strong>StopTrace</strong>トレース セッションを停止しません。</p>
<p>この機能は、ユーザーがシステムに必要な診断トレース セッションを停止して、チューニングを防止します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x100</p></td>
<td align="left"><p>EVENT_TRACE_REAL_TIME_MODE</p></td>
<td align="left"><p>リアルタイムのトレース セッションを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x200</p></td>
<td align="left"><p>EVENT_TRACE_DELAY_OPEN_FILE_MODE</p></td>
<td align="left"><p>内部使用専用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x400</p></td>
<td align="left"><p>EVENT_TRACE_BUFFERING_MODE</p></td>
<td align="left"><p>イベントはバッファーに保持されます。 ログ ファイルに書き込まれるまたはトレース コンシューマーに配信するはしないでください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x800</p></td>
<td align="left"><p>EVENT_TRACE_PRIVATE_LOGGER_MODE</p></td>
<td align="left"><p>プライベートのトレース セッションを指定します。 このフラグがグローバルのロガーのトレース セッションは無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000</p></td>
<td align="left"><p>EVENT_TRACE_ADD_HEADER_MODE</p></td>
<td align="left"><p>内部使用専用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2000</p></td>
<td align="left"><p>EVENT_TRACE_USE_KBYTES_FOR_SIZE</p></td>
<td align="left"><p>値を解釈<strong>理由により</strong>MB ではなく、(kb)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4000</p></td>
<td align="left"><p>EVENT_TRACE_USE_GLOBAL_SEQUENCE</p></td>
<td align="left"><p>トレース メッセージのグローバル シーケンス番号を生成します。 これらの数値は、コンピューター上のすべてのトレース セッションに一意です。</p>
<p>既定では、トレース メッセージはすべてシーケンス番号はありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8000</p></td>
<td align="left"><p>EVENT_TRACE_USE_LOCAL_SEQUENCE</p></td>
<td align="left"><p>トレース メッセージをローカルのシーケンス番号を生成します。 これらの数値は、トレース セッション内で一意です。</p>
<p>既定では、トレース メッセージはすべてシーケンス番号はありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10000</p></td>
<td align="left"><p>EVENT_TRACE_RELOG_MODE</p></td>
<td align="left"><p>内部使用専用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>これに対して、0x80000</p></td>
<td align="left"><p>EVENT_TRACE_KD_FILTER_MODE</p></td>
<td align="left"><p>カーネル デバッガーにトレース メッセージをリダイレクトし、トレース バッファーのサイズをデバッガーの最大バッファー サイズは 3 KB に設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000000</p></td>
<td align="left"><p>EVENT_TRACE_MODE_RESERVED</p></td>
<td align="left"><p>グローバルのロガーのトレース セッションでは無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x01000000</p></td>
<td align="left"><p>EVENT_TRACE_USE_PAGED_MEMORY</p></td>
<td align="left"><p>トレース セッション バッファー ページング可能なメモリからを割り当てます。 既定では、バッファーは、非ページング メモリから割り当てられます。</p></td>
</tr>
</tbody>
</table>
 





