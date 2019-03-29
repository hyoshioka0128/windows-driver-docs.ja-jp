---
title: eula XML 要素
description: eula XML 要素
ms.assetid: ab647583-b0e1-4f40-86af-9b7923f5535c
keywords:
- 使用許諾契約書 XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- eula XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a68d948e02e536b78e5f5df9225134d20c8a497b
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464148"
---
# <a name="eula-xml-element"></a>eula XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

**Eula** XML 要素がカスタム テキスト DPInst EULA ページを含んでいる使用許諾契約書のテキスト ファイルを指定する 2 つの属性を含む空の XML 要素。

### <a name="element-tag"></a>要素タグ

```cpp
<eula>
```

### <a name="xml-attributes"></a>XML 属性

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>型</strong></p></td>
<td align="left"><p>ベンダーから提供された使用許諾契約書の種類。 文字列"txt"は、プレーン テキスト ファイルには、この属性の値を設定する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Path</strong></p></td>
<td align="left"><p>DPInst EULA ページのテキストを含むファイルの名前を識別する文字列。 Utf-8 エンコーディングを使用して、使用許諾契約書のテキスト ファイルをエンコードする必要があります。 DPInst の実行可能ファイルを含むディレクトリである DPInst のルート ディレクトリに、EULA ファイルを配置する必要があります (<em>DPInst.exe</em>)、または DPInst のルート ディレクトリの下のサブディレクトリ。 使用許諾契約書のファイルがサブディレクトリ内にある場合は、DPInst のルート ディレクトリに対して相対的な完全修飾ファイル名を指定します。</p></td>
</tr>
</tbody>
</table>

 

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
<td align="left"><p>許可なし</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素が重複しています</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>「解説」

次のコード例に示します、 **eula**ことを指定する要素*データ\\Eula409.txt*カスタム使用許諾契約書のテキストが含まれています。 *Eula409.txt*ファイルは、*データ*ディレクトリで、DPInst のルート ディレクトリの下のサブディレクトリにある必要があります。 カスタムの使用許諾契約書ファイルを指定するテキストを使用して次に示す、 &lt;eula&gt;タグ。

```cpp
<dpinst>
  ...
  <language code="0x0409">
    ...
    <eula type="txt" path="Data\Eula409.txt"/>
    ...
  </language>
  ...
</dpinst>
```

## <a name="see-also"></a>関連項目


[**言語**](language-xml-element.md)

 

 






