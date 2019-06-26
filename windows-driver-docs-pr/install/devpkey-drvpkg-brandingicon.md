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
ms.openlocfilehash: 170ee952fb65d498426fcb1a66f8d73d67113310
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377290"
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

DEVPKEY_DrvPkg_BrandingIcon によっての値を設定することができます、 [ **INF AddProperty ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addproperty-directive)に含まれている、 [ **INF *DDInstall*セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)のデバイスをインストールする INF ファイル。 DEVPKEY_DrvPkg_BrandingIcon の値を取得するには呼び出すことによって[ **SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)します。

<a name="requirements"></a>必要条件
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

[**INF AddProperty ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addproperty-directive)

[**INF *DDInstall*セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






