---
title: .event_code (イベント コードの表示)
description: .Event_code コマンドは、現在のイベントの命令を表示します。
ms.assetid: f2ab0f4d-493c-4b8b-a7a0-82c10586d485
keywords:
- .event_code (イベント コードの表示) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .event_code (Display Event Code)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f0badc8a5a9b9befb7fce0e58f054291b755da5e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571299"
---
# <a name="eventcode-display-event-code"></a>イベントに対する\_コード (イベント コードの表示)


**イベントに対する\_コード**コマンドは、現在のイベントの命令を表示します。

```dbgcmd
.event_code 
```

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
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

**イベントに対する\_コード**コマンドは、現在のイベントの命令ポインターで 16 進数の命令を表示します。 表示には、可能な場合、64 バイトまでの手順が含まれます。

 

 





