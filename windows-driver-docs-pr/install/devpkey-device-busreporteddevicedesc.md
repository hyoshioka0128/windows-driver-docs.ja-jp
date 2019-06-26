---
title: DEVPKEY_Device_BusReportedDeviceDesc
description: DEVPKEY_Device_BusReportedDeviceDesc
ms.assetid: 3a03b4f0-728c-4a15-9c97-03d03f65afc7
keywords:
- DEVPKEY_Device_BusReportedDeviceDesc デバイスとドライバーのインストール
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
ms.openlocfilehash: 2ebe588421ac6c49c52bea600d1ec80cda971d5d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387105"
---
# <a name="devpkeydevicebusreporteddevicedesc"></a>DEVPKEY_Device_BusReportedDeviceDesc


DEVPKEY_Device_BusReportedDeviceDesc デバイス プロパティは、デバイスのインスタンスのバス ドライバーによって報告された文字列値を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_BusReportedDeviceDesc</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

DEVPKEY_Device_BusReportedDeviceDesc の値によって Windows のプラグ アンド プレイ (PnP) 値に設定されます、文字列インスタンスのデバイス、バス ドライバーによって報告されます。 クエリを実行時に、この値を返します、バス ドライバー [ **IRP_MN_QUERY_DEVICE_TEXT**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text)します。

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) DEVPKEY_Device_BusReportedDeviceDesc の値を取得します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h (Devpkey.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






