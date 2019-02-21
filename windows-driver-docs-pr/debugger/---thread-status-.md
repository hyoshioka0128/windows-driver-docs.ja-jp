---
title: ~ (スレッドの状態)
description: チルダ (~) コマンドでは、現在のプロセスで指定したスレッドまたはすべてのスレッドの状態が表示されます。
ms.assetid: c27e4c72-86da-459d-833f-d27d26bdea0e
keywords:
- ~ (スレッド ステータス) Windows のデバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- ~ (Thread Status)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 42c87cbfb06cd0afb50b2f1da6275ecfea8dfe77
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535487"
---
# <a name="-thread-status"></a>~ (スレッドの状態)


チルダ (**~**) コマンドは、現在のプロセスで指定したスレッドまたはすべてのスレッドの状態を表示します。

```dbgcmd
~ Thread
```

## <a name="span-idddkcmdthreadstatusdbgspanspan-idddkcmdthreadstatusdbgspanparameters"></a><span id="ddk_cmd_thread_status_dbg"></span><span id="DDK_CMD_THREAD_STATUS_DBG"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
表示するスレッドを指定します。 このパラメーターを省略した場合は、すべてのスレッドが表示されます。 構文の詳細については、次を参照してください。[スレッド構文](thread-syntax.md)します。

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

スレッドは、ユーザー モードでのみ指定できます。 カーネル モードで、チルダ (**~**) プロセッサを参照します。

多くのコマンドの前にスレッドのシンボルを追加できます。 チルダの意味の詳細については (**~**) 後、コマンド、コマンド自体のエントリを参照してください。

次の例では、このコマンドを使用する方法を示します。 次のコマンドは、すべてのスレッドを表示します。

```dbgcmd
0:001> ~
```

次のコマンドでは、すべてのスレッドも表示されます。

```dbgcmd
0:001> ~*
```

次のコマンドは、現在アクティブなスレッドを表示します。

```dbgcmd
0:001> ~.
```

次のコマンドは、最初の例外の原因となった (または、プロセスにデバッガーがアタッチされている場合にアクティブだった) のスレッドを表示します。

```dbgcmd
0:001> ~#
```

次のコマンドは、スレッド数 2 を表示します。

```dbgcmd
0:001> ~2
```

前のコマンドでは、次の出力が表示されます。

```dbgcmd
0:001> ~
   0 id: 4dc.470 Suspend: 0 Teb 7ffde000 Unfrozen
. 1 id: 4dc.534 Suspend: 0 Teb 7ffdd000 Unfrozen
#  2 id: 4dc.5a8 Suspend: 0 Teb 7ffdc000 Unfrozen
```

この出力の最初の行では 0、10 進数のスレッド数、4DC は 16 進数のプロセス ID、470 は 16 進数のスレッド ID、0x7FFDE000 は TEB のアドレスと**保持を解除**スレッドの状態します。 スレッド 1 の前にピリオド (.) は、このスレッドは、現在のスレッドを意味します。 シャープ記号 (\#) スレッド 2 は、このスレッドが最初の例外が発生したか、アクティブであったことを意味する前に、デバッガー アタッチされている場合、プロセスにします。

 

 





