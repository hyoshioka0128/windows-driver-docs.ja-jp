---
title: NdisOidDoubleRequest ルール (ndis)
description: この NdisOidDoubleRequest ルールでは、ミニポート ドライバーが、NDIS を完了する必要がありますを検証\_OID\_は現在保留中要求。
ms.assetid: 67B179ED-EEAF-4717-B714-9601BE806269
ms.date: 05/21/2018
keywords:
- NdisOidDoubleRequest ルール (ndis)
topic_type:
- apiref
api_name:
- NdisOidDoubleRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 07e91bf84ffbe9e8263d0b024caae355db992ae9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362170"
---
# <a name="ndisoiddoublerequest-rule-ndis"></a>NdisOidDoubleRequest ルール (ndis)


これは、 **NdisOidDoubleRequest**ルールことを確認します。

-   ミニポート ドライバーが完了する必要があります、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)現在保留中です。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x0009100E) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を選択し、 <a href="https://msdn.microsoft.com/library/windows/hardware/dn312128" data-raw-source="[NDIS/WIFI verification](https://msdn.microsoft.com/library/windows/hardware/dn312128)">NDIS/WIFI 検証</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>対象
----------

[**MiniportOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff559416)
[**NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622)
 

 





