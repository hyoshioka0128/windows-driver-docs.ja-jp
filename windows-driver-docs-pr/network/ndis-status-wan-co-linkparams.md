---
title: NDIS_STATUS_WAN_CO_LINKPARAMS
description: NDIS_STATUS_WAN_CO_FRAGMENT 状態は、CoNDIS ミニポートアダプターでアクティブになっている特定の VC のパラメーターが変更されたことを示します。
ms.assetid: a28460fc-c9e6-49c4-949a-badd3491cdd6
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WAN_CO_LINKPARAMS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: df3f9d0d371bd06f9734e106e5c8bd19fd3b37da
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842382"
---
# <a name="ndis_status_wan_co_linkparams"></a>NDIS\_ステータス\_WAN\_CO\_LINKPARAMS


NDIS\_STATUS\_WAN\_CO\_フラグメントの状態は、CoNDIS ミニポートアダプタでアクティブになっている特定の VC のパラメータが変更されたことを示します。

<a name="remarks"></a>注釈
-------

[**NDIS\_ステータス\_示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体の**statusbuffer**メンバーには、 [**WAN\_CO\_linkparams**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565819(v=vs.85))構造体へのポインターが含まれています。 WAN\_CO\_LINKPARAMS 構造体は、VC の新しいパラメーターについて説明します。

NDIS\_ステータス\_WAN\_CO\_LINKPARAMS の詳細については、「 [wan のミニポートドライバーの状態](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-condis-wan-miniport-driver-status)を確認する」を参照してください。 CoNDIS WAN インターフェイスの詳細については、「 [CONDIS Wan ミニポートドライバーの実装](https://docs.microsoft.com/windows-hardware/drivers/network/implementing-condis-wan-miniport-drivers)」を参照してください。

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

[**WAN\_CO\_LINKPARAMS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565819(v=vs.85))

 

 




