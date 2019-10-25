---
title: NDIS_STATUS_WWAN_IP_ADDRESS_STATE
description: ミニポートドライバーは、NDIS_STATUS_WWAN_IP_ADDRESS_STATE 通知を使用して、追加の PDP コンテキストの IP 構成の変更について MB サービスに通知します。
ms.assetid: 98E4028D-AD75-4F12-ADA4-41725253166F
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_IP_ADDRESS_STATE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: c547aec60bd2c0334db6d282bc2f66fc3a16095a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843025"
---
# <a name="ndis_status_wwan_ip_address_state"></a>NDIS\_ステータス\_WWAN\_IP\_アドレス\_状態


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_IP\_アドレス\_状態通知を使用して、追加の PDP コンテキストの IP 構成の変更を MB サービスに通知します。

この通知では、 [**NDIS\_WWAN\_IP\_アドレスの\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ip_address_state)構造を使用します。

<a name="remarks"></a>注釈
-------

この通知は、追加の PDP コンテキストセッションに関連付けられている NDIS ポートで送信される必要があります。

追加の PDP コンテキストが正常にアクティブ化され、そのコンテキストに対して IP 構成が取得された後に、ミニポートドライバーはこの通知を送信する必要があります。 デバイスが、コンテキストが要求されていない IP 構成の変更を示している場合は、ミニポートドライバーは、更新された IP 構成を使用して、この通知に対して要請されていない通知を送信します

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
<td><p>Windows の Windows 8.1 以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_IP\_アドレス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ip_address_state)

 

 




