---
title: NDIS_STATUS_WWAN_VENDOR_SPECIFIC
description: ミニポートドライバーは、NDIS_STATUS_WWAN_VENDOR_SPECIFIC 通知を使用して、ベンダー固有の操作またはベンダー固有の変更通知に対するトランザクション完了応答を実装します。
ms.assetid: 2032ed5e-8a4a-4c1c-9dbe-05e7cec1b683
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_VENDOR_SPECIFIC ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 3d7e66cda2941f45fc8aa93298c6e99201510ed6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834649"
---
# <a name="ndis_status_wwan_vendor_specific"></a>NDIS\_状態\_WWAN\_ベンダー\_固有


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_ベンダ\_特定の通知を使用して、ベンダー固有の操作またはベンダー固有の変更通知に対するトランザクション完了応答を実装します。

ミニポートドライバーは、この通知を使用して、要請されていないイベントも送信できます。

この通知では、 [**NDIS\_WWAN\_ベンダ\_特定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_vendor_specific)の構造を使用します。

<a name="remarks"></a>注釈
-------

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
<td><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_ベンダー\_固有**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_vendor_specific)

[OID\_WWAN\_ベンダー\_固有のもの](oid-wwan-vendor-specific.md)

 

 




