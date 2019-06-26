---
title: installHeaderTitle XML 要素
description: installHeaderTitle XML 要素
ms.assetid: 43f8611c-9504-46ab-a8f2-06141bf74f1f
keywords:
- installHeaderTitle XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- installHeaderTitle XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dd3d1fa07d9182f26addda55e6e3f5ff02315fe4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370006"
---
# <a name="installheadertitle-xml-element"></a>installHeaderTitle XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)します。\]

**InstallHeaderTitle** XML 要素が DPInst のインストール ページに表示されるインストール ヘッダー タイトルの太字のテキストをカスタマイズします。

### <a name="element-tag"></a>要素タグ

```cpp
<installHeaderTitle>
```

### <a name="xml-attributes"></a>XML 属性

なし

### <a name="element-information"></a>要素情報

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>親要素</strong></p></td>
<td align="left"><p><a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"><strong>言語</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>データの内容</strong></p></td>
<td align="left"><p>文字列、インストール ページのタイトルのテキストをカスタマイズします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素が重複しています</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>「解説」

次のコード例に示します、 **installHeaderTitle**インストール ページのタイトルのテキストをカスタマイズする要素。 カスタム インストール ヘッダーのタイトルを指定するテキストが太字のフォント スタイルで表示されます。

```cpp
<dpinst>
  ...
  <language code="0x0409">
    ...
    <installHeaderTitle>Installing the software for your Toaster device...</installHeaderTitle>
    ...
  </language>
  ...
</dpinst>
```

場合、 **installHeaderTitle**要素が指定されていない、DPInst は既定のインストール ページに表示される既定のタイトル テキストを表示します。

## <a name="see-also"></a>関連項目


[**言語**](language-xml-element.md)

 

 






