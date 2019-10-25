---
title: DEVPKEY_Device_BusTypeGuid
description: DEVPKEY_Device_BusTypeGuid
ms.assetid: a68e7ff2-9afa-48d5-9764-3c400561024e
keywords:
- DEVPKEY_Device_BusTypeGuid デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_BusTypeGuid
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4d72b4fc89d03c177e279d75d385b8c864ce6da2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838755"
---
# <a name="devpkey_device_bustypeguid"></a>DEVPKEY_Device_BusTypeGuid


DEVPKEY_Device_BusTypeGuid device プロパティは、デバイスインスタンスのバスの種類を識別する GUID を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_BusTypeGuid</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-guid.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_GUID&lt;/strong&gt;](devprop-type-guid.md)"><strong>DEVPROP_TYPE_GUID</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティアクセス</strong></p></td>
<td align="left"><p>インストールアプリケーションおよびインストーラーによる読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPDRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPDRP_BUSTYPEGUID</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>必須ではない</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

DEVPKEY_Device_BusTypeGuid の値は、 [**IRP_MN_QUERY_BUS_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-bus-information)要求に応じてバスドライバーが返す[**PNP_BUS_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pnp_bus_information)構造体の BusTypeGuid メンバーの値に設定されます。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出して、DEVPKEY_Device_BusTypeGuid の値を取得できます。

Windows Server 2003、Windows XP、および Windows 2000 では、このプロパティはサポートされていますが、DEVPKEY_Device_BusTypeGuid プロパティキーはサポートされていません。 代わりに、対応する SPDRP_BUSTYPEGUID 識別子を使用して、これらの以前のバージョンの Windows でプロパティの値にアクセスできます。 これらの以前のバージョンの Windows でこのプロパティ値にアクセスする方法の詳細については、「[デバイスインスタンス SPDRP_Xxx のプロパティ](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)へのアクセス」を参照してください。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey (Devpkey を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IRP_MN_QUERY_BUS_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-bus-information)

[**PNP_BUS_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pnp_bus_information)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






