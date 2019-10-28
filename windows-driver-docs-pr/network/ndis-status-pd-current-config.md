---
title: NDIS_STATUS_PD_CURRENT_CONFIG
description: この状態は、NDIS_PD_CONFIG 構造体が変更されたことを示す通知です。
ms.assetid: 0B63E85E-36A8-4DC4-A060-C40DCB6BE454
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PD_CURRENT_CONFIG ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 6804254fae8e70074525778117d7226649e23ece
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842774"
---
# <a name="ndis_status_pd_current_config"></a>NDIS\_の状態\_PD\_現在の\_構成


この状態は、 [**NDIS\_PD\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pd_config)構造が変更されたことを示す通知です。

PacketDirect 対応のミニポートドライバーでは、\_\_現在の\_構成の状態を確認する必要があります。これは、 [oid\_pd](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pd-close-provider)の後、\_プロバイダーまたは oid\_を閉じるか、または OID を終了した後に\_[\_11_ プロバイダー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pd-open-provider)要求。

ミニポートドライバーは、 [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)を呼び出してステータスを表示します。また、 *statusindication*パラメーターを使用して、 [**NDIS\_status\_を示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体へのポインターを渡す必要があります。 このことを示すには、ミニポートドライバーで、 **NDIS\_STATUS\_** 表示構造体の次のメンバーを設定する必要があります。

-   **Sourcehandle**は、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数の*miniportadapterhandle*パラメーターでミニポートが受信したハンドルに設定する必要があります。

-   **StatusCode**は、現在の\_CONFIG\_\_PD\_STATUS に設定する必要があります。

-   **Statusbuffer**は ULONG 変数のアドレスに設定する必要があります。これにより、スキャン操作の結果に対する適切な NDIS\_の状態\_xxxx コードが格納されます。

-   **Statusbuffersize**は**sizeof**(ULONG) に設定する必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

[OID\_PD\_\_プロバイダーを閉じる](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pd-close-provider)

[OID\_PD\_オープン\_プロバイダー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pd-open-provider)

 

 




