---
title: GFlags のフラグ テーブル
description: GFlags のフラグ テーブル
ms.assetid: 09029471-8b29-4232-bee1-d2802035b0fb
keywords:
- GFlags、フラグ テーブル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb658615d208ca432f411b0a0cb9896f1a867c50
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370866"
---
# <a name="gflags-flag-table"></a>GFlags のフラグ テーブル


## <span id="ddk_gflags_flag_table_dtools"></span><span id="DDK_GFLAGS_FLAG_TABLE_DTOOLS"></span>


次の表は、GFlags を変更するフラグ、16 進数の値と、各フラグとフラグが有効である宛先 (R はレジストリにイメージ ファイルには、カーネルは K) の省略形を示します。

各フラグの詳細については、次を参照してください。、[グローバル フラグ参照](global-flag-reference.md)します。

GFlags の使用方法の詳細については、次を参照してください。 [GFlags 概要](gflags-overview.md)と[GFlags 詳細](gflags-details.md)します。

**重要な**   Windows Server 2003 および以降のバージョンの Windows では完全に有効になってプール タグ付けします。 これらのシステムで、**プール タグ付けを有効にする**チェック ボックスをオン、**グローバル フラグ** ダイアログ ボックスは淡色表示になり、プール タグ付けの失敗を有効または無効にするコマンド。

 

