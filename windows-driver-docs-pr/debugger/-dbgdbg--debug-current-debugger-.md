---
title: .dbgdbg (現在のデバッガーのデバッグ)
description: .Dbgdbg コマンドは、CDB; の新しいインスタンスを起動します。現在のデバッガーは、この新しいデバッガーは、そのターゲットとして受け取ります。
ms.assetid: a90392b5-d8ae-495d-8074-060e4ec89037
keywords:
- .dbgdbg (現在のデバッガーをデバッグする) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .dbgdbg (Debug Current Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 20c74ab6390a7a18b07aee3df31d3456691ab24d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336889"
---
# <a name="dbgdbg-debug-current-debugger"></a>.dbgdbg (現在のデバッガーのデバッグ)


**.Dbgdbg** CDB の新しいインスタンスを起動するコマンドは、この新しいデバッガーはそのターゲットとしての現在のデバッガーです。

```dbgcmd
.dbgdbg 
```

## <span id="ddk_meta_debug_current_debugger_dbg"></span><span id="DDK_META_DEBUG_CURRENT_DEBUGGER_DBG"></span>


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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**.Dbgdbg**コマンドと似ています、 [ **CTRL + P (現在のデバッガーのデバッグ)** ](ctrl-p--debug-current-debugger-.md)コントロール キー。 ただし、 **.dbgdbg** WinDbg だけでなく KD、CDB から使用でき、リモート コンピューター上のデバッグ サーバーをデバッグするために使用できるため、用途が広く、です。

 

 





