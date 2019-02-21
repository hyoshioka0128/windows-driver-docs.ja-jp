---
title: DEVPKEY_NAME (デバイス インターフェイス)
description: DEVPKEY_NAME (デバイス インターフェイス)
ms.assetid: 276862d0-8ab9-4914-9e57-834cc17d0e59
keywords:
- DEVPKEY_NAME (デバイス インターフェイス) デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_NAME (Device Interface)
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 96d917d97f39fefc1117d19228251d0f792e4314
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531058"
---
# <a name="devpkeyname-device-interface"></a>DEVPKEY_NAME (デバイス インターフェイス)


DEVPKEY_NAME デバイス インターフェイスのプロパティは、デバイス インターフェイスの名前を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_NAME</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって読み取り専用アクセス。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>〇</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ユーザー インターフェイスの項目で、エンドユーザーへのインターフェイスを識別するために、DEVPKEY_NAME の値を使用する必要があります。

DEVPKEY_NAME の値の値と同じ、 [ **DEVPKEY_DeviceInterface_FriendlyName** ](devpkey-deviceinterface-friendlyname.md) DEVPKEY_DeviceInterface_FriendlyName が設定されている場合、デバイス プロパティ。 それ以外の場合、DEVPKEY_NAME は存在しません。

DEVPKEY_NAME の値を取得するには呼び出すことによって[ **SetupDiGetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551122)します。

デバイスのインターフェイスについては、次を参照してください。[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)と[ **INF AddInterface ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546310)します。

Windows Server 2003、Windows XP、および Windows 2000 は、対応する名前プロパティを直接サポートされません。 ただし、Windows の以前のバージョンは、DEVPKEY_DeviceInterface_FriendlyName に対応するプロパティをサポートする操作を行います。

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


[**DEVPKEY_DeviceInterface_FriendlyName**](devpkey-deviceinterface-friendlyname.md)

[**INF AddInterface ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546310)

[**SetupDiGetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551122)

 

 






