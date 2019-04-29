---
title: ~e (スレッド固有のコマンド)
description: ~ E コマンド ターゲット プロセスの特定のスレッド、またはすべてのスレッドは、1 つまたは複数のコマンドを実行します。E (入力の値) のコマンドでは、このコマンドを混同しないでください。
ms.assetid: a14f0a5f-48f9-46dd-baa6-b7d91b15772c
keywords:
- スレッド固有のコマンド (~ e) コマンド
- スレッド、スレッド固有のコマンド (~ e) コマンド
- ~ e (スレッド固有のコマンドで) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~e (Thread-Specific Command)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 35ecb0d499b458c29a6211fe3a16711c72f314be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336791"
---
# <a name="e-thread-specific-command"></a>~e (スレッド固有のコマンド)


**~ E**コマンド ターゲット プロセスの特定のスレッド、またはすべてのスレッドは、1 つまたは複数のコマンドを実行します。

このコマンドを混同しないでください、 [ **e (値を入力)** ](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md)コマンド。

```dbgcmd
~Thread e CommandString
```

## <a name="span-idddkcmdthreadspecificcommanddbgspanspan-idddkcmdthreadspecificcommanddbgspanparameters"></a><span id="ddk_cmd_thread_specific_command_dbg"></span><span id="DDK_CMD_THREAD_SPECIFIC_COMMAND_DBG"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
デバッガーを実行するスレッドを指定します*クラスヒント*の。 構文の詳細については、次を参照してください。[スレッド構文](thread-syntax.md)します。

<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
実行する 1 つまたは複数のコマンドを指定します。 セミコロンを使用して、複数のコマンドを分離する必要があります。 *クラスヒント*入力行の残りの部分が含まれています。 すべての文字"e"に続くテキストは、この文字列の一部として解釈されます。 囲まないで*クラスヒント*引用符で囲んで指定します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでのみ</p></td>
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

スレッドを制御する他のコマンドの詳細については、次を参照してください。[を制御するプロセスとスレッド](controlling-processes-and-threads.md)します。

<a name="remarks"></a>コメント
-------

スレッドは、ユーザー モードでのみ指定できます。 カーネル モードではチルダ (~) は、プロセッサを表します。

使用すると、 **~ e**コマンド 1 つのスレッドと共に、 **~ e**キーボード入力のみ保存されます。 たとえば、次の 2 つのコマンドは同等です。

```dbgcmd
0:000> ~2e r; k; kd 

0:000> ~2r; ~2k; ~2kd 
```

ただし、使用することができます、 **~ e**コマンドまたは拡張機能のコマンドを複数回繰り返して修飾子。 この方法で、修飾子を使用すると、余分な入力を排除することができます。 たとえば、次のコマンドを繰り返し、 [ **! gle** ](-gle.md)デバッグしているすべてのスレッドの拡張機能コマンド。

```dbgcmd
0:000> ~*e !gle 
```

1 つのコマンドの実行でエラーが発生する場合は、次のコマンドを使用して実行が続行されます。

使用することはできません、 **~ e**実行コマンドと共に修飾子 ([**g**](g--go-.md)、 [ **gh**](gh--go-with-exception-handled-.md)、 [**gn**](gn--gn--go-with-exception-not-handled-.md)、 **gN**、 [ **gu**](gu--go-up-.md)、 [ **p** ](p--step-.md)、 [ **pa**](pa--step-to-address-.md)、 [ **pc**](pc--step-to-next-call-.md)、 [ **t**](t--trace-.md)、 [**ta**](ta--trace-to-address-.md)、 [ **tb**](tb--trace-to-next-branch-.md)、 [ **tc**](tc--trace-to-next-call-.md)、 [ **wt**](wt--trace-and-watch-data-.md))。

使用することはできません、 **~ e**修飾子と共に、 [ **j (実行 If-else)** ](j--execute-if---else-.md)または[ **z (実行中に)** ](z--execute-while-.md)条件付きコマンド。

1 つ以上のプロセスをデバッグしている場合は使用できません、 **~ e**コマンドを非アクティブなプロセスの仮想メモリ空間にアクセスします。

 

 





