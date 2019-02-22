---
title: C28124
description: 警告 C28124 が呼び出しによって IRQ レベルの分析中の関数で許容される最小値より小さく設定します。
ms.assetid: d0540a52-2252-49d5-ba03-3d026e07670a
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28124
ms.openlocfilehash: 7a6ffe1c8147d9d0bcee51cbf40c46e4166e71e0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529770"
---
# <a name="c28124"></a>C28124


C28124 を警告します。呼び出しによって、IRQ レベルの分析中の関数で許容される最小値より小さく設定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>最低限の法的な IRQL が最後に設定&lt; <em>IRQL</em> &gt;行&lt;<em>行番号</em>&gt;します。 レベルの制限が、現在の関数上の注釈から取得します。</p></td>
</tr>
</tbody>
</table>

 

ドライバーでは、IRQL を関数の現在の型の最小の IRQL 未満のレベルに変更する関数を呼び出します。 コード分析ツールでは、関数の型や注釈からこの情報を推測します。

注釈を付けている関数内でこの警告が発生した、  **\_ \_drv\_minIRQL**注釈関数のコーディング エラーまたはの誤解のいずれかを示し、注釈での関数のコントラクト。

 

 





