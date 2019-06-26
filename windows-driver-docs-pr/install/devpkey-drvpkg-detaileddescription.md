---
title: DEVPKEY_DrvPkg_DetailedDescription
description: DEVPKEY_DrvPkg_DetailedDescription
ms.assetid: ee9080d1-8c66-42b3-af48-cb1fbfc332e2
keywords:
- DEVPKEY_DrvPkg_DetailedDescription デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DrvPkg_DetailedDescription
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: da5d3433eb6603bacf3c76370a73f38446ef27d0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377285"
---
# <a name="devpkeydrvpkgdetaileddescription"></a>DEVPKEY_DrvPkg_DetailedDescription


DEVPKEY_DrvPkg_DetailedDescription デバイス プロパティは、デバイスのインスタンスの機能の詳細な説明を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DrvPkg_DetailedDescription</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>データ形式</strong></p></td>
<td align="left"><p>限られた XML タグ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>〇</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

詳細な説明文字列は XML 形式です。 XML 形式を使うと、Windows がサポートされているハイパー テキスト マークアップ言語 (HTML) タグの次のサブセットに基づく情報の表示形式を設定します。 これらのタグの操作では、HTML タグの操作に似ています。

<a href="" id="heading-level-tags"></a>見出しレベルのタグ  
&lt;h1&gt;、 &lt;h2&gt;、 &lt;h3&gt;

<a href="" id="list-tags"></a>タグの一覧  
&lt;ul&gt;、 &lt;ol&gt;、 &lt;li&gt;

<a href="" id="paragraph-tag"></a>段落タグ  
&lt;p&gt;

DEVPKEY_DrvPkg_DetailedDescription によっての値を設定することができます、 [ **INF AddProperty ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addproperty-directive)に含まれている、 [ **INF *DDInstall*セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)のデバイスをインストールする INF ファイル。 DEVPKEY_DrvPkg_DetailedDescription の値を取得するには呼び出すことによって[ **SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)します。

次に、INF を使用する方法の例**AddProperty** DEVPKEY_DrvPkg_DetailedDescription、INF によってインストールされているデバイス インスタンスの値を設定するディレクティブ*DDInstall*セクション"SampleDDInstallSection":

```cpp
[SampleDDinstallSection]
...
AddProperty=SampleAddPropertySection
...

[SampleAddPropertySection] 
DeviceDetailedDescription,,,,"<xml><h1>Microsoft DiscoveryCam 530</h1><h2>Overview<h2>The Microsoft DiscoveryCam is great.<p>Really.<p><h2>Features</h2>The Microsoft DiscoveryCam has three features.<ol><li>Feature 1</li><li>Feature 2</li><li>Feature 3</li></ol></xml>"
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


[**INF AddProperty ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addproperty-directive)

[**INF *DDInstall*セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






