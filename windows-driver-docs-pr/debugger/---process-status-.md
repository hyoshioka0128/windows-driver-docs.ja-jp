---
title: (プロセスの状態)
description: パイプ () のコマンドは、指定されたプロセスまたは現在デバッグ中のすべてのプロセスの状態を表示します。(システム状態) コマンドを使用してこのコマンドを混同しないでください。
ms.assetid: 78f53049-e949-4431-b6b1-0710da047ced
keywords:
- (プロセスの状態)Windows デバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Process Status)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3af3ba4af34516df61e3826e759be964c495f3e2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334847"
---
# <a name="-process-status"></a>| (プロセスの状態)


パイプ (**|**) コマンドは、指定したプロセスの状態を表示します。 または、現在デバッグ中のすべてが処理します。

このコマンドを混同しないでください、 [ **| |(システム状態)** ](----system-status-.md)コマンド。

```dbgcmd
    | Process
```

## <a name="span-idddkcmdprocessstatusdbgspanspan-idddkcmdprocessstatusdbgspanparameters"></a><span id="ddk_cmd_process_status_dbg"></span><span id="DDK_CMD_PROCESS_STATUS_DBG"></span>パラメーター


<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span> *プロセス*   
表示するプロセスを指定します。 このパラメーターを省略した場合は、デバッグしているすべてのプロセスが表示されます。 構文の詳細については、次を参照してください。[プロセス構文](process-syntax.md)します。

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

表示するためのプロセスとスレッドを制御するには、他の方法と詳細については、次を参照してください。[を制御するプロセスとスレッド](controlling-processes-and-threads.md)します。

<a name="remarks"></a>注釈
-------

プロセスは、ユーザー モードでのみ指定できます。

多くのコマンドの前にプロセスのシンボルを追加することができます。 パイプの意味の詳細については (**|**) 後、コマンド、コマンド自体のエントリを参照してください。

デバッグ セッションを起動したときに、子プロセスのデバッグを有効にした場合を除き、デバッガーの使用可能な 1 つだけのプロセスがあります。

次の例では、このコマンドを使用する方法を示します。 次のコマンドは、すべてのプロセスを表示します。

```dbgcmd
2:005> |
```

次のコマンドでは、すべてのプロセスも表示されます。

```dbgcmd
2:005> |*
```

次のコマンドは、現在アクティブなプロセスを表示します。

```dbgcmd
2:005> |.
```

次のコマンドは、最初の例外の原因となった (または、デバッガーが最初に接続されている) プロセスを表示します。

```dbgcmd
2:005> |#
```

次のコマンドは、プロセス数 2 を表示します。

```dbgcmd
2:005> |2
```

前のコマンドでは、次の出力が表示されます。

```dbgcmd
0:002> |
#  0 id: 224   name: myprog.exe 
   1 id: 228   name: onechild.exe 
. 2 id: 22c   name: anotherchild.exe 
```

この出力の最初の行で 0 には、プロセスの 10 進数、224 は 16 進数のプロセス ID、および*Myprog.exe*プロセスのアプリケーションの名前です。 ピリオド (.) プロセス 2 はことを意味する前にこのプロセスは、現在のプロセスです。 シャープ記号 (\#) 前に、プロセス 0 は、このプロセスが最初の例外が発生したかをデバッガーがアタッチされていることを意味します。

 

 





