---
title: package XML 要素
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
ms.openlocfilehash: 215cc82ab29f8dfce9c397a37d052fedb820c112
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384249"
---
# <a name="package-xml-element"></a>package XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)します。\]

**パッケージ**の INF ファイルを指定する XML 要素を[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)します。

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

 

**注釈**

次のコード例に示します、**パッケージ**DirAbc を指定する要素\\Abc.inf の INF ファイルとして、[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)します。

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

 

 






