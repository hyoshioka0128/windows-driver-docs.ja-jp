---
title: C28751
description: 警告 C28751 では、ExAllocatePool とそのバリエーションの使用が禁止されています。
ms.assetid: A2FBEDA8-FA5D-42A5-B298-FF0A32B1662C
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28751
ms.openlocfilehash: f2e329c09f5c018cf8d52e9a8938d7cf426ae7af
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839589"
---
# <a name="c28751"></a>C28751


警告 C28751: ExAllocatePool とそのバリエーションの禁止された使用

この警告は、関数が使用されていて、その機能が使用されていないことを示しています。これは、より堅牢で安全な代替手段です。

カーネルメモリ割り当て関数 ExAllocatePool と ExAllocatePoolWithQuota には、後のデバッグに役立つタグが用意されていません。 これらの関数には、デバッグを容易にするために使用できる置換があります。

代替機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">API</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="ExAllocatePool"></span><span id="exallocatepool"></span><span id="EXALLOCATEPOOL"></span>ExAllocatePool</p></td>
<td align="left"><p>セキュリティで保護された置換: <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)"> <strong>Exallocatepoolwithtag</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ExAllocatePoolWithQuota"></span><span id="exallocatepoolwithquota"></span><span id="EXALLOCATEPOOLWITHQUOTA"></span>ExAllocatePoolWithQuota</p></td>
<td align="left"><p>セキュリティで保護された置換: <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithQuotaTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag)"><strong>Exallocatepoolwithquotatag</strong></a>ルーチン</p></td>
</tr>
</tbody>
</table>

 

 

 





