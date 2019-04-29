---
title: DEVPKEY_DrvPkg_BrandingIcon
description: DEVPKEY_DrvPkg_BrandingIcon
ms.assetid: 4a830401-5677-4fda-a087-407b1246699f
keywords:
- DEVPKEY_DrvPkg_BrandingIcon デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DrvPkg_BrandingIcon
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2d11bcb467ab7c7e113020f09f189d76a3e78405
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335283"
---
# <a name="devpkeydrvpkgbrandingicon"></a>DEVPKEY_DrvPkg_BrandingIcon


DEVPKEY_DrvPkg_BrandingIcon デバイス プロパティは、ベンダーとデバイスのインスタンスに関連付けるアイコンの一覧を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DrvPkg_BrandingIcon</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
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

.Ico ファイル、または実行可能ファイル内のリソースとして、ブランド アイコンを指定できます。

アイコンの一覧の形式は説明のと同じ、 [ **DEVPKEY_DrvPkg_Icon** ](devpkey-drvpkg-icon.md)デバイス プロパティ。

DEVPKEY_DrvPkg_BrandingIcon によっての値を設定することができます、 [ **INF AddProperty ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546318)に含まれている、 [ **INF *DDInstall*セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)のデバイスをインストールする INF ファイル。 DEVPKEY_DrvPkg_BrandingIcon の値を取得するには呼び出すことによって[ **SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)します。

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


[**DEVPKEY_DrvPkg_Icon**](devpkey-drvpkg-icon.md)

[**INF AddProperty ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546318)

[**INF *DDInstall*セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






