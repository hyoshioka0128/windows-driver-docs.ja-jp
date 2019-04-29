---
title: DEVPKEY_NAME (デバイス セットアップ クラス)
description: DEVPKEY_NAME (デバイス セットアップ クラス)
ms.assetid: cc953918-f11a-464c-95cc-ee2a9aa68b7a
keywords:
- DEVPKEY_NAME (デバイス セットアップ クラス) のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_NAME (Device Setup Class)
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3939d28abf4ae90921e48c724f29200e739b1d3d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327499"
---
# <a name="devpkeyname-device-setup-class"></a>DEVPKEY_NAME (デバイス セットアップ クラス)


DEVPKEY_NAME デバイス プロパティの名前を表す、[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)します。

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
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>〇</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

DEVPKEY_NAME の値は、ユーザー インターフェイスの項目で、エンドユーザーのデバイス セットアップ クラスを識別するために使用できます。

DEVPKEY_NAME の値は、の値として同じ DEVPKEY_DeviceClass_Name が設定されている場合、 [ **DEVPKEY_DeviceClass_Name** ](devpkey-deviceclass-name.md)デバイス プロパティ。 それ以外の場合、DEVPKEY_NAME 値は、の値として同じ、 [ **DEVPKEY_DeviceClass_ClassName** ](devpkey-deviceclass-classname.md)デバイス プロパティ。

呼び出すことができます[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)または[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090) DEVPKEY_NAME のデバイスの値を取得するにはセットアップ クラスです。

Windows Server 2003、Windows XP、および Windows 2000 は、対応する名前プロパティを直接サポートされません。 ただし、以前のバージョンの Windows では、DEVPKEY_DeviceClass_Name および DEVPKEY_DeviceClass_ClassName に対応するプロパティをサポートしています。

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


[**DEVPKEY_DeviceClass_ClassName**](devpkey-deviceclass-classname.md)

[**DEVPKEY_DeviceClass_Name**](devpkey-deviceclass-name.md)

[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090)

[**SetupDiGetClassDescription**](https://msdn.microsoft.com/library/windows/hardware/ff551053)

[**SetupDiClassNameFromGuid**](https://msdn.microsoft.com/library/windows/hardware/ff550947)

 

 






