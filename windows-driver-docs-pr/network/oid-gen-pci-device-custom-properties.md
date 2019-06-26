---
title: OID_GEN_PCI_DEVICE_CUSTOM_PROPERTIES
description: 上にあるドライバーはクエリとして OID_GEN_PCI_DEVICE_CUSTOM_PROPERTIES OID を使用して、デバイスの PCI のカスタム プロパティを取得します。
ms.assetid: fe94884b-f5e3-4c60-8f52-e61d0df81a2a
ms.date: 08/08/2017
keywords: -OID_GEN_PCI_DEVICE_CUSTOM_PROPERTIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b4682a1d13192db3a0cfe06dce88da1446a1dbda
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386219"
---
# <a name="oidgenpcidevicecustomproperties"></a>OID\_GEN\_PCI\_デバイス\_カスタム\_プロパティ


上にあるドライバーが、OID を使用するクエリとして\_GEN\_PCI\_デバイス\_カスタム\_デバイスの PCI のカスタム プロパティを取得するプロパティの OID。

<a name="remarks"></a>注釈
-------

NDIS 処理 OID\_GEN\_PCI\_デバイス\_カスタム\_プロパティおよびミニポート ドライバーが、OID クエリを受信しません。

このクエリでは、その他の NDIS ドライバーのオプションです。

NDIS を返します、 [ **NDIS\_PCI\_デバイス\_カスタム\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pci_device_custom_properties) PCI のカスタム プロパティを含む構造体。

NDIS ミニポート アダプターが非 PCI、OID は失敗\_GEN\_PCI\_デバイス\_カスタム\_NDIS プロパティ\_状態\_無効な\_デバイス\_状態コードを要求します。

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
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_PCI\_デバイス\_カスタム\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pci_device_custom_properties)

 

 




