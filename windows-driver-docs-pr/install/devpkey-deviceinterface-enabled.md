---
title: DEVPKEY_DeviceInterface_Enabled
description: DEVPKEY_DeviceInterface_Enabled
ms.assetid: 8e7ea36c-827d-43bd-b424-41c06ba8c20d
keywords:
- デバイスとドライバーのインストールの DEVPKEY_DeviceInterface_Enabled
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceInterface_Enabled
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: da0fed10b95104a977ad20f419f7f259f907665d
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418526"
---
# <a name="devpkey_deviceinterface_enabled"></a>DEVPKEY_DeviceInterface_Enabled


**Deviceinterfaceenabled**デバイスプロパティは、デバイスインターフェイスが有効になっているかどうかを示すブール型のフラグを表します。

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
<td align="left"><p>DEVPKEY_DeviceInterface_Enabled</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>インストールアプリケーションおよびインストーラーによる読み取り専用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

DEVPKEY_DeviceInterface_Enabled の値が DEVPROP_TRUE 場合は、インターフェイスが有効になります。 それ以外の場合、インターフェイスは有効になりません。

[**Setupdigetdeviceinterfaceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)を呼び出して、DEVPKEY_DeviceInterface_Enabled の値を取得できます。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートしていますが、DEVPKEY_DeviceInterface_Enabled プロパティキーをサポートしていません。 以前のバージョンの Windows でデバイスインターフェイスのアクティビティの状態を取得する方法については、「[デバイスインターフェイスのプロパティへのアクセス](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-interface-properties)」に用意されている[**Setupdienumdeviceinterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)の使用方法に関する情報を参照してください。

デバイスインターフェイスの詳細については、「[デバイスインターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)」と「 [**INF addinterface ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive)」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**INF AddInterface ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive)

[**SetupDiEnumDeviceInterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)

[**SetupDiGetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)

 

 






