---
title: DEVPKEY_Device_DriverRank
description: DEVPKEY_Device_DriverRank
ms.assetid: 9a6a8e9f-fd3c-4a64-b0d2-565cda0dae52
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_DriverRank
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DriverRank
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1edf9eb8a4ad38f1b1a981cf5ef0a2b71599397f
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418571"
---
# <a name="devpkey_device_driverrank"></a>DEVPKEY_Device_DriverRank


DEVPKEY_Device_DriverRank デバイスプロパティは、デバイスインスタンスにインストールされているドライバーのランクを表します。

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
<td align="left"><p>DEVPKEY_Device_DriverRank</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-uint32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_UINT32&lt;/strong&gt;](devprop-type-uint32.md)"><strong>DEVPROP_TYPE_UINT32</strong></a></p></td>
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

DEVPKEY_Device_DriverRank の値が設定されます。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出して、DEVPKEY_Device_DriverRank の値を取得できます。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートしていますが、DEVPKEY_Device_DriverRank プロパティキーをサポートしていません。 以前のバージョンの Windows でこのプロパティにアクセスする方法の詳細については、「[デバイスドライバーのプロパティ](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-driver-properties)へのアクセス」を参照してください。

ドライバーランクの詳細については、「 [Windows がドライバーをランク付けする方法](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-ranks-drivers)」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiGetDriverInstallParams**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdriverinstallparamsa)

[**SP_DRVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_drvinstall_params)

 

 






