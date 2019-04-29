---
title: ~f (スレッドの凍結)
description: ~ F コマンドが停止し、固定が解除されるまで待機する原因と、特定のスレッドがフリーズします。F (塗りつぶしメモリ) のコマンドでは、このコマンドを混同しないでください。
ms.assetid: 86fbbcee-c752-4425-a330-4d95a4069b0d
keywords:
- ~ f (スレッドを凍結) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~f (Freeze Thread)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fe2de154ad16c54c4a465491a19bccbad4bddd22
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334480"
---
# <a name="f-freeze-thread"></a>~f (スレッドの凍結)


**~ F**コマンドが停止し、固定が解除されるまで待機する原因と、特定のスレッドがフリーズします。

このコマンドを混同しないでください、 [ **f (塗りつぶしメモリ)** ](f--fp--fill-memory-.md)コマンド。

```dbgcmd
~Thread f 
```

## <a name="span-idddkcmdfreezethreaddbgspanspan-idddkcmdfreezethreaddbgspanparameters"></a><span id="ddk_cmd_freeze_thread_dbg"></span><span id="DDK_CMD_FREEZE_THREAD_DBG"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
スレッドの凍結を指定します。 構文の詳細については、次を参照してください。[スレッド構文](thread-syntax.md)します。

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

**~ F**コマンドにより、指定されたスレッドを固定します。 デバッガーは、実行を再開する対象のアプリケーションで、他のスレッドは、このスレッドが停止中に期待どおりを実行します。

次の例では、このコマンドを使用する方法を示します。 次のコマンドは、すべてのスレッドの現在の状態を表示します。

```dbgcmd
0:000> ~* k
```

次のコマンドは、現在の例外の原因となったスレッドを停止します。

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

 

 





