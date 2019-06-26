---
title: 一般的な WIA ユーティリティの関数
description: 一般的な WIA ユーティリティの関数
ms.assetid: 235c07a1-4903-4df6-b29f-0ecc342782b4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17d0ee16270e306db6abfb9e4bf92b73254f88dc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370600"
---
# <a name="general-wia-utility-functions"></a>一般的な WIA ユーティリティの関数





ドライバーのコンテキスト アイテムを取得、システム レジストリから情報を取得、文字列のコピーを次の関数を使用できます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaugetdrvitemcontext" data-raw-source="[&lt;strong&gt;wiauGetDrvItemContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaugetdrvitemcontext)"><strong>wiauGetDrvItemContext</strong></a></p></td>
<td><p>ドライバーのコンテキスト アイテムと、必要に応じて、ドライバーの項目を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaugetresourcestring" data-raw-source="[&lt;strong&gt;wiauGetResourceString&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaugetresourcestring)"><strong>wiauGetResourceString</strong></a></p></td>
<td><p>格納することとして、リソース文字列を取得、 <strong>BSTR</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaugetvalidformats" data-raw-source="[&lt;strong&gt;wiauGetValidFormats&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaugetvalidformats)"><strong>wiauGetValidFormats</strong></a></p></td>
<td><p>呼び出し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvGetWiaFormatInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo)"> <strong>IWiaMiniDrv::drvGetWiaFormatInfo</strong> </a>メソッドし、指定したフラグの値を使用して、有効な形式の一覧を作成します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaupropinpropspec" data-raw-source="[&lt;strong&gt;wiauPropInPropSpec&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaupropinpropspec)"><strong>wiauPropInPropSpec</strong></a></p></td>
<td><p>このような値の配列で指定したプロパティの指定の識別子 (ID) が含まれているかどうかを判断します。 関数は、必要に応じてインデックスを取得しますプロパティ仕様 ID が見つかりました。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaupropsinpropspec" data-raw-source="[&lt;strong&gt;wiauPropsInPropSpec&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaupropsinpropspec)"><strong>wiauPropsInPropSpec</strong></a></p></td>
<td><p>プロパティで指定の Id の一覧のいずれかがこのような値の配列内に含まれるかどうかを判断します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaureggetdwordw" data-raw-source="[&lt;strong&gt;wiauRegGetDword&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaureggetdwordw)"><strong>wiauRegGetDword</strong></a></p></td>
<td><p>取得、 <strong>DWORD</strong>値から、 <strong>DeviceData</strong>レジストリのセクション。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaureggetstrw" data-raw-source="[&lt;strong&gt;wiauRegGetStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaureggetstrw)"><strong>wiauRegGetStr</strong></a></p></td>
<td><p>文字列値を取得、 <strong>DeviceData</strong>レジストリのセクション。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiauregopendataw" data-raw-source="[&lt;strong&gt;wiauRegOpenData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiauregopendataw)"><strong>wiauRegOpenData</strong></a></p></td>
<td><p>開く、 <strong>DeviceData</strong>レジストリ キー。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiausetimageitemsize" data-raw-source="[&lt;strong&gt;wiauSetImageItemSize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiausetimageitemsize)"><strong>wiauSetImageItemSize</strong></a></p></td>
<td><p>(Microsoft Windows SDK のドキュメントで定義されている) 現在の WIA_IPA_FORMAT 設定に基づいて、イメージのバイト単位の幅とサイズを計算し、適切なプロパティに新しい値を書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaustrc2c" data-raw-source="[&lt;strong&gt;wiauStrC2C&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaustrc2c)"><strong>wiauStrC2C</strong></a></p></td>
<td><p>ANSI コピーは文字を ANSI 文字の文字列を別の文字列です。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaustrc2w" data-raw-source="[&lt;strong&gt;wiauStrC2W&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaustrc2w)"><strong>wiauStrC2W</strong></a></p></td>
<td><p>ANSI 文字の文字列を Unicode 文字列に変換します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaustrw2c" data-raw-source="[&lt;strong&gt;wiauStrW2C&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaustrw2c)"><strong>wiauStrW2C</strong></a></p></td>
<td><p>Unicode 文字列を ANSI 文字の文字列に変換します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaustrw2w" data-raw-source="[&lt;strong&gt;wiauStrW2W&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaustrw2w)"><strong>wiauStrW2W</strong></a></p></td>
<td><p>Unicode のコピーは、他の Unicode 文字列に文字列です。</p></td>
</tr>
</tbody>
</table>

 

 

 




