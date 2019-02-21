---
title: Const (TCP/IP)
description: TCP/IP Const コンストラクトでは、データ型と返される必要がある値を定義します。
ms.assetid: a0ede11d-ada4-4dc4-87a4-68c96635c0fd
keywords:
- Const のコンストラクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b11d920fea90128b47768c9b4cd6450ea77b3089
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535610"
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
<td><p><strong>型</strong></p></td>
<td><p>内のデータ型、<strong>値</strong>属性の値、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff545211" data-raw-source="[&lt;strong&gt;BIDI_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545211)"> <strong>BIDI_TYPE</strong> </a>列挙体。</p></td>
</tr>
<tr class="odd">
<td><p><strong>値</strong></p></td>
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

 

 




