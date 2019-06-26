---
title: GUID_NDIS_GEN_PCI_DEVICE_CUSTOM_PROPERTIES
description: WMI クライアントでは、現在のリンクの状態を判断するのに GUID_NDIS_GEN_PCI_DEVICE_CUSTOM_PROPERTIES メソッド GUID を使用できます。
ms.assetid: a02b9049-e521-41df-ab4d-41e334ef779e
ms.date: 08/08/2017
keywords: -GUID_NDIS_GEN_PCI_DEVICE_CUSTOM_PROPERTIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 8247297d1f9e65e5c7d0b43b65a0e6b0c9406090
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382713"
---
# <a name="guidndisgenpcidevicecustomproperties"></a>GUID\_NDIS\_GEN\_PCI\_デバイス\_カスタム\_プロパティ


WMI クライアントが、GUID を使用できる\_NDIS\_GEN\_PCI\_デバイス\_カスタム\_プロパティ メソッドのリンクの現在の状態を確認するのには GUID です。

<a name="remarks"></a>注釈
-------

NDIS は、この GUID を処理し、ミニポート ドライバーが、OID クエリを受信しません。

WMI クライアントが GUID を発行したとき\_NDIS\_GEN\_PCI\_デバイス\_カスタム\_プロパティ WMI メソッドを要求、NDIS ミニポートの PCI デバイスの PCI のカスタム プロパティを返しますアダプター。 WMI のメソッド識別子は、NDIS をする必要があります\_WMI\_既定\_メソッド\_ID、および WMI の入力バッファーに格納する必要があります、 [ **NDIS\_WMI\_メソッド\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_method_header)構造体。

この GUID を持つ NDIS が返すデータ バッファーを含む、 [ **NDIS\_PCI\_デバイス\_カスタム\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pci_device_custom_properties)構造体。

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

[**NDIS\_WMI\_メソッド\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_method_header)

 

 




