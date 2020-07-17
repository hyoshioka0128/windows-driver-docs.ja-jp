---
title: DEVPKEY_DeviceInterface_FriendlyName
description: DEVPKEY_DeviceInterface_FriendlyName
ms.assetid: 398618a2-621b-477f-b90b-127e8df24b3d
keywords:
- デバイスとドライバーのインストールの DEVPKEY_DeviceInterface_FriendlyName
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceInterface_FriendlyName
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 67bb065765dac77d90e4ac682602f99f42ff4a20
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418219"
---
# <a name="devpkey_deviceinterface_friendlyname"></a>DEVPKEY_DeviceInterface_FriendlyName


DEVPKEY_DeviceInterface_FriendlyName デバイスプロパティは、デバイスインターフェイスのフレンドリ名を表します。

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
<td align="left"><p>DEVPKEY_DeviceInterface_FriendlyName</p></td>
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
<td align="left"><p><strong>対応するレジストリ値の名前</strong></p></td>
<td align="left"><p><strong>フレンドリ</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>はい</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

デバイスインターフェイスクラスの**FriendlyName**レジストリ値は、Inf ddinstall に含まれている[**inf addinterface ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive)によって設定され[**ます。 *DDInstall***](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-interfaces-section)デバイスインターフェイスをインストールする INF ファイルの interface セクション。

Windows は、インターフェイスの[**DEVPKEY_NAME**](devpkey-name--device-interface-.md)デバイスプロパティの値を DEVPKEY_DeviceInterface_FriendlyName の値に設定します。 ユーザーインターフェイス項目内のデバイスインターフェイスを識別するには、DEVPKEY_DeviceInterface_FriendlyName の値ではなく、デバイスインターフェイスの DEVPKEY_NAME の値を使用します。

DEVPKEY_DeviceInterface_FriendlyName の値を取得するには、 [**Setupdigetdeviceinterfaceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)を呼び出し、 [**setupdigetdeviceinterfaceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)を呼び出して設定します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートしていますが、DEVPKEY_DeviceInterface_FriendlyName プロパティキーをサポートしていません。 このプロパティの値にアクセスするには、デバイスインターフェイスの対応する**FriendlyName**レジストリエントリの値にアクセスします。 デバイスインターフェイスのレジストリエントリ値にアクセスする方法の詳細については、「[デバイスインターフェイスのプロパティ](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-interface-properties)へのアクセス」を参照してください。

デバイスインターフェイスの詳細については、「[デバイスインターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)」と「 [**INF addinterface ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive)」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**DEVPKEY_NAME (デバイス インターフェイス)**](devpkey-name--device-interface-.md)

[**INF AddInterface ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive)

[**INF *Ddinstall*。インターフェイスセクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-interfaces-section)

[**SetupDiGetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)

[**SetupDiOpenDeviceInterfaceRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey)

[**SetupDiSetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)

 

 






