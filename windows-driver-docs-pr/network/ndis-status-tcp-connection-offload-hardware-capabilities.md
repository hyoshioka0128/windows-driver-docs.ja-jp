---
title: NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES
description: MUX 中間ドライバーは、NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES 機能の状態の表示を使用して、基盤となるハードウェアの接続オフロード特性が変更されたことを NDIS およびそれ以降のドライバーに通知します.
ms.assetid: 694cc0c4-0987-4095-8490-14ddfc9eaedb
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: fb3399d76ad54d860701a07ea1427e507fa538e1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843507"
---
# <a name="ndis_status_tcp_connection_offload_hardware_capabilities"></a>NDIS\_ステータス\_TCP\_接続\_オフロード\_ハードウェア\_機能


MUX 中間ドライバーは、NDIS\_の状態\_TCP\_接続を使用して\_オフロード\_ハードウェア\_機能機能の状態を示します。これは、変更されていることを NDIS およびそれ以降のドライバーに通知するためのものです。基になるハードウェアの接続オフロード特性。

<a name="remarks"></a>注釈
-------

基になる NIC を追加または削除した場合、MUX 中間ドライバーに関連付けられているハードウェア機能の全体的なセットが変更される可能性があります。

[**Ndis\_ステータス\_示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体の**statusbuffer**メンバーには、 [**ndis\_TCP\_接続\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)構造体が含まれています。 NDIS\_TCP\_接続\_オフロードでは、タスクのオフロードハードウェア機能を指定します。

タスクオフロードハードウェア機能の詳細については、「 [OID\_TCP\_接続\_オフロード\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-hardware-capabilities)」を参照してください。

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
<td><p>NDIS 6.0 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_TCP\_接続\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)

[OID\_TCP\_接続\_オフロード\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-hardware-capabilities)

 

 




