---
title: NDIS_STATUS_PM_OFFLOAD_REJECTED
description: NDIS_STATUS_PM_OFFLOAD_REJECTED の状態は、電源管理プロトコルのオフロードが拒否されたことを示しています。
ms.assetid: 54922e70-2b56-4141-b79b-73418c7553e3
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PM_OFFLOAD_REJECTED ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 4bc9ac0203c8578492d1590895d2c50de82a42cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843538"
---
# <a name="ndis_status_pm_offload_rejected"></a>NDIS\_STATUS\_PM\_オフロード\_拒否されました


NDIS\_STATUS\_PM\_オフロード\_拒否状態は、電源管理プロトコルオフロードが拒否されたことを示します。

<a name="remarks"></a>注釈
-------

NDIS またはミニポートドライバーは、\_オフロードされたプロトコルを削除すると、\_PM オフロード\_の\_状態を示すことができます。 [**NDIS\_状態の\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**statusbuffer**メンバーは、拒否されたプロトコルオフロードのプロトコルオフロード識別子の ULONG を含みます。 NDIS は、 [**ndis\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)構造体の**ProtocolOffloadId**メンバーにプロトコルオフロード識別子を提供しました。

NDIS では、以前にオフロードされたプロトコルをネットワークアダプターから削除する必要がある場合に、NDIS\_STATUS\_PM\_オフロード\_拒否状態が通知されます。 たとえば、NDIS はプロトコルオフロードを削除して、優先順位の高いプロトコルオフロード用にリソースを解放する場合があります。 NDIS は、拒否されたプロトコルオフロードをオフロードしたバインディングに状態表示を送信しますが、他のバインドには送信しません。

ミニポートドライバーは、以前に受け入れられたプロトコルオフロードを拒否するようにこのステータスを報告します。 たとえば、WiFi WOL ケースの場合、ミニポートドライバーは、(ベンダー固有のインフラストラクチャのサポートにより) WOL をサポートするために PTK/GTK ローテーションが必要でない場合に、NDIS\_状態\_PM\_オフロード\_拒否状態を示す必要があります。

インフラストラクチャ要素を使用してプロトコルをオフロードし、インフラストラクチャ間のローミングを行うワイヤレスネットワークアダプターでは、新しいインフラストラクチャ要素が前のものと同じ機能をサポートしていない可能性があります。 この場合、ミニポートドライバーは NDIS に状態を示す状態を発行し、ndis は NDIS\_STATUS\_PM\_オフロード\_特定のエラーコードで拒否を発行します。

WiFi ドライバーは、プロトコルオフロード要求をローカルにキャッシュする場合があります。 ドライバーがプロトコルオフロードを追加または削除するための OID を処理する場合、ドライバーはローカルキャッシュの更新のみを選択できます。 ドライバーは、 [oid\_PM\_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters) oid を受け取るまで、インフラストラクチャの更新を遅らせることができます。

インフラストラクチャには、すべてのプロトコルのオフロードに対応するのに十分なリソースがない可能性があります。 この場合、インフラストラクチャは、プロトコルオフロードの部分的な一覧を受け入れることができます。 ミニポートドライバーが OID\_PM\_PARAMETERS set 要求を完了すると、ミニポートドライバーは、各プロトコルの\_拒否された状態の状態を\_PM に設定\_する必要があります。却下.

たとえば、ネットワークアダプターは、ARP オフロードをサポートするために AP のプロキシ ARP を使用できます。

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


[**NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID\_PM\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)

 

 




