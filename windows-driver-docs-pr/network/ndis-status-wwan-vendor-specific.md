---
title: NDIS_STATUS_WWAN_VENDOR_SPECIFIC
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_VENDOR_SPECIFIC 通知を使用して、仕入先の特定の操作のトランザクションの完了の応答を実装する、またはベンダー固有の変更通知します。
ms.assetid: 2032ed5e-8a4a-4c1c-9dbe-05e7cec1b683
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_VENDOR_SPECIFIC ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a90a1013e6e62224a1f536c42b26012fe644d520
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372509"
---
# <a name="ndisstatuswwanvendorspecific"></a>NDIS\_状態\_WWAN\_ベンダー\_特定


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_ベンダー\_仕入先の特定の操作またはベンダー固有のトランザクションの完了の応答を実装するために特定の通知は通知を変更します。

ミニポート ドライバーには、この通知が不要なイベントを送信できます。

この通知を使用して、 [ **NDIS\_WWAN\_ベンダー\_特定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_vendor_specific)構造体。

<a name="remarks"></a>注釈
-------

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
<td><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_ベンダー\_特定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_vendor_specific)

[OID\_WWAN\_ベンダー\_特定](oid-wwan-vendor-specific.md)

 

 




