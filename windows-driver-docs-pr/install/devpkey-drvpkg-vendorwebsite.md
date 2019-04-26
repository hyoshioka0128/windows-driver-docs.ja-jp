---
title: DEVPKEY_DrvPkg_VendorWebSite
description: DEVPKEY_DrvPkg_VendorWebSite
ms.assetid: 5a460073-64ec-4f86-af18-ddd065ed03b1
keywords:
- DEVPKEY_DrvPkg_VendorWebSite デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DrvPkg_VendorWebSite
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3a064f71e53857bb1b350aa30be5e775377afba8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342360"
---
# <a name="devpkeydrvpkgvendorwebsite"></a>DEVPKEY_DrvPkg_VendorWebSite


DEVPKEY_DrvPkg_VendorWebSite デバイス プロパティは、デバイスのインスタンスのベンダーの URL を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DrvPkg_VendorWebSite</p></td>
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

URL は、ベンダーの web サイト、web サイト、またはリダイレクト ページ内で web ページのルートへのリンクを指定できます。 URL パラメーターを含めることも、たとえば、次の URL が含まれている、 **prod** "DSC530"製品識別子を提供するパラメーターと**rev**パラメーター数「34」を提供します。

```cpp
http://www.microsoft.com/redirect?prod=DSC530&rev=34
```

DEVPKEY_DrvPkg_VendorWebSite によっての値を設定することができます、 [ **INF AddProperty ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546318)に含まれている、 [ **INF DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)のデバイスをインストールする INF ファイル。 DEVPKEY_DrvPkg_VendorWebSite の値を取得するには呼び出すことによって[ **SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)します。

次に、INF を使用する方法の例**AddProperty** 、INF によってインストールされているデバイスの DEVPKEY_DrvPkg_VendorWebSite プロパティ値を設定するディレクティブ*DDInstall*セクション"SampleDDInstallSection":

```cpp
[SampleDDinstallSection]
...
AddProperty=SampleAddPropertySection
...

[SampleAddPropertySection] 
DeviceVendorWebsite,,,,"http://www.microsoft.com/redirect?prod=DSC530&rev=34"
...
```

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


[**INF AddProperty ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546318)

[**INF *DDInstall*セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






