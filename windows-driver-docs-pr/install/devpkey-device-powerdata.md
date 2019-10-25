---
title: DEVPKEY_Device_PowerData
description: DEVPKEY_Device_PowerData
ms.assetid: a5ebb465-674c-483a-ae2c-c46c30a67662
keywords:
- DEVPKEY_Device_PowerData デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_PowerData
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b19cc8cc4143dbb1087d326483e271e2b52328b4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840644"
---
# <a name="devpkey_device_powerdata"></a>DEVPKEY_Device_PowerData


DEVPKEY_Device_PowerData device プロパティは、デバイスインスタンスに関する電源情報を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_PowerData</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-binary.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BINARY&lt;/strong&gt;](devprop-type-binary.md)"><strong>DEVPROP_TYPE_BINARY</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティアクセス</strong></p></td>
<td align="left"><p>インストールアプリケーションおよびインストーラーによる読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPDRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPDRP_DEVICE_POWER_DATA</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>必須ではない</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

DEVPKEY_Device_PowerData の値が設定されます。 DEVPKEY_Device_PowerData の値には、 [**CM_POWER_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-cm_power_data_s)構造体が含まれています。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出して、DEVPKEY_Device_PowerData の値を取得できます。

Windows Server 2003、Windows XP、および Windows 2000 では、このプロパティはサポートされていますが、DEVPKEY_Device_PowerData プロパティキーはサポートされていません。 代わりに、対応する SPDRP_DEVICE_POWER_DATA 識別子を使用して、これらの以前のバージョンの Windows でプロパティの値にアクセスできます。 これらの以前のバージョンの Windows でこのプロパティ値にアクセスする方法の詳細については、「[デバイスインスタンス SPDRP_Xxx のプロパティ](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)へのアクセス」を参照してください。

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


[**CM_POWER_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-cm_power_data_s)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