**注**  各フラグのシンボリック名では、参照のみが提供されます。 シンボル名を変更するため、信頼性の高いグローバル フラグの識別子ではありません。

 

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">説明</th>
<th align="left">シンボリック名</th>
<th align="left">16 進数の値</th>
<th align="left">省略形</th>
<th align="left">宛先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="buffer-dbgprint-output.md" data-raw-source="[Buffer DbgPrint Output](buffer-dbgprint-output.md)">バッファーによる DbgPrint の出力</a></p></td>
<td align="left"><p>FLG_DISABLE_DBGPRINT</p></td>
<td align="left"><p>0x08000000</p></td>
<td align="left"><p>ddp</p></td>
<td align="left"><p>R、K</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="create-kernel-mode-stack-trace-database.md" data-raw-source="[Create kernel mode stack trace database](create-kernel-mode-stack-trace-database.md)">カーネル モード スタック トレースのデータベースを作成します。</a></p></td>
<td align="left"><p>FLG_KERNEL_STACK_TRACE_DB</p></td>
<td align="left"><p>0x2000</p></td>
<td align="left"><p>kst</p></td>
<td align="left"><p>R</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="create-user-mode-stack-trace-database.md" data-raw-source="[Create user mode stack trace database](create-user-mode-stack-trace-database.md)">ユーザー モードのスタック トレースのデータベースを作成します。</a></p></td>
<td align="left"><p>FLG_USER_STACK_TRACE_DB</p></td>
<td align="left"><p>0x1000</p></td>
<td align="left"><p>ust</p></td>
<td align="left"><p>R、K は</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-initial-command.md" data-raw-source="[Debug initial command](debug-initial-command.md)">最初のコマンドをデバッグします。</a></p></td>
<td align="left"><p>FLG_DEBUG_INITIAL_COMMAND</p></td>
<td align="left"><p>0x04</p></td>
<td align="left"><p>dic</p></td>
<td align="left"><p>R</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-winlogon.md" data-raw-source="[Debug WinLogon](debug-winlogon.md)">WinLogon をデバッグします。</a></p></td>
<td align="left"><p>FLG_DEBUG_INITIAL_COMMAND_EX</p></td>
<td align="left"><p>0x04000000</p></td>
<td align="left"><p>dwl</p></td>
<td align="left"><p>R</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="disable-heap-coalesce-on-free.md" data-raw-source="[Disable heap coalesce on free](disable-heap-coalesce-on-free.md)">ヒープを無効にする無料の結合</a></p></td>
<td align="left"><p>FLG_HEAP_DISABLE_COALESCING</p></td>
<td align="left"><p>0x00200000</p></td>
<td align="left"><p>dhc</p></td>
<td align="left"><p>R、K は</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="disable-paging-of-kernel-stacks.md" data-raw-source="[Disable paging of kernel stacks](disable-paging-of-kernel-stacks.md)">カーネル スタックのページングを無効にします。</a></p></td>
<td align="left"><p>FLG_DISABLE_PAGE_KERNEL_STACKS</p></td>
<td align="left"><p>0x080000</p></td>
<td align="left"><p>dps</p></td>
<td align="left"><p>R</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="disable-protected-dll-verification.md" data-raw-source="[Disable protected DLL verification](disable-protected-dll-verification.md)">保護されている DLL の検証を無効にします。</a></p></td>
<td align="left"><p>FLG_DISABLE_PROTDLLS</p></td>
<td align="left"><p>0x80000000</p></td>
<td align="left"><p>dpd</p></td>
<td align="left"><p>R、K は</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="disable-stack-extension.md" data-raw-source="[Disable stack extension](disable-stack-extension.md)">スタックの拡張機能を無効にします。</a></p></td>
<td align="left"><p>FLG_DISABLE_STACK_EXTENSION</p></td>
<td align="left"><p>0x010000</p></td>
<td align="left"><p>dse</p></td>
<td align="left"><p>I</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="early-critical-section-event-creation.md" data-raw-source="[Early critical section event creation](early-critical-section-event-creation.md)">初期のクリティカル セクション イベントの作成</a></p></td>
<td align="left"><p>FLG_CRITSEC_EVENT_CREATION</p></td>
<td align="left"><p>0x10000000</p></td>
<td align="left"><p>cse</p></td>
<td align="left"><p>R、K は</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="enable-application-verifier.md" data-raw-source="[Enable application verifier](enable-application-verifier.md)">アプリケーション検証ツールを有効にします。</a></p></td>
<td align="left"><p>FLG_APPLICATION_VERIFIER</p></td>
<td align="left"><p>0x0100</p></td>
<td align="left"><p>vrf</p></td>
<td align="left"><p>R、K は</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enable-bad-handles-detection.md" data-raw-source="[Enable bad handles detection](enable-bad-handles-detection.md)">無効なハンドルの検出を有効にします。</a></p></td>
<td align="left"><p>FLG_ENABLE_HANDLE_EXCEPTIONS</p></td>
<td align="left"><p>0x40000000</p></td>
<td align="left"><p>bhd</p></td>
<td align="left"><p>R、K</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="enable-close-exception.md" data-raw-source="[Enable close exception](enable-close-exception.md)">閉じる例外を有効にします。</a></p></td>
<td align="left"><p>FLG_ENABLE_CLOSE_EXCEPTIONS</p></td>
<td align="left"><p>0x400000</p></td>
<td align="left"><p>ece</p></td>
<td align="left"><p>R、K</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enable-debugging-of-win32-subsystem.md" data-raw-source="[Enable debugging of Win32 subsystem](enable-debugging-of-win32-subsystem.md)">Win32 サブシステムのデバッグを有効にします。</a></p></td>
<td align="left"><p>FLG_ENABLE_CSRDEBUG</p></td>
<td align="left"><p>0x020000</p></td>
<td align="left"><p>d32</p></td>
<td align="left"><p>R</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="enable-exception-logging.md" data-raw-source="[Enable exception logging](enable-exception-logging.md)">例外のログ記録を有効にします。</a></p></td>
<td align="left"><p>FLG_ENABLE_EXCEPTION_LOGGING</p></td>
<td align="left"><p>0x800000</p></td>
<td align="left"><p>eel</p></td>
<td align="left"><p>R、K</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enable-heap-free-checking.md" data-raw-source="[Enable heap free checking](enable-heap-free-checking.md)">ヒープの無料のチェックを有効にします。</a></p></td>
<td align="left"><p>FLG_HEAP_ENABLE_FREE_CHECK</p></td>
<td align="left"><p>0x20</p></td>
<td align="left"><p>hfc</p></td>
<td align="left"><p>R、K は</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="enable-heap-parameter-checking.md" data-raw-source="[Enable heap parameter checking](enable-heap-parameter-checking.md)">ヒープ パラメーター チェックを有効にします。</a></p></td>
<td align="left"><p>FLG_HEAP_VALIDATE_PARAMETERS</p></td>
<td align="left"><p>0x40</p></td>
<td align="left"><p>hpc</p></td>
<td align="left"><p>R、K は</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enable-heap-tagging.md" data-raw-source="[Enable heap tagging](enable-heap-tagging.md)">ヒープのタグ付けを有効にします。</a></p></td>
<td align="left"><p>FLG_HEAP_ENABLE_TAGGING</p></td>
<td align="left"><p>0x0800</p></td>
<td align="left"><p>加熱</p></td>
<td align="left"><p>R、K は</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="enable-heap-tagging-by-dll.md" data-raw-source="[Enable heap tagging by DLL](enable-heap-tagging-by-dll.md)">DLL をヒープでタグ付けを有効にします。</a></p></td>
<td align="left"><p>FLG_HEAP_ENABLE_TAG_BY_DLL</p></td>
<td align="left"><p>0x8000</p></td>
<td align="left"><p>htd</p></td>
<td align="left"><p>R、K は</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enable-heap-tail-checking.md" data-raw-source="[Enable heap tail checking](enable-heap-tail-checking.md)">ヒープの末尾のチェックを有効にします。</a></p></td>
<td align="left"><p>FLG_HEAP_ENABLE_TAIL_CHECK</p></td>
<td align="left"><p>0x10</p></td>
<td align="left"><p>HTC</p></td>
<td align="left"><p>R、K は</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="enable-heap-validation-on-call.md" data-raw-source="[Enable heap validation on call](enable-heap-validation-on-call.md)">呼び出しでヒープの検証を有効にします。</a></p></td>
<td align="left"><p>FLG_HEAP_VALIDATE_ALL</p></td>
<td align="left"><p>0x80</p></td>
<td align="left"><p>hvc</p></td>
<td align="left"><p>R、K は</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enable-loading-of-kernel-debugger-symbols.md" data-raw-source="[Enable loading of kernel debugger symbols](enable-loading-of-kernel-debugger-symbols.md)">カーネル デバッガーのシンボルの読み込みを有効にします。</a></p></td>
<td align="left"><p>FLG_ENABLE_KDEBUG_SYMBOL_LOAD</p></td>
<td align="left"><p>0x040000</p></td>
<td align="left"><p>ksl</p></td>
<td align="left"><p>R、K</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="enable-object-handle-type-tagging.md" data-raw-source="[Enable object handle type tagging](enable-object-handle-type-tagging.md)">オブジェクト ハンドル型のタグ付けを有効にします。</a></p></td>
<td align="left"><p>FLG_ENABLE_HANDLE_TYPE_TAGGING</p></td>
<td align="left"><p>0x01000000</p></td>
<td align="left"><p>eot</p></td>
<td align="left"><p>R、K</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enable-page-heap.md" data-raw-source="[Enable page heap](enable-page-heap.md)">ページ ヒープを有効にします。</a></p></td>
<td align="left"><p>FLG_HEAP_PAGE_ALLOCS</p></td>
<td align="left"><p>0x02000000</p></td>
<td align="left"><p>hpa</p></td>
<td align="left"><p>R、K は</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<a href="enable-pool-tagging.md" data-raw-source="[Enable pool tagging](enable-pool-tagging.md)">プールのタグ付けを有効にする</a>(Windows 2000 および Windows XP の場合のみ)</td>
<td align="left"><p>FLG_POOL_ENABLE_TAGGING</p></td>
<td align="left"><p>0x0400</p></td>
<td align="left"><p>ptg</p></td>
<td align="left"><p>R</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enable-system-critical-breaks.md" data-raw-source="[Enable system critical breaks](enable-system-critical-breaks.md)">システムの重要な区切りを有効にします。</a></p></td>
<td align="left"><p>FLG_ENABLE_SYSTEM_CRIT_BREAKS</p></td>
<td align="left"><p>0x100000</p></td>
<td align="left"><p>scb</p></td>
<td align="left"><p>R、K は</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="load-image-using-large-pages-if-possible.md" data-raw-source="[Load image using large pages if possible](load-image-using-large-pages-if-possible.md)">可能であれば大きなページを使用してイメージを読み込む</a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>lpg</p></td>
<td align="left"><p>I</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="maintain-a-list-of-objects-for-each-type.md" data-raw-source="[Maintain a list of objects for each type](maintain-a-list-of-objects-for-each-type.md)">各型のオブジェクトの一覧を管理します。</a></p></td>
<td align="left"><p>FLG_MAINTAIN_OBJECT_TYPELIST</p></td>
<td align="left"><p>0x4000</p></td>
<td align="left"><p>otl</p></td>
<td align="left"><p>R</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="enable-silent-process-exit-monitoring.md" data-raw-source="[Enable silent process exit monitoring](enable-silent-process-exit-monitoring.md)">サイレント プロセス終了の監視を有効にします。</a></p></td>
<td align="left"><p>FLG_MONITOR_SILENT_PROCESS_EXIT</p></td>
<td align="left"><p>0x200</p></td>
<td align="left"></td>
<td align="left"><p>R</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="object-reference-tracing.md" data-raw-source="[Object Reference Tracing](object-reference-tracing.md)">オブジェクト参照のトレース</a></p>
<p>(Windows Vista 以降)</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>R、K</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="show-loader-snaps.md" data-raw-source="[Show loader snaps](show-loader-snaps.md)">ローダーのスナップを表示します。</a></p></td>
<td align="left"><p>FLG_SHOW_LDR_SNAPS</p></td>
<td align="left"><p>0x02</p></td>
<td align="left"><p>sls</p></td>
<td align="left"><p>R、K は</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特別なプール</a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>spp</p></td>
<td align="left"><p>R</p>
<p>R、K (Windows Vista 以降)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="stop-on-exception.md" data-raw-source="[Stop on exception](stop-on-exception.md)">例外を停止します。</a></p></td>
<td align="left"><p>FLG_STOP_ON_EXCEPTION</p></td>
<td align="left"><p>0x01</p></td>
<td align="left"><p>soe と略記されます。</p></td>
<td align="left"><p>R、K は</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="stop-on-hung-gui.md" data-raw-source="[Stop on hung GUI](stop-on-hung-gui.md)">ハングした GUI を停止します。</a></p></td>
<td align="left"><p>FLG_STOP_ON_HUNG_GUI</p></td>
<td align="left"><p>0x08</p></td>
<td align="left"><p>shg</p></td>
<td align="left"><p>K</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="stop-on-unhandled-user-mode-exception.md" data-raw-source="[Stop on unhandled user-mode exception](stop-on-unhandled-user-mode-exception.md)">ユーザー モードのハンドルされない例外で停止します。</a></p></td>
<td align="left"><p>FLG_STOP_ON_UNHANDLED_EXCEPTION</p></td>
<td align="left"><p>0x20000000</p></td>
<td align="left"><p>sue</p></td>
<td align="left"><p>R、K は</p></td>
</tr>
</tbody>
</table>

 

 

 





