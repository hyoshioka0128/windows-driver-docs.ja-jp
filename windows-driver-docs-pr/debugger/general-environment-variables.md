---
title: 一般的な環境変数
description: 一般的な環境変数
ms.assetid: 1f37de92-0c62-4317-b3c6-24b3efd9b3b3
keywords:
- 一般的な環境変数
- _NO_DEBUG_HEAP 環境変数
- _NT_ALT_SYMBOL_PATH 環境変数
- _NT_DEBUG_HISTORY_SIZE 環境変数
- _NT_DEBUG_LOG_FILE_APPEND 環境変数
- _NT_DEBUG_LOG_FILE_OPEN 環境変数
- _NT_DEBUGGER_EXTENSION_PATH 環境変数
- _NT_EXECUTABLE_IMAGE_PATH 環境変数
- _NT_SOURCE_PATH 環境変数
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04adc9364db52af5579676fa1da57524c38fe799
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578105"
---
# <a name="general-environment-variables"></a>一般的な環境変数


## <span id="ddk_general_environment_variables_dbg"></span><span id="DDK_GENERAL_ENVIRONMENT_VARIABLES_DBG"></span>


次の表は、ユーザー モードとカーネル モードのデバッグの両方で使用できる環境変数を一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">変数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>_NT_DEBUGGER_EXTENSION_PATH = <em>Path</em></p></td>
<td align="left"><p>デバッガーが最初に拡張 Dll の検索パスを指定します。 <em>パス</em>コロンの後にドライブ文字を含めることができます (<strong>:</strong>)。 複数のディレクトリをセミコロンで区切ります (<strong>;</strong>)。 詳細については、<a href="loading-debugger-extension-dlls.md" data-raw-source="[Loading Debugger Extension DLLs](loading-debugger-extension-dlls.md)">デバッガー拡張 Dll の読み込み</a>を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_EXECUTABLE_IMAGE_PATH = <em>Path</em></p></td>
<td align="left"><p>バイナリの実行可能ファイルを含むパスを指定します。 <em>パス</em>コロンの後にドライブ文字を含めることができます (<strong>:</strong>)。 複数のディレクトリをセミコロンで区切ります (<strong>;</strong>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_SOURCE_PATH = <em>Path</em></p></td>
<td align="left"><p>ターゲットのソース ファイルを含むパスを指定します。 <em>パス</em>コロンの後にドライブ文字を含めることができます (<strong>:</strong>)。 複数のディレクトリをセミコロンで区切ります (<strong>;</strong>)。 詳細については、およびこのパスを変更するには、他の方法については、「<a href="source-path.md" data-raw-source="[Source Path](source-path.md)">ソース パス</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_SYMBOL_PATH = <em>Path</em></p></td>
<td align="left"><p>シンボル ファイルを含むディレクトリ ツリーのルートを指定します。 <em>パス</em>コロンの後にドライブ文字を含めることができます (<strong>:</strong>)。 複数のディレクトリをセミコロンで区切ります (<strong>;</strong>)。 詳細については、およびこのパスを変更するには、他の方法については、「<a href="symbol-path.md" data-raw-source="[Symbol Path](symbol-path.md)">シンボル パス</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_ALT_SYMBOL_PATH = <em>Path</em></p></td>
<td align="left"><p>_NT_SYMBOL_PATH の前に検索、代替のシンボル パスを指定します。 これは、シンボル ファイルのプライベート バージョンを保持する場合に便利です。 <em>パス</em>コロンの後にドライブ文字を含めることができます (<strong>:</strong>)。 複数のディレクトリをセミコロンで区切ります (<strong>;</strong>)。 詳細については、<a href="symbol-path.md" data-raw-source="[Symbol Path](symbol-path.md)">シンボル パス</a>を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_SYMBOL_PROXY =<em>プロキシ</em><strong>:</strong><em>ポート</em></p></td>
<td align="left"><p>SymSrv で使用するプロキシ サーバーを指定します。 詳細については、<a href="firewalls-and-proxy-servers.md" data-raw-source="[Firewalls and Proxy Servers](firewalls-and-proxy-servers.md)">ファイアウォールとプロキシ サーバー</a>を参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_DEBUG_HISTORY_SIZE = <em>Number</em></p></td>
<td align="left"><p>リモート デバッグ中にアクセスできるコマンドの履歴では、コマンドの数を指定します。 使用可能な行の数が一致も一致しないため、コマンドの可変長、<em>数</em>します。 詳細については、およびこの数を変更するには、他の方法については、「<a href="using-debugger-commands.md" data-raw-source="[Using Debugger Commands](using-debugger-commands.md)">デバッガー コマンドを使用して</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_DEBUG_LOG_FILE_OPEN = <em>Filename</em></p></td>
<td align="left"><p>(CDB と KD のみ)デバッガーが、出力を送信するログ ファイルを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_DEBUG_LOG_FILE_APPEND = <em>Filename</em></p></td>
<td align="left"><p>(CDB と KD のみ)デバッガーが出力を追加する必要があります、ログ ファイルを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_EXPR_EVAL = {<strong>masm</strong> | <strong>c++</strong>}</p></td>
<td align="left"><p>既定の式エバリュエーターを指定します。 場合<strong>masm</strong>指定すると、MASM 式の構文が使用されます。 場合<strong>c++</strong>指定すると、C++ 式の構文が使用されます。 MASM 式の構文では、既定値です。 参照してください<a href="evaluating-expressions.md" data-raw-source="[Evaluating Expressions](evaluating-expressions.md)">を評価する式</a>詳細についてはします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NO_DEBUG_HEAP</p></td>
<td align="left"><p>ユーザー モード デバッグのデバッグ ヒープを使用しないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBGENG_NO_DEBUG_PRIVILEGE</p></td>
<td align="left"><p>継承 SeDebugPrivilege デバッガーにより生成されたプロセスをできないようにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBGENG_NO_BUGCHECK_ANALYSIS</p></td>
<td align="left"><p>自動バグチェック分析をできないようにします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBGHELP_HOMEDIR</p></td>
<td align="left"><p>SymSrv と SrcSrv で使用される既定のダウン ストリームのストアのルートのパスを指定します。 <em>パス</em>コロンの後にドライブ文字を含めることができます (<strong>:</strong>)。 複数のディレクトリをセミコロンで区切ります (<strong>;</strong>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SRCSRV_INI_FILE</p></td>
<td align="left"><p>使用される構成ファイルの名前とパスを指定します<a href="srcsrv.md" data-raw-source="[SrcSrv](srcsrv.md)">SrcSrv</a>します。 既定では、パスは、Windows のツールをデバッグ インストール ディレクトリの srcsrv サブディレクトリとファイル名は、Srcsrv.ini します。 参照してください<a href="source-indexing.md" data-raw-source="[Source Indexing](source-indexing.md)">ソースのインデックス作成</a>詳細についてはします。</p></td>
</tr>
</tbody>
</table>

 

 

 





