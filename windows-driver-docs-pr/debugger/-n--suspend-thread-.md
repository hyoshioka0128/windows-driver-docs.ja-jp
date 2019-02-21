---
title: ~ n (スレッドを中断する)
description: ~ N 個のコマンドは、指定したスレッドの実行を中断します。N (設定数の基本) コマンドを使用してこのコマンドを混同しないでください。
ms.assetid: 4b1063ad-edba-4cd3-9084-dc6c08c69f55
keywords:
- ~ n (スレッドを中断) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~n (Suspend Thread)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 64c0026bbc37a027ca11865800c1e28e1381f701
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530468"
---
# <a name="n-suspend-thread"></a>~ n (スレッドを中断する)


**~ N**コマンドは、指定したスレッドの実行を中断します。

このコマンドを混同しないでください、 [ **n (設定数の基本)** ](n--set-number-base-.md)コマンド。

```dbgcmd
~Thread n 
```

## <a name="span-idddkcmdsuspendthreaddbgspanspan-idddkcmdsuspendthreaddbgspanparameters"></a><span id="ddk_cmd_suspend_thread_dbg"></span><span id="DDK_CMD_SUSPEND_THREAD_DBG"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
スレッドまたはスレッドを中断するを指定します。 構文の詳細については、次を参照してください。[スレッド構文](thread-syntax.md)します。

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
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

中断の詳細についてはカウントとどのように中断されたスレッドの動作し、中断とスレッドの固定を制御するその他のコマンドの一覧は、次を参照してください。[を制御するプロセスとスレッド](controlling-processes-and-threads.md)します。

<a name="remarks"></a>注釈
-------

スレッドは、ユーザー モードでのみ指定できます。 カーネル モードではチルダ (~) は、プロセッサを表します。

使用するたびに、 **~ n**コマンド、スレッドの中断カウントが 1 増加します。

このコマンドを使用する場合は、スレッドの開始アドレスが表示されます。

 

 





