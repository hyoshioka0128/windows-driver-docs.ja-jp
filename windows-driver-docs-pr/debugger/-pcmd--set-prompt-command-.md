---
title: .pcmd (プロンプトの set コマンド)
description: .Pcmd コマンドでは、登録またはターゲットの状態情報を含むデバッガー コマンド ウィンドウで、プロンプトを表示して、ターゲットの実行が停止されるたびに、コマンドを実行するデバッガーを実行します。
ms.assetid: 8cda10c3-860c-453d-9fdd-0dfc74d71c53
keywords:
- .pcmd (Prompt コマンドのセット) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .pcmd (Set Prompt Command)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 25113801956a4519271aca0743b6dbfa9ffa6b2b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552345"
---
# <a name="pcmd-set-prompt-command"></a>.pcmd (プロンプトの set コマンド)


**.Pcmd**コマンドにより、デバッガーでプロンプトを表示して、ターゲットの実行が停止されるたびに、コマンドを実行する、[デバッガー コマンド ウィンドウ](debugger-command-window.md)登録またはターゲットの状態情報を使用します。

```dbgcmd
.pcmd -s CommandString 
.pcmd -c 
.pcmd 
```

## <a name="span-idddkmetasetpromptcommanddbgspanspan-idddkmetasetpromptcommanddbgspanparameters"></a><span id="ddk_meta_set_prompt_command_dbg"></span><span id="DDK_META_SET_PROMPT_COMMAND_DBG"></span>パラメーター


<span id="_______-s_______CommandString______"></span><span id="_______-s_______commandstring______"></span><span id="_______-S_______COMMANDSTRING______"></span> **-s** **** *クラスヒント*   
新しいコマンド プロンプト文字列を指定します。 たびに、ターゲットは実行すると、デバッガーの問題を停止し、すぐに実行、*クラスヒント*コマンド。 場合*クラスヒント*スペースや、セミコロンが含まれていますが、引用符で囲む必要があります。

<span id="_______-c______"></span><span id="_______-C______"></span> **-c**   
既存のプロンプトのコマンド文字列を削除します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

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
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

デバッガー コマンド ウィンドウのプロンプトの詳細については、[デバッガー コマンドを使用して](using-debugger-commands.md)を参照してください。

<a name="remarks"></a>注釈
-------

使用する場合、 **.pcmd**パラメーターを指定せずコマンドの現在のプロンプトのコマンドが表示されます。

使用してコマンド プロンプトを設定すると **.pcmd-s**、指定した*クラスヒント*ターゲットの実行が停止されるたびに発行されます (場合など、 [ **g**](g--go-.md)、 [ **p**](p--step-.md)、または[ **t** ](t--trace-.md)コマンドが終了)。 *クラスヒント*コマンドが発行されません非実行コマンドを使用する場合に限り、そのコマンドは、レジスタまたはターゲットの状態情報が表示されます。

次の例では、最初の使用の **.pcmd**プロンプトが表示される固定文字列を設定します。 第 2 の用途の **.pcmd**デバッガーが、ターゲットの現在のプロセス ID を表示し、スレッド ID、プロンプトが表示されるたびにします。 後は、特別なプロンプトが表示されない、 [ **.ttime** ](-ttime--display-thread-times-.md)そのコマンドが実行を含まないため、コマンドを使用します。

```dbgcmd
0:000> .pcmd
No per-prompt command

0:000> .pcmd -s ".echo Execution is done."
Per-prompt command is '.echo Execution is done.'

0:000> t
Prymes!isPrime+0xd0:
004016c0 837dc400      cmp dword ptr [ebp-0x3c],0x0 ss:0023:0012fe70=00000002
Execution is done.

0:000> t
Prymes!isPrime+0xd4:
004016c4 7507             jnz     Prymes!isPrime+0xdd (004016cd)
 [br=1]
Execution is done.

0:000> .ttime
Created: Thu Aug 21 13:18:59 2003
Kernel:  0 days 0:00:00.031
User:    0 days 0:00:00.000

0:000> .pcmd -s "r $tpid, $tid"
Per-prompt command is 'r $tpid, $tid'

0:000> t
Prymes!isPrime+0xdd:
004016cd ebc0             jmp     Prymes!isPrime+0x9f (0040168f)
$tpid=0000080c $tid=00000514

0:000> t
Prymes!isPrime+0x9f:
0040168f 8b55fc           mov     edx,[ebp-0x4]     ss:0023:0012fea8=00000005
$tpid=0000080c $tid=00000514
```

 

 





