---
title: NDIS_STATUS_PD_CURRENT_CONFIG
description: この状態表示では、NDIS_PD_CONFIG 構造が変更されたことを示す通知です。
ms.assetid: 0B63E85E-36A8-4DC4-A060-C40DCB6BE454
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PD_CURRENT_CONFIG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1267564707c0a8dfee868eadbd3e064ea9ae8f15
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368540"
---
# <a name="ndisstatuspdcurrentconfig"></a>NDIS\_状態\_PD\_現在\_構成


この状態の表示は、通知を[ **NDIS\_PD\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pd_config)構造が変更されました。

PacketDirect 対応ミニポート ドライバーは、NDIS を行う必要があります\_状態\_PD\_現在\_後の構成状態の表示、 [OID\_PD\_閉じる\_プロバイダー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pd-close-provider)または[OID\_PD\_オープン\_プロバイダー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pd-open-provider)要求。

ミニポート ドライバー呼び出し[ **NdisMIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)ステータスの表示にしてへのポインターを渡す必要があります、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)を通じて構造体、 *StatusIndication*パラメーター。 この通知を行うときに、ミニポート ドライバーがの次のメンバーを設定する必要があります、 **NDIS\_状態\_INDICATION**構造体。

-   **SourceHandle**ミニポートで受信したハンドルに設定する必要があります、 *MiniportAdapterHandle*のパラメーター、 [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。

-   **StatusCode** NDIS に設定する必要があります\_状態\_PD\_現在\_構成します。

-   **StatusBuffer** 、適切な NDIS を格納する ULONG 変数のアドレスを設定する必要があります\_状態\_xxxx コード スキャン操作の結果。

-   **StatusBufferSize**に設定する必要があります**sizeof**(ULONG)。

<a name="requirements"></a>必要条件
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
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)

[OID\_PD\_閉じる\_プロバイダー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pd-close-provider)

[OID\_PD\_オープン\_プロバイダー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pd-open-provider)

 

 




