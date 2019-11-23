---
title: OID_WWAN_NETWORK_IDLE_HINT
description: OID_WWAN_NETWORK_IDLE_HINT は、データがアクティブであるか、またはインターフェイスでアイドル状態であることが予想されるかについて、ネットワークインターフェイスにヒントを送信します。
ms.assetid: 1FE758C1-543A-45B4-A377-336A1307689F
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_WWAN_NETWORK_IDLE_HINT
ms.localizationpriority: medium
ms.openlocfilehash: 939db61fdaa8139b7363a5ba8515161016e22d56
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843828"
---
# <a name="oid_wwan_network_idle_hint"></a>OID\_WWAN\_ネットワーク\_アイドル\_ヒント


OID\_WWAN\_ネットワーク\_アイドル状態の\_ヒントは、データがアクティブであるか、またはインターフェイスでアイドル状態になっているかどうかに関するヒントをネットワークインターフェイスに送信します。 ネットワークサービスはヒューリスティックを使用して、この要求をインターフェイスに送信するタイミングを決定します。通常は、一定期間にわたってネットワークトラフィックが減少すること、またはシステムがアイドル状態 (コネクトスタンバイなど) に入っているかどうかを推定します。 ネットワークインターフェイスは、これをヒューリスティックへの入力として使用して、"fast うち休止期間" などのプロシージャを実装できます。

クエリ要求はサポートされていません。

ミニポートドライバーは、set 要求を非同期に処理し、最初に NDIS\_ステータス\_を返し、元の要求に必要な\_を示します。その後、 [**ndis\_WWAN\_ネットワーク\_アイドル\_ヒント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_idle_hint)構造を使用してネットワークアイドルヒントを示す要求を完了します。

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
<td><p>Windows 10 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_ネットワーク\_アイドル\_ヒント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_idle_hint)

 

 




