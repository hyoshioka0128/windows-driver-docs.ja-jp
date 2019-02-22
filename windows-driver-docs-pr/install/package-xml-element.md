---
title: パッケージの XML 要素
description: パッケージの XML 要素には、ドライバー パッケージ、INF ファイルを指定します。ドライバー パッケージの INF ファイルには、タグ パッケージの XML AttributespathThe パス要素です。
ms.assetid: c7089e58-50c7-46ec-a9bf-c8e2d2bd354a
keywords:
- パッケージの XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- package XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9e3963531b94ed23490d0897cf98b72e0137f39c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557699"
---
# <a name="package-xml-element"></a>パッケージの XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

**パッケージ**の INF ファイルを指定する XML 要素を[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)します。

**要素タグ**

```cpp
<package>
```

**XML 属性**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>パス</strong></p></td>
<td align="left"><p>ドライバー パッケージの INF ファイルへのパス。 DPInst の作業ディレクトリの相対パスです。</p></td>
</tr>
</tbody>
</table>

 

**要素情報**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>親要素</strong></p></td>
<td align="left"><p><a href="group-xml-element.md" data-raw-source="[&lt;strong&gt;group&lt;/strong&gt;](group-xml-element.md)"><strong>グループ</strong></a></p></td>
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

 

**「解説」**

次のコード例に示します、**パッケージ**DirAbc を指定する要素\\Abc.inf の INF ファイルとして、[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)します。

```cpp
<dpinst>
  ...
  <group>
    <package path="DirAbc\Abc.inf" />
  </group>
  ...
</dpinst>
```

## <a name="see-also"></a>関連項目


[**グループ**](group-xml-element.md)

 

 






