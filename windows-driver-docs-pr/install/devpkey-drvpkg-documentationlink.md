---
title: DEVPKEY_DrvPkg_DocumentationLink
description: DEVPKEY_DrvPkg_DocumentationLink
ms.assetid: a4ae1f6c-edf5-4490-8f92-6d7a24040304
keywords:
- DEVPKEY_DrvPkg_DocumentationLink デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DrvPkg_DocumentationLink
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 264a34e2acde3f4716b94c419656155e14f8c954
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377282"
---
# <a name="devpkeydrvpkgdocumentationlink"></a>DEVPKEY_DrvPkg_DocumentationLink


DEVPKEY_DrvPkg_DocumentationLink デバイスのプロパティは、デバイスのインスタンスは、ドキュメントを URL を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DrvPkg_DocumentationLink</p></td>
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

ドキュメントのリンク URL デバイスに関する情報を含むファイルへのリンクがあります。 このプロパティは、デバイスの Web にアクセス可能なドキュメントを提供するものです。 ファイルは、HTML ページ、 *.pdf*ファイル、 *.doc*ファイル、またはその他のファイルの種類します。 唯一の制限は、URL が指定したファイル内ですべてのドキュメントのコンテンツを含める必要があります。 たとえば、 \* *.htm*自己完結型であるファイルが有効で、 \* *.htm*他のグラフィックス ファイルを参照するファイルが有効でないと\* *.mta*参照先のグラフィック ファイルを含む web アーカイブ ファイルが無効です。

URL は、パラメーターを含めることができます。 たとえば、次の URL が含まれている、 **prod** "DSC530"の値を提供するパラメーター、 **rev** 「34」の値を提供するパラメーターと**型**パラメーターを"doc"の値を指定します。

```cpp
http://www.microsoft.com/redirect?prod=DSC530&rev=34&type=docs
```

マイクロソフトでは、Web ホスティングまたは DEVPKEY_DrvPkg_DocumentationLink プロパティの値で指定されている web ページのリダイレクトを提供していません。 URL は、によって管理されている web ページにリンクする必要があります、[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)プロバイダー。

ユーザーは、エンドユーザーのセットアップで生成されたダイアログ ボックスに表示される web サイトのリンクをクリックすると、Windows には、DEVPKEY_DrvPkg_DocumentationLink によって提供される URL を含む HTTP 要求に、次の情報が追加されます。

-   指定したとおり、Windows バージョン、 **pver**パラメーター。 たとえば、"pver 6.0 ="Windows Vista を指定します。

-   指定された在庫保管単位 (SKU)、 **sbp**プロフェッショナルもパラメーターで、ごとに設定することができます。 たとえば、"sbp pro ="professional edition を指定します。

-   指定されたローカル識別子 (LCID)、 **olcid**パラメーター。 たとえば、"olcid = 0x409"英語 (Standard) の言語を指定します。

-   最も固有のハードウェア識別子で指定されたデバイスの場合、 **pnpid**パラメーター。 たとえば、"pnpid PCI % 5cven_8086% 26dev_2533% 26SUBSYS_00000000 %26rev_04 ="PCI デバイスのハードウェア識別子を指定します。

プライバシー上の理由から、ユーザー情報とデバイスのシリアル番号が含まれていない HTTP 要求で。

```cpp
The following example shows the type of HTTP request that would be sent to a web server: http://www.microsoft.com/redirect?prod=DSC530&rev34&type=docs&pver=6.0&spb=pro&olcid=0x409&pnpid=PCI%5CVEN_8086%26DEV_2533%26SUBSYS_00000000%26REV_04
```

DEVPKEY_DrvPkg_DocumentationLink によっての値を設定することができます、 [ **INF AddProperty ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addproperty-directive)に含まれている、 [ **INF *DDInstall*セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)のデバイスをインストールする INF ファイル。 DEVPKEY_DrvPkg_DocumentationLinkproperty の値を取得するには呼び出すことによって[ **SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)します。

次に、INF を使用する方法の例**AddProperty** 、INF によってインストールされているデバイスの DEVPKEY_DrvPkg_DocumentationLink の値を設定するディレクティブ*DDInstall*セクション"SampleDDInstallSection":

```cpp
[SampleDDinstallSection]
...
AddProperty=SampleAddPropertySection
...

[SampleAddPropertySection] 
DeviceDocumentationLink,,,,"http://www.microsoft.com/redirect?prod=DSC530&rev34&type="docs"
...
```

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


[**INF AddProperty ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addproperty-directive)

[**INF *DDInstall*セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






