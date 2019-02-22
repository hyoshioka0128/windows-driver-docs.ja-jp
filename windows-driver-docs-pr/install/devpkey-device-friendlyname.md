---
title: DEVPKEY_Device_FriendlyName
description: DEVPKEY_Device_FriendlyName
ms.assetid: 0acea25e-5068-441b-be6b-fa863d1bdba2
keywords:
- DEVPKEY_Device_FriendlyName デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_FriendlyName
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f01dcf1ca6d06f1fa5de5642986641f91543b183
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553628"
---
# <a name="devpkeydevicefriendlyname"></a>DEVPKEY_Device_FriendlyName


DEVPKEY_Device_FriendlyName デバイス プロパティは、デバイスのインスタンスのフレンドリ名を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_FriendlyName</p></td>
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
<td align="left"><p><strong>対応する SPDRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPDRP_FRIENDLYNAME</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

使用することができます、 [ **DEVPKEY_NAME** ](devpkey-name--device-instance-.md) DEVPKEY_Device_FriendlyName ユーザー インターフェイスの表示でデバイスのインスタンスを識別する名前を表示するのではなくデバイス プロパティ。

使用して DEVPKEY_Device_FriendlyName の値を設定することができます、 [ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)に含まれている、 [ **INF *DDInstall*.ハードウェア セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547330)でデバイスをインストールする INF ファイル。

DEVPKEY_Device_FriendlyName の値を取得するには呼び出すことによって[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)呼び出すことによってこのプロパティを設定することも[ **SetupDiSetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552163)します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_Device_FriendlyName プロパティのキーをサポートしていません。 代わりに、Windows の以前のバージョンのプロパティの値へのアクセスに対応する SPDRP_FRIENDLYNAME 識別子を使用することができます。 Windows の以前のバージョンでこのプロパティの値にアクセスする方法については、次を参照してください。[デバイス インスタンス SPDRP_Xxx プロパティへのアクセス](https://msdn.microsoft.com/library/windows/hardware/ff537737)します。

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


[**DEVPKEY_NAME (デバイス インスタンス)**](devpkey-name--device-instance-.md)

[**INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)

[**INF *DDInstall*します。ハードウェア セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547330)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

[**SetupDiSetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552163)

 

 






