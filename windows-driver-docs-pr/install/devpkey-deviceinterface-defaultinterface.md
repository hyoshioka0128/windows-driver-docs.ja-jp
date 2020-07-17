---
title: DEVPKEY_DeviceInterfaceClass_DefaultInterface
description: DEVPKEY_DeviceInterfaceClass_DefaultInterface
ms.assetid: dab341d1-6cab-420b-9ee0-acf6747e2dac
keywords:
- デバイスとドライバーのインストールの DEVPKEY_DeviceInterfaceClass_DefaultInterface
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceInterfaceClass_DefaultInterface
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7e5aab5edc2715073ba0281b024fa69b369441f2
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418217"
---
# <a name="devpkey_deviceinterfaceclass_defaultinterface"></a>DEVPKEY_DeviceInterfaceClass_DefaultInterface


DEVPKEY_DeviceInterfaceClass_DefaultInterface デバイスプロパティは、デバイスインターフェイスクラスの既定のデバイスインターフェイスのシンボリックリンク名を表します。

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
<td align="left"><p>DEVPKEY_DeviceInterfaceClass_DefaultInterface</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
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

デバイスインターフェイスのインストール方法と使用方法の詳細については、「[デバイスインターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)」と「 [**INF addinterface ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive)」を参照してください。

[**Setupdigetdeviceinterfaceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)を呼び出すことによって、DEVPKEY_DeviceInterfaceClass_DefaultInterface の値を取得できます。 [**Setupdisetdeviceinterfaceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)を呼び出すことによって、DEVPKEY_DeviceInterfaceClass_DefaultInterface を設定できます。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートしていますが、DEVPKEY_DeviceInterfaceClass_DefaultInterface プロパティキーをサポートしていません。 以前のバージョンの Windows でデバイスインターフェイスクラスの既定のインターフェイスにアクセスする方法の詳細については、「[デバイスインターフェイスクラスのプロパティ](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-interface-class-properties)へのアクセス」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**INF AddInterface ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive)

[**SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)

[**SetupDiGetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)

[**SetupDiSetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)

 

 






