---
title: NDIS_STATUS_MEDIA_SPECIFIC_INDICATION
description: NDIS_STATUS_MEDIA_SPECIFIC_INDICATION の状態は、メディア固有の状態を示します。
ms.assetid: 983ffff1-5157-46ae-b4ce-31ee1aa55955
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_MEDIA_SPECIFIC_INDICATION ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 1b8f2431026016ba46320c01fa194e1ff7235a66
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838035"
---
# <a name="ndis_status_media_specific_indication"></a>NDIS\_ステータス\_メディア\_特定の\_表示


NDIS\_ステータス\_メディア\_特定の\_表示状態は、メディア固有の状態を示します。

<a name="remarks"></a>注釈
-------

ミニポートドライバーでは、 [**ndis\_status**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)の**StatusCode**メンバーを使用して[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)関数を呼び出すことによって、メディア固有のステータスを確認します。構造体は、ndis\_status に設定されて\_\_メディア\_特定の\_を示します。 この構造体の**Statusbuffer**メンバーは、ドライバーによって割り当てられたバッファーを指しています。 バッファーには、 **StatusCode**メンバーで識別される状態の表示に固有の形式のデータが含まれています。

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
<td><p>Windows Vista では、NDIS 6.0 および NDIS 5.1 ドライバーでサポートされています。 Windows XP の NDIS 5.1 ドライバーでサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

 

 




