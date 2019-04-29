---
title: .tss (タスク状態セグメントの表示)
description: .Tss コマンドでは、現在のプロセッサの保存されているタスクの状態のセグメント (TSS) 情報の書式設定されたビューが表示されます。
ms.assetid: 3f73b7cf-56a8-434a-bc4d-2e8ab3af9f94
keywords:
- タスクの状態のセグメント (.tss) コマンドが表示されます。
- タスクの状態のセグメント (TSS)
- TSS (タスクの状態の分割)
- .tss (タスクの表示状態セグメント) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .tss (Display Task State Segment)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 66f233b2fea635695b7403e3c2a1851b71ba9852
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334173"
---
# <a name="tss-display-task-state-segment"></a>.tss (タスク状態セグメントの表示)


**.Tss**コマンドには、現在のプロセッサの保存されているタスクの状態のセグメント (TSS) 情報の書式設定されたビューが表示されます。

```dbgcmd
.tss [Address]
```

## <a name="span-idddkmetadisplaytaskstatesegmentdbgspanspan-idddkmetadisplaytaskstatesegmentdbgspanparameters"></a><span id="ddk_meta_display_task_state_segment_dbg"></span><span id="DDK_META_DISPLAY_TASK_STATE_SEGMENT_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
TSS のアドレス。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モードのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>x86 のみ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

出力を調べることで、TSS のアドレスが見つかりません、 [ **! pcr** ](-pcr.md)拡張機能。

 

 





