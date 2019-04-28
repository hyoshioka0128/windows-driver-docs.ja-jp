---
title: DEVPKEY_DeviceInterface_Enabled
description: DEVPKEY_DeviceInterface_Enabled
ms.assetid: 8e7ea36c-827d-43bd-b424-41c06ba8c20d
keywords:
- DEVPKEY_DeviceInterface_Enabled デバイスとドライバーのインストール
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
ms.openlocfilehash: 3eacebe15dc515d84cf0364d1f0783e1991ac15c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381490"
---
# <a name="devpkeydeviceinterfaceenabled"></a>DEVPKEY_DeviceInterface_Enabled


**DeviceInterfaceEnabled**デバイス プロパティは、デバイスのインターフェイスが有効になっているかどうかを示すブール型のフラグを表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceInterface_Enabled</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
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

DEVPKEY_DeviceInterface_Enabled の値が DEVPROP_TRUE の場合は、インターフェイスが有効にします。 それ以外の場合、インターフェイスは無効です。

呼び出すことができます[ **SetupDiGetDeviceInterfaceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551122) DEVPKEY_DeviceInterface_Enabled の値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_DeviceInterface_Enabled プロパティのキーをサポートしていません。 以前のバージョンの Windows 上のデバイス インターフェイスのアクティビティの状態を取得する方法については、使用する方法に関する情報を参照してください[ **SetupDiEnumDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff551015)つまり。提供される[デバイス インターフェイスのプロパティにアクセスする](https://msdn.microsoft.com/library/windows/hardware/ff537740)します。

デバイス インターフェイスの詳細については、次を参照してください。[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)と[ **INF AddInterface ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546310)します。

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

 

 






