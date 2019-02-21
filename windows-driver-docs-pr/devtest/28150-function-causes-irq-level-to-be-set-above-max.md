---
title: C28150
description: 警告 C28150 関数はによって分析対象の関数の許容最大値より大きい設定する IRQ レベルです。
ms.assetid: 7ad53801-fa7f-49c1-a1f0-715c9f4951d1
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28150
ms.openlocfilehash: d1ff92b9b831a75c62a5422b823f7bc91fce19b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536523"
---
# <a name="c28150"></a>C28150


C28150 を警告します。関数によって、IRQ レベルを分析する関数の許容最大値より大きい設定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>レベルの制限が、現在の関数上の注釈から取得します。</p></td>
</tr>
</tbody>
</table>

 

指定された関数は IRQL が現在の関数呼び出しで許可される最大値より大きい IRQL を発生します。

注釈を付けている関数内でこの警告が発生した、  **\_ \_drv\_maxIRQL**注釈関数のコーディング エラーまたはの誤解のいずれかを示し、注釈での関数のコントラクト。

 

 





