---
title: DEVPKEY_Device_DriverVersion
description: DEVPKEY_Device_DriverVersion
ms.assetid: 68df1313-e948-4aea-9b90-c838f7bf228d
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_DriverVersion
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DriverVersion
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 35e08c80f1416a43e099be00076aa917932b0e9e
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418568"
---
# <a name="devpkey_device_driverversion"></a>DEVPKEY_Device_DriverVersion


PKEY_Device_DriverVersion デバイスプロパティは、現在デバイスインスタンスにインストールされているドライバーのバージョンを表します。

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
<td align="left"><p>DEVPKEY_Device_DriverVersion</p></td>
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
<td align="left"><p><strong>対応するレジストリ値の識別子とレジストリ値の名前</strong></p></td>
<td align="left"><p>REGSTR_VAL_DRIVERVERSION</p>
<p><strong>DriverVersion</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

DEVPKEY_Device_DriverVersion の値は、デバイスをインストールする inf ファイルの inf[**バージョンセクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)に含まれている[**inf DriverVer ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)によって提供されるか、デバイスをインストールする[**inf *ddinstall*セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)に含まれるデバイス固有の inf **DriverVer**ディレクティブによって提供されます。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出して、PKEY_Device_DriverVersion の値を取得できます。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートしていますが、DEVPKEY_Device_DriverVersion プロパティキーをサポートしていません。 以前のバージョンの Windows では、デバイスインスタンスのソフトウェアキーの下にある対応する**Driverversion**レジストリ値にアクセスすることによって、このプロパティの値にアクセスできます。 以前のバージョンの Windows でこのプロパティ値にアクセスする方法の詳細については、「[デバイスドライバーのプロパティ](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-driver-properties)へのアクセス」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**INF *Ddinstall*セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)

[**INF DriverVer ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)

[**INF Version セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






