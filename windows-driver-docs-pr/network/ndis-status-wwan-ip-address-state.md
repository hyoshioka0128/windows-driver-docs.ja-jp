---
title: NDIS_STATUS_WWAN_IP_ADDRESS_STATE
description: ミニポート ドライバーでは、MB サービスに追加の PDP コンテキストの IP 構成の変更に関する通知 NDIS_STATUS_WWAN_IP_ADDRESS_STATE 通知を使用します。
ms.assetid: 98E4028D-AD75-4F12-ADA4-41725253166F
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_IP_ADDRESS_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b246b73cc066af436961799c972cdcc05a5a4eec
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377631"
---
# <a name="ndisstatuswwanipaddressstate"></a>NDIS\_STATUS\_WWAN\_IP\_ADDRESS\_STATE


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_IP\_アドレス\_MB サービスに追加の PDP コンテキストの IP 構成の変更に関する通知の状態通知します。

この通知を使用して、 [ **NDIS\_WWAN\_IP\_アドレス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_ip_address_state)構造体。

<a name="remarks"></a>注釈
-------

この通知は、追加の PDP コンテキストのセッションに関連付けられた NDIS ポートで送信する必要があります。

ミニポート ドライバーは、追加の PDP コンテキストが正常にアクティブ化し、そのコンテキストの IP 構成が取得された後、この通知を送信する必要があります。 デバイスには、要請していない IP 構成の変更後のコンテキストのアクティベーションが示されている場合ミニポート ドライバー更新された IP 構成でこの通知が不要なを示す値を送信する必要があります。

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
<td><p>Windows 8.1 と Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_IP\_ADDRESS\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_ip_address_state)

 

 




