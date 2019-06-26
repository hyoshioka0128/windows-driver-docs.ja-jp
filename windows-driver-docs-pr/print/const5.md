---
title: Const (WSD)
description: Devices (WSD) Const コンストラクトの Web サービスでは、データ型と返される必要がある値を定義します。
ms.assetid: e9bcf007-0117-48a9-9873-a9bbc5702e29
keywords:
- Const のコンストラクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 608c8b54be0dde51b37b1117366428f7c328d4b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374676"
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

 

 




