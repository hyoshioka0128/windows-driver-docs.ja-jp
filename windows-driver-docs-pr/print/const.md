---
title: Const (TCP/IP)
description: TCP/IP Const コンストラクトでは、データ型と返される必要がある値を定義します。
ms.assetid: a0ede11d-ada4-4dc4-87a4-68c96635c0fd
keywords:
- Const のコンストラクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db847ce99201eb146899bdaae9a422a0c2aada3a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379715"
---
# <a name="const-tcpip"></a>Const (TCP/IP)


TCP/IP Const コンストラクトでは、データ型と返される必要がある値を定義します。 Const 要素の値に変更されないためです。 Const のコンス トラクターは、Tcpbidi.xsd で定義されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>name</strong></p></td>
<td><p>スキーマの値の名前。</p></td>
</tr>
<tr class="even">
<td><p><strong>type</strong></p></td>
<td><p>内のデータ型、<strong>値</strong>属性の値、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winspool/ne-winspool-bidi_type" data-raw-source="[&lt;strong&gt;BIDI_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winspool/ne-winspool-bidi_type)"> <strong>BIDI_TYPE</strong> </a>列挙体。</p></td>
</tr>
<tr class="odd">
<td><p><strong>value</strong></p></td>
<td><p>定数の値を含む文字列。</p></td>
</tr>
</tbody>
</table>

 

### <a name="code-example"></a>コード例

次のコード例では、双方向通信のスキーマを拡張を追加して、`Extension`プロパティを`Printer`プロパティ、および`Version`プロパティを`Extension`プロパティ。 例では、`Extension`定数が含まれる**値**エントリ、`Category`します。 また、`Version`が 2 つの定数**値**エントリ、`Major`と`Minor`します。

```cpp
<Property name="Printer">
  <Property name="Extension">
    <Const name="Category" type="BIDI_STRING" value="Extension"/>
    <Property name="Version">
      <Const name="Major" type="BIDI_INT" value="1"/>
      <Const name="Minor" type="BIDI_INT" value="0"/>
    </Property>
  </Property>
</Property>
```

前の例は、次のクエリ結果します。

```cpp
\Printer.Extension:Category
\Printer.Extension.Version:Major
\Printer.Extension.Version:Minor
```

 

 




