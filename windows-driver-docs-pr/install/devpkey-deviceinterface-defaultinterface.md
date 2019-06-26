---
title: DEVPKEY_DeviceInterfaceClass_DefaultInterface
description: DEVPKEY_DeviceInterfaceClass_DefaultInterface
ms.assetid: dab341d1-6cab-420b-9ee0-acf6747e2dac
keywords:
- DEVPKEY_DeviceInterfaceClass_DefaultInterface デバイスとドライバーのインストール
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
ms.openlocfilehash: 62d2e482b17d433c4c14fada88233cb5dd102270
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377294"
---
# <a name="devpkeydeviceinterfaceclassdefaultinterface"></a>DEVPKEY_DeviceInterfaceClass_DefaultInterface


DEVPKEY_DeviceInterfaceClass_DefaultInterface デバイス プロパティは、デバイスのインターフェイス クラスの既定デバイス インターフェイスのシンボリック リンクの名前を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceInterfaceClass_DefaultInterface</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>読み取りおよび書き込みアクセス アプリケーションをインストールしてインストーラー</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

インストールして、デバイスのインターフェイスを使用して確認する方法については[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)と[ **INF AddInterface ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive)します。

DEVPKEY_DeviceInterfaceClass_DefaultInterface の値を取得するには呼び出すことによって[ **SetupDiGetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)します。 呼び出して DEVPKEY_DeviceInterfaceClass_DefaultInterface を設定する[ **SetupDiSetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_DeviceInterfaceClass_DefaultInterface プロパティのキーをサポートしていません。 Windows の以前のバージョンのデバイスのインターフェイス クラスの既定のインターフェイスにアクセスする方法については、次を参照してください。[インターフェイス クラス プロパティのデバイスへのアクセス](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-interface-class-properties)します。

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
<td align="left"><p>Windows Vista および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h (Devpkey.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**INF AddInterface ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive)

[**SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)

[**SetupDiGetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)

[**SetupDiSetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)

 

 






