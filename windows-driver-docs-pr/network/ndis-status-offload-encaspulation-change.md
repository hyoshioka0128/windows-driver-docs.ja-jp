---
title: NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE
description: ミニポート ドライバーでは、カプセル化設定の変更があった NDIS と関連付けたドライバーに通知するのに、NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE 状態を示す値を使用します。
ms.assetid: 2db2a42e-85a2-41a6-b6ab-13b493057648
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 11c0078f342297f19958da8cc173225fcd650b6f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560228"
---
# <a name="ndisstatusoffloadencaspulationchange"></a>NDIS\_状態\_オフロード\_カプセル化\_変更


ミニポート ドライバーを使用して、NDIS\_状態\_オフロード\_カプセル化\_カプセル化設定の変更があった NDIS と関連付けたドライバーに通知する状態表示を変更します。

<a name="remarks"></a>注釈
-------

**StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造に含まれる、 [ **NDIS\_オフロード\_カプセル化**](https://msdn.microsoft.com/library/windows/hardware/ff566702)構造体。 NDIS\_オフロード\_カプセル化をカプセル化の設定を指定します。

カプセル化設定の詳細については、[OID\_オフロード\_カプセル化](https://msdn.microsoft.com/library/windows/hardware/ff569762)を参照してください。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.0 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_オフロード\_カプセル化**](https://msdn.microsoft.com/library/windows/hardware/ff566702)

[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[OID\_オフロード\_カプセル化](https://msdn.microsoft.com/library/windows/hardware/ff569762)

 

 




