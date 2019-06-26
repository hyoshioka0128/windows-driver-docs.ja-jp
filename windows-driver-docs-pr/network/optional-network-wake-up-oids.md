---
title: オプションのネットワーク ウェイクアップ OID
description: オプションのネットワーク ウェイクアップ OID
ms.assetid: 0e9b4844-1623-4bfd-8e73-ebbd970c7e95
keywords:
- 省略可能なネットワークのウェイク アップの Oid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ce2422317338729fccbca0920664bbb9d938449
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366563"
---
# <a name="optional-network-wake-up-oids"></a>オプションのネットワーク ウェイクアップ OID





ネットワークへの復帰イベントをサポートするために、リモートの NDIS デバイスでサポートする必要がありますさらに、 [OID\_PNP\_を有効にする\_WAKE\_を](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-enable-wake-up)両方のネットワーク プロトコル (TCP/IP) によって使用される OIDおよび NDIS ウェイク アップ機能を有効にします。 さらに、ウェイク アップ パターンの特定の種類を有効にするは次の表に示すオプションです。 詳細については、Microsoft Windows 2000 Driver Development Kit (DDK) を参照してください。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-enable-wake-up" data-raw-source="[OID_PNP_ENABLE_WAKE_UP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-enable-wake-up)">OID_PNP_ENABLE_WAKE_UP</a></p></td>
<td align="left"><p>NDIS リモート デバイスのウェイク アップ機能を有効にすることができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-add-wake-up-pattern" data-raw-source="[OID_PNP_ADD_WAKE_UP_PATTERN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-add-wake-up-pattern)">OID_PNP_ADD_WAKE_UP_PATTERN</a></p></td>
<td align="left"><p>デバイスにリモートの NDIS ミニポート ドライバーを読み込む必要のあるウェイク アップ パターン</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-remove-wake-up-pattern" data-raw-source="[OID_PNP_REMOVE_WAKE_UP_PATTERN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-remove-wake-up-pattern)">OID_PNP_REMOVE_WAKE_UP_PATTERN</a></p></td>
<td align="left"><p>デバイスからリモートの NDIS ミニポート ドライバーを削除する必要がありますウェイク アップ パターン</p></td>
</tr>
</tbody>
</table>

 

 

 





