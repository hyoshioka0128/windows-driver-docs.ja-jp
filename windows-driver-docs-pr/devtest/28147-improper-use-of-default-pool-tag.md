---
title: C28147
description: 警告 C28147 既定プール タグの使用 (' kdD' または 'mdW') のこの関数の呼び出しのプールがタグ付けの目的が果たせなくなります。
ms.assetid: 4838b006-349e-45d1-8ac3-42cbf0d880b7
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28147
ms.openlocfilehash: c7f1ec8ad87abc76898da94ced4c9bc4ea1fe270
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553983"
---
# <a name="c28147"></a>C28147


C28147 を警告します。既定のプール タグの使用 (' kdD' または 'mdW') のこの関数の呼び出しのプールがタグ付けの目的が果たせなくなります

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>これは、ExAllocatePool を直接使用によって発生する可能性があります。 またはタグをマクロからコピーすることがあります。 いずれの場合も、一意のタグが付いた exallocatepoolwithtag に (など) を使用してください。</p></td>
</tr>
</tbody>
</table>

 

ドライバーは、既定のプール タグを指定します。 システムでは、プール タグを使用してプールの使用を追跡しているため、プールの一意のタグを使用するドライバーだけは識別しのプールの使用を区別できます。

**ExAllocatePool**と**ExAllocatePoolWithQuota**が廃止され、置き換えられる[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)と[ **ExAllocatePoolWithQuotaTag**](https://msdn.microsoft.com/library/windows/hardware/ff544513)プールの一意のタグを指定できます。

 

 





