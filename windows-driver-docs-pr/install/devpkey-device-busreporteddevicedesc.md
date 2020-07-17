---
title: DEVPKEY_Device_BusReportedDeviceDesc
description: DEVPKEY_Device_BusReportedDeviceDesc
ms.assetid: 3a03b4f0-728c-4a15-9c97-03d03f65afc7
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_BusReportedDeviceDesc
topic_type:
- apiref
api_name:
- DEVPKEY_Device_BusReportedDeviceDesc
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bf2af5c130fbd34266662c1c9f2387971434e214
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418513"
---
# <a name="devpkey_device_busreporteddevicedesc"></a>DEVPKEY_Device_BusReportedDeviceDesc


DEVPKEY_Device_BusReportedDeviceDesc デバイスプロパティは、デバイスインスタンスのバスドライバーによって報告された文字列値を表します。

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
<td align="left"><p>DEVPKEY_Device_BusReportedDeviceDesc</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>インストールアプリケーションおよびインストーラーによる読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

DEVPKEY_Device_BusReportedDeviceDesc の値は、デバイスインスタンスのバスドライバーによって報告される文字列値を使用して、Windows プラグアンドプレイ (PnP) によって設定されます。 [**IRP_MN_QUERY_DEVICE_TEXT**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text)でクエリを行う場合、バスドライバーはこの値を返します。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出して、DEVPKEY_Device_BusReportedDeviceDesc の値を取得できます。

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


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






