---
title: DEVPKEY_Device_PhysicalDeviceLocation
description: DEVPKEY_Device_PhysicalDeviceLocation
ms.assetid: DEF01D17-7E32-45BB-8846-D3B3B60506EB
keywords:
- DEVPKEY_Device_PhysicalDeviceLocation デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_PhysicalDeviceLocation
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 580beb199fac00a965011bc3e28d23ceeacd2a8a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384265"
---
# <a name="devpkeydevicephysicaldevicelocation"></a>DEVPKEY_Device_PhysicalDeviceLocation


DEVPKEY_Device_PhysicalDeviceLocation デバイスのプロパティには、Windows に用意されているデバイスのファームウェア、物理デバイスの場所情報がカプセル化します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_PhysicalDeviceLocation</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BINARY&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_BINARY</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPDRP_<em>Xxx</em></strong>  <strong>識別子</strong></p></td>
<td align="left"><p>SPDRP_PHYSICAL_DEVICE_LOCATION</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

Windows では、物理デバイスの位置情報で DEVPKEY_Device_PhysicalDeviceLocation の値を設定します。 ACPI 4.0 a で、情報の形式が定義されている仕様、6.1.6 を参照します。

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963) DEVPKEY_Device_PhysicalDeviceLocation の値を取得します。

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
<td align="left"><p>Windows 8 以降で利用可能</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h (Devpkey.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






