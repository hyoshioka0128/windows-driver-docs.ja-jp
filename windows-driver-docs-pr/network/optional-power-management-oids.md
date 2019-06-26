---
title: オプションの電源管理 OID
description: オプションの電源管理 OID
ms.assetid: 31c8ec45-ecb2-42e2-be4d-2b89fe02a908
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b7b8551028d0531d4815e6bd4160a814547ac42
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366546"
---
# <a name="optional-power-management-oids"></a>オプションの電源管理 OID





デバイスの電源の管理 - を考慮する NDIS 用対応する必要がありますしても応答 Oid が、次の表に示す 3 つの電源管理。 デバイスのクエリに対する応答でエラー状態コードが返されますかどうか[OID\_PNP\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)ホストができない電源管理とデバイスを検討してください。 NDIS にリモートの NDIS デバイスが接続されている、基になる bus テクノロジに基づいてこの OID を照会するかどうかを決定します。 いくつかのバスは、これらの種類のリモートの NDIS デバイスが電源管理しやすいと見なされる最小の Oid をサポートする必要がありますので電源管理が可能な USB など。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">サポート</th>
<th align="left">OID</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities" data-raw-source="[OID_PNP_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)">OID_PNP_CAPABILITIES</a></p></td>
<td align="left"><p>NIC の電源管理機能</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-query-power" data-raw-source="[OID_PNP_QUERY_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-query-power)">OID_PNP_QUERY_POWER</a></p></td>
<td align="left"><p>デバイスが特定の電源状態に移行できるかどうかを決定するクエリ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power" data-raw-source="[OID_PNP_SET_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)">OID_PNP_SET_POWER</a></p></td>
<td align="left"><p>指定した電源の状態、デバイスを設定するコマンド</p></td>
</tr>
</tbody>
</table>

 

 

 





