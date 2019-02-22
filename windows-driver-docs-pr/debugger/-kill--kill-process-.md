---
title: .kill (kill プロセス)
description: ユーザー モードでは、.kill コマンドは、デバッグ対象プロセスを終了します。
ms.assetid: e4bc13e4-2566-4438-9ae7-a5ba05b727de
keywords:
- .kill (kill プロセス) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .kill (Kill Process)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a3940664ca0131d87aa42b23ffd6e99fca9c6d36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535596"
---
# <a name="kill-kill-process"></a>.kill (kill プロセス)


ユーザー モードで、 **.kill**コマンドは、デバッグ中のプロセスを終了します。

カーネル モードで、 **.kill**コマンドは、ターゲット コンピューター上のプロセスを終了します。

ユーザー モードの構文

```dbgcmd
.kill [ /h | /n ]
```

カーネル モードの構文

```dbgcmd
.kill Process 
```

## <a name="span-idddkmetakillprocessdbgspanspan-idddkmetakillprocessdbgspanparameters"></a><span id="ddk_meta_kill_process_dbg"></span><span id="DDK_META_KILL_PROCESS_DBG"></span>パラメーター


<span id="________h______"></span><span id="________H______"></span> **/h**   
(ユーザー モードのみ)未処理のデバッグ イベントは続きし、処理済みとしてマークします。 これが既定値です。

<span id="________n______"></span><span id="________N______"></span> **/n**   
(ユーザー モードのみ)処理済みとしてマークしなくても、未処理のデバッグ イベントが引き続き行われます。

<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span> *プロセス*   
終了するプロセスのアドレスを指定します。 場合*プロセス*を省略するか、0 の場合は、現在のシステム状態が終了するため、既定のプロセス。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

カーネル モードでこのコマンドは、Microsoft Windows Server 2003 および Windows の以降のバージョンでサポートされます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ユーザー モードでは、このコマンドは、デバッグ対象プロセスを終了します。 使用することができる場合、子プロセスにデバッガーをアタッチすると、 **.kill**を親プロセスを終了せずに、子プロセスを終了します。 詳細については、例を参照してください。

カーネル モードでは、このコマンドは、終了の対象コンピュータで選択したプロセスをスケジュールします。 次回のターゲットが実行できます (などを使用して、 [ **g (移動)** ](g--go-.md)コマンド)、指定されたプロセスが終了しました。

このコマンドは、ローカル カーネル デバッグ中に使用することはできません。

<a name="examples"></a>例
--------

**.Childdbg を使用します。**

子プロセスを作成する前に、親プロセス (Parent.exe) にデバッガーをアタッチするとします。 コマンドを入力する[ **.childdbg 1** ](-childdbg--debug-child-processes-.md)親を作成する子プロセスにアタッチするデバッガーに指示します。

```dbgcmd
1:001> .childdbg 1
Processes created by the current process will be debugged
```

ここで親プロセスを実行し、子プロセスが作成した後中断するようにします。 使用して、 [ **|(プロセスの状態)** ](---process-status-.md)コマンドを親と子プロセスのプロセスの番号を参照してください。

```dbgcmd
0:002> |*
.  0    id: 7f8 attach  name: C:\Parent\x64\Debug\Parent.exe
   1    id: 2d4 child   name: notepad.exe
```

上記の出力では、子プロセス (notepad.exe) の数は 1 です。 最初の行の先頭にドット (.) は、親プロセスが現在のプロセスであることを指示します。 子の現在のプロセスを処理するために、次のように入力します。 **| 1 s**します。

```dbgcmd
0:002> |1s
...
1:001> |*
#  0    id: 7f8 attach  name: C:\Parent\x64\Debug\Parent.exe
.  1    id: 2d4 child   name: notepad.exe
```

子プロセスを強制終了するコマンドを入力 **.kill**します。 親プロセスが実行を続けます。

```dbgcmd
1:001> .kill
Terminated.  Exit thread and process events will occur.
1:001> g
```

**-O パラメーターを使用します。**

使用することができます、WinDbg または CDB を開始するときに、 **-o**子プロセスにアタッチする必要があります、ことをデバッガーに指示するパラメーター。 たとえば、次のコマンドは、WinDbg を起動し、Parent.exe にアタッチしますを開始します。 Parent.exe 子プロセスを作成するとき、WinDbg は子プロセスにアタッチします。

**windbg -g -G -o Parent.exe**

詳細については、次を参照してください。 [ **WinDbg コマンド ライン オプション**](windbg-command-line-options.md)と[ **CDB コマンド ライン オプション**](cdb-command-line-options.md)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>バージョン:(Kernel mode) 以降 Windows Server 2003 ではサポートされています。</p></td>
</tr>
</tbody>
</table>

 

 





