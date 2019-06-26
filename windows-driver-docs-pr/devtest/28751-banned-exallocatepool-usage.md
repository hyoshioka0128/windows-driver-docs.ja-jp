---
title: C28751
description: ExAllocatePool とそのバリエーションの C28751 禁止の使用状況を警告します。
ms.assetid: A2FBEDA8-FA5D-42A5-B298-FF0A32B1662C
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28751
ms.openlocfilehash: 39dc9d7d8627644b8cf2729edf7769c784dca865
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371704"
---
# <a name="c28751"></a>C28751


C28751 を警告します。ExAllocatePool とそのバリエーションの禁止された使用状況

この警告は、関数が使用されていることを禁止されておりより堅牢でセキュリティで保護された交換を示します。

ExAllocatePool と ExAllocatePoolWithQuota カーネル メモリ割り当て関数では、後でデバッグを支援するタグは提供されません。 これらの関数を使用することができますが、デバッグが簡単に交換があります。

代替

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
<td align="left"><p>セキュリティで保護された交換:<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)"><strong>Exallocatepoolwithtag に</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ExAllocatePoolWithQuota"></span><span id="exallocatepoolwithquota"></span><span id="EXALLOCATEPOOLWITHQUOTA"></span>ExAllocatePoolWithQuota</p></td>
<td align="left"><p>セキュリティで保護された交換:<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithquotatag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithQuotaTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithquotatag)"><strong>ExAllocatePoolWithQuotaTag</strong> </a>ルーチン</p></td>
</tr>
</tbody>
</table>

 

 

 





