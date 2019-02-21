---
title: 初期のクリティカル セクション イベントの作成
description: 初期のクリティカル セクション イベントの作成
ms.assetid: a9453e6d-7566-4226-a950-d32d6192f8ac
keywords:
- 初期クリティカル セクション イベントの作成 (グローバル フラグ)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6d9cfcae920046584bf2decab62f48649ed7a77
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552907"
---
# <a name="early-critical-section-event-creation"></a>初期のクリティカル セクション イベントの作成


## <span id="ddk_early_critical_section_event_creation_dtools"></span><span id="DDK_EARLY_CRITICAL_SECTION_EVENT_CREATION_DTOOLS"></span>


**クリティカル セクション イベントの事前作成**イベントが必要になるまで待機ではなく、クリティカル セクションが初期化されると、イベントのハンドルをフラグが作成されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>cse</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x10000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_CRITSEC_EVENT_CREATION</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>変換先</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ、カーネルのフラグ、イメージ ファイルのレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

イベントを作成できないのは、Windows、初期化中に例外が生成され、enter および leave クリティカル セクションへの呼び出しが失敗しません。

このフラグは、大量の非ページ プール メモリを使用するための十分なメモリが非常に信頼性の高いシステムでのみ使用できます。

 

 





