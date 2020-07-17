---
title: DEVPKEY_Device_ResourcePickerExceptions
description: DEVPKEY_Device_ResourcePickerExceptions
ms.assetid: 65a2c709-fe3a-44e2-90f9-4ad6dbcb50bd
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_ResourcePickerExceptions
topic_type:
- apiref
api_name:
- DEVPKEY_Device_ResourcePickerExceptions
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 30b3382ae2d82f99ce657812ef579f075a56ac13
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418430"
---
# <a name="devpkey_device_resourcepickerexceptions"></a>DEVPKEY_Device_ResourcePickerExceptions


デバイスの DEVPKEY_Device_ResourcePickerExceptions プロパティは、デバイスインスタンスで許可されているリソースの競合を表します。

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
<td align="left"><p>DEVPKEY_Device_ResourcePickerExceptions</p></td>
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
<td align="left"><p>REGSTR_VAL_RESOURCE_PICKER_EXCEPTIONS</p>
<p><strong>ResourcePickerExceptions</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

DEVPKEY_Device_ResourcePickerExceptions の値は、デバイスをインストールする inf ファイルの inf [** *ddinstall*セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)に含まれている[**inf AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)を使用して設定できます。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出すことによって DEVPKEY_Device_ResourcePickerExceptions の値を取得できます。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートしていますが、DEVPKEY_Device_ResourcePickerExceptions プロパティキーをサポートしていません。 以前のバージョンの Windows では、デバイスインスタンスのソフトウェアキーの下にある対応する**ResourcePickerExceptions**レジストリ値にアクセスすることによって、このプロパティの値にアクセスできます。 以前のバージョンの Windows でこのプロパティ値にアクセスする方法の詳細については、「[デバイスドライバーのプロパティ](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-driver-properties)へのアクセス」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)

[**INF *Ddinstall*セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






