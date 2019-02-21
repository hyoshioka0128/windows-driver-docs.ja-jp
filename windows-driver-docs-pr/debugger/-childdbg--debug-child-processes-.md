---
title: .childdbg (子プロセスのデバッグ)
description: .Childdbg コマンドでは、子プロセスのデバッグを制御します。
ms.assetid: 87d70d3b-d9d5-4a37-b8a7-1616ba78b2f3
keywords:
- .childdbg (子プロセスのデバッグ) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .childdbg (Debug Child Processes)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 83df9291f16ec69bc8a1286e5d098fc77352e44b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549417"
---
# <a name="childdbg-debug-child-processes"></a>.childdbg (子プロセスのデバッグ)


**.Childdbg**コマンドは、子プロセスのデバッグを制御します。

```dbgsyntax
.childdbg 0 
.childdbg 1 
.childdbg 
```

## <a name="span-idddkmetadebugchildprocessesdbgspanspan-idddkmetadebugchildprocessesdbgspanparameters"></a><span id="ddk_meta_debug_child_processes_dbg"></span><span id="DDK_META_DEBUG_CHILD_PROCESSES_DBG"></span>パラメーター


<span id="_______0______"></span> **0**   
デバッガーが子プロセスをデバッグするを防ぎます。

<span id="_______1______"></span> **1**   
子プロセスをデバッグするデバッガーをによりします。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

このコマンドは、Windows XP および Windows の以降のバージョンでのみサポートされます。

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
<td align="left"><p>x86、x64、および Itanium のみ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**子プロセスが**追加の処理を元のターゲット アプリケーションを起動します。

パラメーターなしで **.childdbg**子プロセスのデバッグの現在の状態が表示されます。

 

 





