---
title: オプションのネットワーク ウェイクアップ OID
description: オプションのネットワーク ウェイクアップ OID
ms.assetid: 0e9b4844-1623-4bfd-8e73-ebbd970c7e95
keywords:
- 省略可能なネットワークのウェイク アップの Oid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70dff227b8fab5b832dfe5b6f6c5e14990f167a0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359238"
---
# <a name="optional-network-wake-up-oids"></a>オプションのネットワーク ウェイクアップ OID





ネットワークへの復帰イベントをサポートするために、リモートの NDIS デバイスでサポートする必要がありますさらに、 [OID\_PNP\_を有効にする\_WAKE\_を](https://msdn.microsoft.com/library/windows/hardware/ff569775)両方のネットワーク プロトコル (TCP/IP) によって使用される OIDおよび NDIS ウェイク アップ機能を有効にします。 さらに、ウェイク アップ パターンの特定の種類を有効にするは次の表に示すオプションです。 詳細については、Microsoft Windows 2000 Driver Development Kit (DDK) を参照してください。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569775" data-raw-source="[OID_PNP_ENABLE_WAKE_UP](https://msdn.microsoft.com/library/windows/hardware/ff569775)">OID_PNP_ENABLE_WAKE_UP</a></p></td>
<td align="left"><p>NDIS リモート デバイスのウェイク アップ機能を有効にすることができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569773" data-raw-source="[OID_PNP_ADD_WAKE_UP_PATTERN](https://msdn.microsoft.com/library/windows/hardware/ff569773)">OID_PNP_ADD_WAKE_UP_PATTERN</a></p></td>
<td align="left"><p>デバイスにリモートの NDIS ミニポート ドライバーを読み込む必要のあるウェイク アップ パターン</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569779" data-raw-source="[OID_PNP_REMOVE_WAKE_UP_PATTERN](https://msdn.microsoft.com/library/windows/hardware/ff569779)">OID_PNP_REMOVE_WAKE_UP_PATTERN</a></p></td>
<td align="left"><p>デバイスからリモートの NDIS ミニポート ドライバーを削除する必要がありますウェイク アップ パターン</p></td>
</tr>
</tbody>
</table>

 

 

 





