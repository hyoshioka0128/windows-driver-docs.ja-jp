---
title: GUID_NDIS_GEN_PCI_DEVICE_CUSTOM_PROPERTIES
description: WMI クライアントは、GUID_NDIS_GEN_PCI_DEVICE_CUSTOM_PROPERTIES メソッド GUID を使用して、現在のリンクの状態を確認できます。
ms.assetid: a02b9049-e521-41df-ab4d-41e334ef779e
ms.date: 08/08/2017
keywords: -Windows Vista 以降の GUID_NDIS_GEN_PCI_DEVICE_CUSTOM_PROPERTIES ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 60970160dc2044c8523f11e937cbcbaa536e254b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842292"
---
# <a name="guid_ndis_gen_pci_device_custom_properties"></a>GUID\_NDIS\_GEN\_PCI\_デバイス\_カスタム\_プロパティ


WMI クライアントは、GUID\_NDIS\_GEN\_PCI\_デバイス\_カスタム\_プロパティメソッド GUID を使用して、現在のリンクの状態を確認できます。

<a name="remarks"></a>注釈
-------

NDIS では、この GUID とミニポートドライバーは OID クエリを受け取りません。

WMI クライアントが GUID\_NDIS\_GEN\_PCI\_デバイス\_カスタム\_プロパティの WMI メソッド要求を発行すると、NDIS はミニポートアダプターの PCI デバイスの PCI カスタムプロパティを返します。 Wmi メソッド識別子は、NDIS\_WMI\_既定の\_メソッド\_ID であり、WMI 入力バッファーには、 [**ndis\_wmi\_method\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header)構造体が含まれている必要があります。

この GUID と共に NDIS が返すデータバッファーには、[**カスタム\_プロパティの構造\_ndis\_PCI\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pci_device_custom_properties)が含まれています。

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
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_PCI\_デバイス\_カスタム\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pci_device_custom_properties)

[**NDIS\_WMI\_メソッド\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header)

 

 




