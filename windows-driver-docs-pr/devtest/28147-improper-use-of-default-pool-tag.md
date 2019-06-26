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
ms.openlocfilehash: f836334872c5157def7396b87055149c3db3f198
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364108"
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

**ExAllocatePool**と**ExAllocatePoolWithQuota**が廃止され、置き換えられる[ **exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)と[ **ExAllocatePoolWithQuotaTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithquotatag)プールの一意のタグを指定できます。

 

 





