---
title: 一般的な WIA ユーティリティの関数
description: 一般的な WIA ユーティリティの関数
ms.assetid: 235c07a1-4903-4df6-b29f-0ecc342782b4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cdce15f2994b3c3f1e833c82c350d3e39f752f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840837"
---
# <a name="general-wia-utility-functions"></a>一般的な WIA ユーティリティの関数





次の関数を使用すると、ドライバーの項目コンテキストを取得し、システムレジストリから情報を取得して、文字列をコピーできます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaugetdrvitemcontext" data-raw-source="[&lt;strong&gt;wiauGetDrvItemContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaugetdrvitemcontext)"><strong>wiauGetDrvItemContext</strong></a></p></td>
<td><p>ドライバー項目コンテキストと、必要に応じてドライバー項目を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaugetresourcestring" data-raw-source="[&lt;strong&gt;wiauGetResourceString&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaugetresourcestring)"><strong>Wi/Getresourcestring</strong></a></p></td>
<td><p><strong>BSTR</strong>として格納されているリソース文字列を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaugetvalidformats" data-raw-source="[&lt;strong&gt;wiauGetValidFormats&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaugetvalidformats)"><strong>Wi/Getvalidformats</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvGetWiaFormatInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo)"><strong>IWiaMiniDrv::D rvgetwiaformatinfo</strong></a>メソッドを呼び出し、指定された TYMED 値を使用して有効な形式の一覧を作成します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaupropinpropspec" data-raw-source="[&lt;strong&gt;wiauPropInPropSpec&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaupropinpropspec)"><strong>Wi/Propinpropspec</strong></a></p></td>
<td><p>指定されたプロパティ仕様識別子 (ID) が、そのような値の配列に含まれているかどうかを判断します。 関数は、必要に応じて、プロパティの指定 ID が見つかったインデックスを取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaupropsinpropspec" data-raw-source="[&lt;strong&gt;wiauPropsInPropSpec&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaupropsinpropspec)"><strong>Wi/Propsinpropspec</strong></a></p></td>
<td><p>プロパティ指定 Id のリストのいずれかが、このような値の配列内に含まれているかどうかを判断します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaureggetdwordw" data-raw-source="[&lt;strong&gt;wiauRegGetDword&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaureggetdwordw)"><strong>Wi# reggetdword</strong></a></p></td>
<td><p>レジストリの<strong>Devicedata</strong>セクションから<strong>DWORD</strong>値を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaureggetstrw" data-raw-source="[&lt;strong&gt;wiauRegGetStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaureggetstrw)"><strong>Wi# reggetstr</strong></a></p></td>
<td><p>レジストリの<strong>Devicedata</strong>セクションから文字列値を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiauregopendataw" data-raw-source="[&lt;strong&gt;wiauRegOpenData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiauregopendataw)"><strong>wiauRegOpenData</strong></a></p></td>
<td><p><strong>Devicedata</strong>レジストリキーを開きます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiausetimageitemsize" data-raw-source="[&lt;strong&gt;wiauSetImageItemSize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiausetimageitemsize)"><strong>wiauSetImageItemSize</strong></a></p></td>
<td><p>Microsoft Windows SDK のドキュメントで定義されている現在の WIA_IPA_FORMAT 設定に基づいて、イメージのサイズと幅をバイト単位で計算し、適切なプロパティに新しい値を書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaustrc2c" data-raw-source="[&lt;strong&gt;wiauStrC2C&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaustrc2c)"><strong>wiauStrC2C</strong></a></p></td>
<td><p>ANSI 文字列を別の ANSI 文字列にコピーします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaustrc2w" data-raw-source="[&lt;strong&gt;wiauStrC2W&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaustrc2w)"><strong>wiauStrC2W</strong></a></p></td>
<td><p>ANSI 文字列を Unicode 文字列に変換します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaustrw2c" data-raw-source="[&lt;strong&gt;wiauStrW2C&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaustrw2c)"><strong>wiauStrW2C</strong></a></p></td>
<td><p>Unicode 文字列を ANSI 文字列に変換します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaustrw2w" data-raw-source="[&lt;strong&gt;wiauStrW2W&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaustrw2w)"><strong>wiauStrW2W</strong></a></p></td>
<td><p>Unicode 文字列を別の Unicode 文字列にコピーします。</p></td>
</tr>
</tbody>
</table>

 

 

 




