---
title: Const (WSD)
description: Devices (WSD) Const コンストラクトの Web サービスでは、データ型と返される必要がある値を定義します。
ms.assetid: e9bcf007-0117-48a9-9873-a9bbc5702e29
keywords:
- Const のコンストラクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a1c26fa8413e64461e7c61bf4ae068521a482e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550043"
---
# <a name="const-wsd"></a>Const (WSD)


Devices (WSD) Const コンストラクトの Web サービスでは、データ型と返される必要がある値を定義します。 Const 要素の値に変更されないためです。 Const のコンス トラクターは、WsdBidi.xsd で定義されます。

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

次のコード例では、特定の bidi スキーマ クエリの bidi 拡張ファイルで定義されている定数値を返します。

```cpp
<Property name="Printer">
  <Property name="Extension">
    <Const name="Version" type="BIDI_INT">1</Const>
  </Property>
</Property>
```

この例では、次のクエリ結果します。

```cpp
\Printer.Extension.Version:1
```

 

 




