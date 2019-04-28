---
title: finishText XML 要素
description: finishText XML 要素
ms.assetid: b8c63f75-e0d3-458f-9265-a19d6f64ac6b
keywords:
- finishText XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- finishText XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 40d0d7d4b1093e6d4d38f7baf2c5cff1e346b9e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377086"
---
# <a name="finishtext-xml-element"></a>finishText XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

**FinishText** XML 要素が DPInst は DPInst の完了 ページに表示されるメインのテキストをカスタマイズします。

### <a name="element-tag"></a>要素タグ

```cpp
<finishText>
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
<td align="left"><p>[完了] ページでメイン テキストをカスタマイズする文字列</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素が重複しています</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>「解説」

次のコード例に示します、 **finishText** DPInst の表示を正常にインストールする [完了] ページでメイン テキストをカスタマイズする要素。 カスタム テキストを [完了] を指定するテキストが太字のフォント スタイルで表示されます。

```cpp
dpinst>
  ...
  <language code="0x0409">
    ...
    <finishText>Enjoy using the Toaster.</finishText>
    ...
  </language>
  ...
</dpinst>
```

場合、 **finishText**要素が指定されていない、DPInst インストールが成功または失敗したかどうかを示す既定の [完了] のテキストを表示します。

## <a name="see-also"></a>関連項目


[**finishTitle**](finishtitle-xml-element.md)

[**言語**](language-xml-element.md)

 

 






