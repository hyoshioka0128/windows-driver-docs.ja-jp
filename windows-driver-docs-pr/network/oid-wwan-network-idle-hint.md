---
title: OID_WWAN_NETWORK_IDLE_HINT
description: OID_WWAN_NETWORK_IDLE_HINT は、データのインターフェイスでのアクティブまたはアイドル状態のことが必要だかどうかに関するネットワーク インターフェイスにヒントを送信します。
ms.assetid: 1FE758C1-543A-45B4-A377-336A1307689F
ms.date: 08/08/2017
keywords: -OID_WWAN_NETWORK_IDLE_HINT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e2765c66ef4da9ffa395171c5c38a0dabdce77d7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360773"
---
# <a name="oidwwannetworkidlehint"></a>OID\_WWAN\_ネットワーク\_IDLE\_ヒント


OID\_WWAN\_ネットワーク\_IDLE\_ヒントは、データのインターフェイスでのアクティブまたはアイドル状態のことが必要だかどうかに関するネットワーク インターフェイスにヒントを送信します。 ネットワーク サービスでは、ヒューリスティックを使用して、一定期間があるネットワーク トラフィックを削減することを算出する場合、またはシステムがアイドル状態になった (コネクト スタンバイ) などを入力する場合に、インターフェイスにこの要求を通常送信するかを判断します。 ネットワーク インターフェイスを使用できますこのヒューリスティックへの入力として「高速休止期間」などの手順の実装します。

クエリ要求はサポートされていません。

ミニポート ドライバーが非同期的に、最初に返す NDIS セット要求を処理する必要があります\_状態\_INDICATION\_元の要求と後で使用して要求を完了するには、必要な作業、 [ **NDIS\_WWAN\_ネットワーク\_IDLE\_ヒント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_network_idle_hint)ネットワーク アイドル状態のヒントを示す構造体。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 10 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_ネットワーク\_IDLE\_ヒント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_network_idle_hint)

 

 




