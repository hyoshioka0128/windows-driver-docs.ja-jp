---
title: ~u (スレッドの凍結解除)
description: ~、指定されたスレッドの凍結を u コマンド。U (Unassemble) コマンドを使用してこのコマンドを混同しないでください。
ms.assetid: 6ac3c84a-3734-4b16-a239-4233e186c2df
keywords:
- ~ u (スレッドを解放) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~u (Unfreeze Thread)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f1a6a3486589d110713195e82536b06ba07b7f68
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334172"
---
# <a name="u-unfreeze-thread"></a>~u (スレッドの凍結解除)


**~ U**コマンドは、指定したスレッドを凍結します。

このコマンドを混同しないでください、 [ **U (Unassemble)** ](u--unassemble-.md)コマンド。

```dbgcmd
~Thread u 
```

## <a name="span-idddkcmdunfreezethreaddbgspanspan-idddkcmdunfreezethreaddbgspanparameters"></a><span id="ddk_cmd_unfreeze_thread_dbg"></span><span id="DDK_CMD_UNFREEZE_THREAD_DBG"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
固定解除するスレッドを指定します。 構文の詳細については、次を参照してください。[スレッド構文](thread-syntax.md)します。

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

どの凍結されたスレッドの詳細については次のように動作します。 および、固定を制御するその他のコマンドの一覧と、スレッドの中断を参照してください。[を制御するプロセスとスレッド](controlling-processes-and-threads.md)します。

<a name="remarks"></a>注釈
-------

スレッドは、ユーザー モードでのみ指定できます。 カーネル モードではチルダ (~) は、プロセッサを表します。

次の例は、使用する方法を表示、~ コマンド。

次のコマンドは、すべてのスレッドの現在の状態を表示します。

```dbgcmd
0:000> ~* k
```

次のコマンドは、現在の例外の原因となったスレッドを凍結します。

```dbgcmd
0:000> ~# f
```

次のコマンドは、このスレッドの状態が中断されているかを確認します。

```dbgcmd
0:000> ~* k
```

次のコマンドは、スレッド番号 123 を解除します。

```dbgcmd
0:000> ~123 u
```

 

 





