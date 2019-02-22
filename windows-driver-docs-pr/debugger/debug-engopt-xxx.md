---
title: デバッグ\_ENGOPT\_XXX
description: デバッグ\_ENGOPT\_XXX 定数は、グローバル オプションは、デバッガー エンジンの動作に影響します。
ms.date: 08/10/2018
topic_type:
- apiref
api_name:
- DEBUG_ENGOPT_XXX
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 9f4ac904c4a2498defac56e4fb0dd9985e3ffe3c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549865"
---
# <a name="debugengoptxxx"></a>デバッグ\_ENGOPT\_XXX

次のグローバル オプションでは、デバッガー エンジンの動作に影響します。
<table>
<tr>
<th>定数</th>
<th>説明</th>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_IGNORE_DBGHELP_VERSION"></a><a id="debug_engopt_ignore_dbghelp_version"></a><dl>
<dt><b>DEBUG_ENGOPT_IGNORE_DBGHELP_VERSION</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>デバッガー エンジンでは、DbgHelp DLL のバージョンがデバッガー エンジンのバージョンと一致しない場合、エラーではなく警告が生成されます。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_IGNORE_EXTENSION_VERSIONS"></a><a id="debug_engopt_ignore_extension_versions"></a><dl>
<dt><b>DEBUG_ENGOPT_IGNORE_EXTENSION_VERSIONS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>バージョンの拡張機能を無効にします。  これにより、デバッガー エンジンが抑制&#39;CheckVersion の呼び出し。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_ALLOW_NETWORK_PATHS"></a><a id="debug_engopt_allow_network_paths"></a><dl>
<dt><b>DEBUG_ENGOPT_ALLOW_NETWORK_PATHS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>シンボルと拡張機能を読み込むため、ネットワーク共有を使用できます。 エンジンをいくつかのシステム プロセスをデバッグするときに、ネットワーク パスを禁止するためのオプションと、注意して使用する必要があります。</p>
<p>DEBUG_ENGOPT_DISALLOW_NETWORK_PATHS が設定されている場合、このオプションを設定することはできません。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_DISALLOW_NETWORK_PATHS"></a><a id="debug_engopt_disallow_network_paths"></a><dl>
<dt><b>DEBUG_ENGOPT_DISALLOW_NETWORK_PATHS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>シンボルと拡張機能を読み込むため、ネットワーク共有を使用できません。 エンジンは、一部のシステム プロセスをデバッグするときに、このオプションを設定しようとします。</p>
<p>DEBUG_ENGOPT_ALLOW_NETWORK_PATHS が設定されている場合、このオプションを設定することはできません。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_NETWORK_PATHS"></a><a id="debug_engopt_network_paths"></a><dl>
<dt><b>DEBUG_ENGOPT_NETWORK_PATHS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>DEBUG_ENGOPT_ALLOW_NETWORK_PATHS と DEBUG_ENGOPT_DISALLOW_NETWORK_PATHS のビットごとの OR。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_IGNORE_LOADER_EXCEPTIONS"></a><a id="debug_engopt_ignore_loader_exceptions"></a><dl>
<dt><b>DEBUG_ENGOPT_IGNORE_LOADER_EXCEPTIONS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>一部の古いバージョンの Windows でローダーによって生成される予期される初回例外を無視します。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_INITIAL_BREAK"></a><a id="debug_engopt_initial_break"></a><dl>
<dt><b>DEBUG_ENGOPT_INITIAL_BREAK</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>ターゲットにデバッガーに割り込む&#39;s 最初のイベント。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_INITIAL_MODULE_BREAK"></a><a id="debug_engopt_initial_module_break"></a><dl>
<dt><b>DEBUG_ENGOPT_INITIAL_MODULE_BREAK</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>ターゲットの 1 つ目のモジュールの読み込み時に、デバッガーを中断します。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_FINAL_BREAK"></a><a id="debug_engopt_final_break"></a><dl>
<dt><b>DEBUG_ENGOPT_FINAL_BREAK</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>ターゲットにデバッガーに割り込む&#39;s の最終的なイベント。 ライブ ユーザー モードのターゲット プロセスが終了する場合です。 カーネル モードの影響を与えません。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_NO_EXECUTE_REPEAT"></a><a id="debug_engopt_no_execute_repeat.md"></a><dl>
<dt><b>DEBUG_ENGOPT_NO_EXECUTE_REPEAT</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>空のコマンドを指定する場合、デバッガー エンジンは最後のコマンドは繰り返されません。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_FAIL_INCOMPLETE_INFORMATION"></a><a id="debug_engopt_fail_incomplete_information.md"></a><dl>
<dt><b>DEBUG_ENGOPT_FAIL_INCOMPLETE_INFORMATION</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>デバッガーをマップできません。 イメージがモジュールの読み込み防止します。</p>
<p>デバッガーは、イメージが含まれていないミニダンプをデバッグするときにイメージの読み込みを試みます。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_ALLOW_READ_ONLY_BREAKPOINTS"></a><a id="debug_engopt_allow_read_only_breakpoints"></a><dl>
<dt><b>DEBUG_ENGOPT_ALLOW_READ_ONLY_BREAKPOINTS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>メモリの読み取り専用のセクションではソフトウェアのブレークポイントの設定を許可する対象のページ保護を操作するデバッガー エンジンを使用できます。</p>
<p>エンジンが、ターゲットの変更を透過的にソフトウェアのブレークポイントを設定するときに&#39;割り込み命令を挿入するメモリ。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_SYNCHRONIZE_BREAKPOINTS"></a><a id="debug_engopt_synchronize_breakpoints"></a><dl>
<dt><b>DEBUG_ENGOPT_SYNCHRONIZE_BREAKPOINTS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>ライブ ユーザー モードのデバッグでは、エンジンは、挿入とターゲットのすべてのスレッドでは、常に一貫性のあるブレークポイント状態が存在することを確認するブレークポイントを削除するときに、余分な作業を実行します。</p>
<p>このオプションは、複数のスレッドが、ブレークポイントを設定する対象のコードを使用する場合に便利です。 ただし、デッドロックの可能性が生じます。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_DISALLOW_SHELL_COMMANDS"></a><a id="debug_engopt_disallow_shell_commands"></a><dl>
<dt><b>DEBUG_ENGOPT_DISALLOW_SHELL_COMMANDS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>デバッガーで実行中のシェル コマンドを許可しないようにします。</p>
<p>このオプションを設定した後は、設定を解除することはできません。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_KD_QUIET_MODE"></a><a id="debug-engopt-kd-quiet-mode.md"></a><dl>
<dt><b>DEBUG_ENGOPT_KD_QUIET_MODE</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>Quiet モードを有効にします。 詳細については、次を参照してください。 <a href="sq--set-quiet-mode-.md"> <b>sq (非表示モードの設定)</b></a>します。 </p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_DISABLE_MANAGED_SUPPORT"></a><a id="debug_engopt_disable_managed_support"></a><dl>
<dt><b>DEBUG_ENGOPT_DISABLE_MANAGED_SUPPORT</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>デバッガーのマネージ コードのエンジンのサポートを無効にします。 サポートのマネージ コードは既に使用して、この場合、オプションが影響を与えません。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_DISABLE_MODULE_SYMBOL_LOAD"></a><a id="debug_engopt_disable_module_symbol_load"></a><dl>
<dt><b>DEBUG_ENGOPT_DISABLE_MODULE_SYMBOL_LOAD</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>デバッガーでは、このフラグが設定されているときに読み込まれるモジュールのシンボルは読み込まれません。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_DISABLE_EXECUTION_COMMANDS"></a><a id="debug_engopt_disable_execution_commands"></a><dl>
<dt><b>DEBUG_ENGOPT_DISABLE_EXECUTION_COMMANDS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>実行を開始するようにターゲットを原因となる任意のコマンドをできないようにします。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_DISALLOW_IMAGE_FILE_MAPPING"></a><a id="debug_engopt_disallow_image_file_mapping"></a><dl>
<dt><b>DEBUG_ENGOPT_DISALLOW_IMAGE_FILE_MAPPING</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>ディスクから画像ファイルのマッピングは許可しません。 たとえば、このオプションは、ミニダンプ ファイルのデバッグ中にメモリの内容のイメージのマッピングを禁止します。
このオプションでは既存のマッピングには影響しませんイメージ ファイルにマップする以降にのみ影響します。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_PREFER_DML"></a><a id="debug_engopt_prefer_dml"></a><dl>
<dt><b>DEBUG_ENGOPT_PREFER_DML</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>デバッガーには、既定のコマンドと操作の DML が強化されたバージョンが実行されます。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_DISABLESQM"></a><a id="debug_engopt_disablesqm"></a><dl>
<dt><b>DEBUG_ENGOPT_DISABLESQM</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>ソフトウェア Quality Metrics (SQM) のデータのアップロードを無効にします。</p>
</td>
</tr>
</table>


<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">DbgEng.h (DbgEng.h を含む)</td>
</tr>
</tbody>
</table>

 
