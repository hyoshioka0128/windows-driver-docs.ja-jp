---
title: DEVPKEY_DeviceInterface_ClassGuid
description: DEVPKEY_DeviceInterface_ClassGuid
ms.assetid: f7346189-9986-4b26-b059-b1a58c8313d1
keywords:
- DEVPKEY_DeviceInterface_ClassGuid デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceInterface_ClassGuid
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3156d69db3a3ced33ad42cc32bf5c5432098ee26
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381496"
---
# <a name="devpkeydeviceinterfaceclassguid"></a>DEVPKEY_DeviceInterface_ClassGuid


DEVPKEY_DeviceInterface_ClassGuid デバイス プロパティは、デバイス インターフェイスのクラスを識別する GUID を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceInterface_ClassGuid</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-guid.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_GUID&lt;/strong&gt;](devprop-type-guid.md)"><strong>DEVPROP_TYPE_GUID</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

形式 {0}*デバイス インターフェイス-クラス*} キーの値は"{*nnnnnnnn*-*nnnn*-*nnnn* -*nnnn*-*nnnnnnnnnnnn*}"ここで、各*n*は 16 進数。

呼び出すことができます[ **SetupDiGetDeviceInterfaceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551122) DEVPKEY_DeviceInterface_ClassGuid の値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_DeviceInterface_ClassGuid プロパティのキーをサポートしていません。 以前のバージョンの Windows 上のデバイス インターフェイスのクラス GUID を取得する方法については、使用する方法に関する情報を参照してください[ **SetupDiEnumDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff551015)で提供されている。[デバイス インターフェイスのプロパティにアクセスする](https://msdn.microsoft.com/library/windows/hardware/ff537740)します。

インストールして表示デバイスのインターフェイスにアクセスする方法については[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)と[ **INF AddInterface ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546310)します。

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


[**INF AddInterface ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546310)

[**SetupDiEnumDeviceInterfaces**](https://msdn.microsoft.com/library/windows/hardware/ff551015)

[**SetupDiGetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551122)

 

 






