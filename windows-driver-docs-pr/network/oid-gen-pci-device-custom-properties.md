---
title: OID_GEN_PCI_DEVICE_CUSTOM_PROPERTIES
description: クエリとして、後続のドライバーは OID_GEN_PCI_DEVICE_CUSTOM_PROPERTIES OID を使用してデバイスの PCI カスタムプロパティを取得します。
ms.assetid: fe94884b-f5e3-4c60-8f52-e61d0df81a2a
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_PCI_DEVICE_CUSTOM_PROPERTIES ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: ded468b6321b33200058aa9cdb06575cb0760bbb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824388"
---
# <a name="oid_gen_pci_device_custom_properties"></a>OID\_GEN\_PCI\_デバイス\_カスタム\_プロパティ


クエリとして、これまでのドライバーでは、デバイスの PCI カスタムプロパティを取得するために、カスタム\_プロパティ OID\_、OID\_GEN\_PCI\_デバイスを使用します。

<a name="remarks"></a>注釈
-------

NDIS は、\_PCI\_デバイスの OID\_GEN を処理\_カスタム\_プロパティとミニポートドライバーは OID クエリを受け取りません。

このクエリは、他の NDIS ドライバーでは省略可能です。

NDIS は、PCI カスタムプロパティを含む[**カスタム\_プロパティの構造\_、ndis\_pci\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pci_device_custom_properties)を返します。

PCI 以外のミニポートアダプターの場合、NDIS は、\_PCI\_デバイスの\_GEN に失敗します。これは、NDIS\_ステータスを持つカスタム\_プロパティ\_無効\_デバイス\_要求状態コードです。

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

 

 




