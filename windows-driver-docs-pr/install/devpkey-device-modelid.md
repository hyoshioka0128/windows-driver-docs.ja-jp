---
title: DEVPKEY_Device_ModelId
description: DEVPKEY_Device_ModelId
ms.assetid: 6066f18b-40bf-4b36-9821-5e886e166256
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_ModelId
topic_type:
- apiref
api_name:
- DEVPKEY_Device_ModelId
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 46f9f69fa92b05c10b87d95afa70913af6005607
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418520"
---
# <a name="devpkey_device_modelid"></a>DEVPKEY_Device_ModelId


デバイスの DEVPKEY_Device_ModelId プロパティは、デバイスを[デバイスメタデータパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/device-metadata-packages)と照合します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr>
<th>属性</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_ModelId</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><a href="devprop-type-guid.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_GUID&lt;/strong&gt;](devprop-type-guid.md)"><strong>DEVPROP_TYPE_GUID</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>インストールアプリケーションとインストーラーによる読み取りおよび書き込みアクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

DEVPKEY_Device_ModelId デバイスプロパティは、Ihv および Oem が、同じ製造元とモデルを共有するデバイスを一意に識別するためのサポートを提供します。 モデル識別子 (ModelID) を使用することにより、Oem および Ihv は、自社のブランド化されたデバイスメタデータパッケージに配布されるデバイスモデルを一致させることができます。

デバイスの DEVPKEY_Device_ModelId プロパティには、デバイスのメタデータパッケージの[**Modelid**](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549295(v=vs.85)) XML 要素の値が含まれます。 デバイスをインストールすると、デバイスによって報告された ModelID の GUID 値がこの PKEY に設定されます。

詳細については、「[デバイスメタデータパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/device-metadata-packages)」を参照してください。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Devpkey (Devpkey を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[デバイスメタデータパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/device-metadata-packages)

[**ModelID**](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549295(v=vs.85))

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






