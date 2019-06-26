---
title: NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES
description: MUX 中間ドライバー NDIS に通知する、NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES 機能の状態を示す値を使用して、接続の変更があった上にあるドライバーは、基になるハードウェアの特性をオフロード.
ms.assetid: 694cc0c4-0987-4095-8490-14ddfc9eaedb
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c68abc8dc96ea9b6a9e8337c025a17d9f58d1570
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372569"
---
# <a name="ndisstatustcpconnectionoffloadhardwarecapabilities"></a>NDIS\_状態\_TCP\_接続\_オフロード\_ハードウェア\_機能


MUX 中間ドライバーを使用して、NDIS\_状態\_TCP\_接続\_オフロード\_ハードウェア\_NDIS と関連付けたドライバーに通知する機能の機能の状態の表示基になるハードウェアの接続のオフロード特性の変更がありました。

<a name="remarks"></a>注釈
-------

基になる NIC を追加したり削除したり、MUX 中間ドライバーに関連付けられているハードウェア機能の全体的なセットを変更できます。

**StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造に含まれる、 [ **NDIS\_TCP\_接続\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)構造体。 NDIS\_TCP\_接続\_オフロードは、タスクのオフロード ハードウェア機能を指定します。

タスクのオフロード ハードウェア機能の詳細については、次を参照してください。 [OID\_TCP\_接続\_オフロード\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-hardware-capabilities)します。

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
<td><p>NDIS 6.0 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_TCP\_接続\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)

[OID\_TCP\_接続\_オフロード\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-hardware-capabilities)

 

 




