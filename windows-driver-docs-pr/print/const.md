---
title: Const (TCP/IP)
description: TCP/IP Const コンストラクトは、返される必要があるデータ型と値を定義します。
ms.assetid: a0ede11d-ada4-4dc4-87a4-68c96635c0fd
keywords:
- Const コンストラクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a60a0caed5bad52519bfd44025e4c1b4e90270e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843680"
---
# <a name="const-tcpip"></a>Const (TCP/IP)


TCP/IP Const コンストラクトは、返される必要があるデータ型と値を定義します。 Const は、値が変更されない要素に使用されます。 Const コンストラクトは、Tcpbidi で定義されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>備わっている</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>name</strong></p></td>
<td><p>スキーマ値の名前です。</p></td>
</tr>
<tr class="even">
<td><p><strong>type</strong></p></td>
<td><p><strong>Value</strong>属性のデータの型。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type" data-raw-source="[&lt;strong&gt;BIDI_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type)"><strong>BIDI_TYPE</strong></a>列挙体の値。</p></td>
</tr>
<tr class="odd">
<td><p><strong>value</strong></p></td>
<td><p>定数値を格納している文字列。</p></td>
</tr>
</tbody>
</table>

 

### <a name="code-example"></a>コード例

次のコード例では、`Printer` プロパティに `Extension` プロパティを追加し、`Extension` プロパティに `Version` プロパティを追加することによって、bidi 通信スキーマを拡張します。 この例では、`Extension` に定数**値**のエントリ `Category`が含まれています。 また、`Version` には、`Major` と `Minor`の2つの定数**値**エントリがあります。

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

前の例では、次のクエリが実行されます。

```cpp
\Printer.Extension:Category
\Printer.Extension.Version:Major
\Printer.Extension.Version:Minor
```

 

 




