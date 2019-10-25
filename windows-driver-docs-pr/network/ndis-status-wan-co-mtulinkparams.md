---
title: NDIS_STATUS_WAN_CO_MTULINKPARAMS
description: NDIS_STATUS_WAN_CO_MTULINKPARAMS の状態は、CoNDIS アダプターでアクティブになっている特定の VC のリンク速度と送信ウィンドウのパラメーターが変更されたことを示します。
ms.assetid: 1ba67087-08aa-4359-9884-e47bf634fda5
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WAN_CO_MTULINKPARAMS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 05269b2d05b5d3a76a04f0f7b6e4487be7934f3e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842379"
---
# <a name="ndis_status_wan_co_mtulinkparams"></a>NDIS\_ステータス\_WAN\_CO\_MTULINKPARAMS


NDIS\_STATUS\_WAN\_CO\_MTULINKPARAMS ステータスは、CoNDIS ミニポートアダプターでアクティブになっている特定の VC のリンク速度と送信ウィンドウパラメーターが変更されたことを示します。

<a name="remarks"></a>注釈
-------

[**NDIS\_ステータス\_示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体の**statusbuffer**メンバーには、 [**WAN\_CO\_mtulinkparams**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565821(v=vs.85))構造体へのポインターが含まれています。 WAN\_CO\_MTULINKPARAMS 構造体は、VC の新しいパラメーターについて説明します。

NDIS\_ステータス\_WAN\_CO\_MTULINKPARAMS の詳細については、「 [Wan ミニポートドライバーの状態](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-condis-wan-miniport-driver-status)を確認する」を参照してください。 CoNDIS WAN インターフェイスの詳細については、「 [CONDIS Wan ミニポートドライバーの実装](https://docs.microsoft.com/windows-hardware/drivers/network/implementing-condis-wan-miniport-drivers)」を参照してください。

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
<td><p>NDIS 6.20 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**WAN\_CO\_MTULINKPARAMS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565821(v=vs.85))

 

 




