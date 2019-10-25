---
title: C28147
description: 警告 C28147 この関数の呼び出しに既定のプールタグ (' kdD ' または ' .Mdw ') を使用すると、プールタグ付けの目的が損なわれます。
ms.assetid: 4838b006-349e-45d1-8ac3-42cbf0d880b7
keywords:
- ドライバーの WDK PREfast の一覧に警告が表示される
- ドライバーの WDK PREfast の一覧にエラーが表示される
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28147
ms.openlocfilehash: 6a7ae7e4e2ad5234ff93b40e23618609dcea0ea6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840314"
---
# <a name="c28147"></a>C28147


警告 C28147: この関数の呼び出しに既定のプールタグ (' kdD ' または ' .Mdw ') を使用すると、プールタグ付けの目的が損なわれます

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>これは、ExAllocatePool を直接使用するか、そのマクロからタグがコピーされている可能性があります。 どのような場合でも、一意のタグと共に ExAllocatePoolWithTag (など) を使用する必要があります。</p></td>
</tr>
</tbody>
</table>

 

ドライバーは、既定のプールタグを指定しています。 プールの使用はプールタグによって追跡されるので、一意のプールタグを使用するドライバーのみがプールの使用を識別し、区別することができます。

**Exallocatepool**と**Exallocatepoolwithquota**は互換性のために残されています。一意のプールタグを指定できるようにするには、 [**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)と[**Exallocatepoolwithquotatag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag)で置き換える必要があります。

 

 





