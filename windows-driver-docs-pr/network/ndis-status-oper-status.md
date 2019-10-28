---
title: NDIS_STATUS_OPER_STATUS
description: NDIS_STATUS_OPER_STATUS の状態は、その後のドライバーに対する NDIS ネットワークインターフェイスの現在の動作状態を示します。
ms.assetid: dbe7ce19-290d-4a48-a6c2-1b95e956c26c
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_OPER_STATUS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 842a418b663666fe1642263a80496ec31b21bf57
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842777"
---
# <a name="ndis_status_oper_status"></a>NDIS\_STATUS\_OPER\_STATUS


NDIS\_STATUS\_OPER\_STATUS status は、NDIS ネットワークインターフェイスの現在の動作状態を、それまでのドライバーに示します。

<a name="remarks"></a>注釈
-------

NDIS は、この状態の表示を生成します。NDIS ミニポートドライバーは、この状態の表示を生成しません。

Ndis は、ndis [ **\_STATUS\_示さ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)れる構造体の**statusbuffer**メンバーに、 [**ndis\_OPER\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_oper_state)構造体を提供します。

[**Ndis\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**statusbuffersize**メンバーが SIZEOF (NDIS\_OPER\_STATE) に設定されています。

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
<td><p>NDIS 6.0 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OPER\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_oper_state)

[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

 

 




