---
title: Const (WSD)
description: Web Services for Devices (WSD) Const コンストラクトでは、返される必要があるデータ型と値が定義されています。
ms.assetid: e9bcf007-0117-48a9-9873-a9bbc5702e29
keywords:
- Const コンストラクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc318ab074a0f1d0fd3cb733539be011f85a9742
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831860"
---
# <a name="const-wsd"></a>Const (WSD)


Web Services for Devices (WSD) Const コンストラクトでは、返される必要があるデータ型と値が定義されています。 Const は、値が変更されない要素に使用されます。 Const コンストラクトは WsdBidi で定義されています。

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

次のコード例では、特定の bidi スキーマクエリの bidi 拡張ファイルで定義されている定数値を返します。

```cpp
<Property name="Printer">
  <Property name="Extension">
    <Const name="Version" type="BIDI_INT">1</Const>
  </Property>
</Property>
```

この例では、次のクエリが実行されます。

```cpp
\Printer.Extension.Version:1
```

 

 




