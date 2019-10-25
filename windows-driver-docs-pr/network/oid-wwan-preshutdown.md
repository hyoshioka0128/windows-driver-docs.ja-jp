---
title: OID_WWAN_PRESHUTDOWN
description: OID_WWAN_PRESHUTDOWN は、システムがシャットダウンフェーズに入っていることをモデムに通知するために送信されます。モデムは、正常にシャットダウンできるように、その操作を完了する必要があります。
ms.assetid: B00A2D70-64E0-4686-92FC-D4095BDD713B
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_PRESHUTDOWN ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: d2799e96843312f4df1964beb413defec873fc3c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843807"
---
# <a name="oid_wwan_preshutdown"></a>OID\_WWAN\_PRESHUTDOWN


OID\_WWAN\_事前シャットダウンは、システムがシャットダウンフェーズに入っていることをモデムに通知するために送信されます。モデムは、正常にシャットダウンできるように操作を完了する必要があります。 物理 MBB アダプターに対応するポート番号を使用して送信されるだけです。 複数の PDP コンテキストをサポートする仮想アダプターは、この OID を受け取ることはできません。

クエリ要求はサポートされていません。

ミニポートドライバーは、set 要求を非同期に処理し、最初に**ndis\_\_状態**を返し、元の要求に必要な\_を示し、後で[**ndis\_ステータス\_WWAN\_を送信する必要があり**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preshutdown-state)MBB ドライバーがシャットダウン前に必要なすべてのモデム操作を完了したときの、状態状態通知の事前シャットダウン\_。 Set 要求には、 [**NDIS\_WWAN\_\_プレシャットダウン\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preshutdown_state)構造が設定されています。

ミニポートドライバーは、この操作をサポートしていない場合、**サポートされていない\_ため、NDIS\_の状態\_返される**必要があります。

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
<td><p>Windows 10 バージョン1511以降で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_ステータス\_WWAN\_プレシャットダウン\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preshutdown-state)

[**NDIS\_WWAN\_\_プレシャットダウン\_状態の設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preshutdown_state)

 

 




