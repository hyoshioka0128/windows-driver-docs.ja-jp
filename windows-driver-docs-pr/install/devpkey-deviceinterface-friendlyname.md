---
title: DEVPKEY_DeviceInterface_FriendlyName
description: DEVPKEY_DeviceInterface_FriendlyName
ms.assetid: 398618a2-621b-477f-b90b-127e8df24b3d
keywords:
- DEVPKEY_DeviceInterface_FriendlyName デバイスとドライバーのインストール
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
ms.openlocfilehash: 3663da355ec776d50c0519c0bd960c133f8765d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529635"
---
# <a name="devpkeydeviceinterfacefriendlyname"></a>DEVPKEY_DeviceInterface_FriendlyName


DEVPKEY_DeviceInterface_FriendlyName デバイス プロパティは、デバイス インターフェイスのフレンドリ名を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceInterface_FriendlyName</p></td>
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
<td align="left"><p><strong>対応するレジストリ値の名前</strong></p></td>
<td align="left"><p><strong>FriendlyName</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>〇</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**FriendlyName**デバイス インターフェイス クラスのレジストリ値によって設定されます、 [ **INF AddInterface ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546310)に含まれている、 [ **INF *DDInstall*します。インターフェイス セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547335)のデバイスのインターフェイスをインストールする INF ファイル。

Windows 設定の値、 [ **DEVPKEY_NAME** ](devpkey-name--device-interface-.md) DEVPKEY_DeviceInterface_FriendlyName の値へのインターフェイスのデバイス プロパティ。 ユーザー インターフェイスの項目でデバイスのインターフェイスを識別するには、DEVPKEY_DeviceInterface_FriendlyName の値ではなく、デバイス インターフェイスの DEVPKEY_NAME の値を使用します。

呼び出すことによって、DEVPKEY_DeviceInterface_FriendlyName の値を取得する[ **SetupDiGetDeviceInterfaceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551122)し、呼び出すことによって設定[ **SetupDiSetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552158)します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_DeviceInterface_FriendlyName プロパティのキーをサポートしていません。 このプロパティの値をアクセスするには、対応するのにアクセスして**FriendlyName**デバイス インターフェイスのレジストリ エントリの値。 デバイスのインターフェイスのレジストリ エントリの値にアクセスする方法については、次を参照してください。[デバイス インターフェイスのプロパティへのアクセス](https://msdn.microsoft.com/library/windows/hardware/ff537740)します。

デバイスのインターフェイスについては、次を参照してください。[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)と[ **INF AddInterface ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546310)します。

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


[**DEVPKEY_NAME (デバイス インターフェイス)**](devpkey-name--device-interface-.md)

[**INF AddInterface ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546310)

[**INF *DDInstall*します。インターフェイス セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547335)

[**SetupDiGetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551122)

[**SetupDiOpenDeviceInterfaceRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff552075)

[**SetupDiSetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552158)

 

 






