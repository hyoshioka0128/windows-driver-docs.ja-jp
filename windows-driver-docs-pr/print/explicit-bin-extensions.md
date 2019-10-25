---
title: 明示的なビン拡張機能
description: 明示的なビン拡張機能
ms.assetid: a9f7f290-1af8-4312-b348-c1c98a3fc4a6
keywords:
- 明示的なビン拡張の WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 780b1885393e758c31af70b018e649a09a5ffdbc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843123"
---
# <a name="explicit-bin-extensions"></a>明示的なビン拡張機能


特別なコンストラクトである**Binvalue**を使用して、暗黙的なビン拡張をさらに拡張できます。 このオブジェクトは、新しいデータを含む、PrprtOutputTable Puttable またはテーブル内の MIB オブジェクトを決定します。

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
<td><p>ビンの名前。</p></td>
</tr>
<tr class="even">
<td><p><strong>type</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type" data-raw-source="[&lt;strong&gt;BIDI_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type)"><strong>BIDI_TYPE</strong></a>列挙内の列挙子。</p></td>
</tr>
<tr class="odd">
<td><p><strong>drvPrinterEvent</strong></p></td>
<td><p>Optionalポートモニターがドライバーに通知を送信するかどうかを示すブール値です。 <strong>TRUE</strong>の値は、ポートモニターがドライバーに通知を送信することを示します。<strong>FALSE</strong>は、ポートモニターがドライバーに通知を送信しないことを示します。</p></td>
</tr>
<tr class="even">
<td><p><strong>valueId</strong></p></td>
<td><p>PrtInput のいずれかの MIB オブジェクトを入力します (printf)。<strong>Valueid</strong> (入力ビン) または PrtOutput. PrtOutputTable. prtOutputEntry.<strong>Valueid</strong> (出力ビン)。</p></td>
</tr>
</tbody>
</table>

 

### <a name="code-example"></a>コード例

次のコード例では、 **Binvalue**コンストラクトを使用して、新しいプロパティである**Security**を追加する方法を示します。 これにより、暗黙的な bin 拡張が拡張されます。

```cpp
<Property name="Layout">
  <Property name="InputBins">
    <InputBin name="TopBin" mibName="TRAY 1">
      <BinValue name="Security" type="BIDI_INT" valueId="19"/>
    </InputBin>
  </Property>
</Property>
```

前の例では、次のクエリが実行されます。

```cpp
\Printer.Layout.InputBins.TopBin:Security
```

次のコード例は、 **binvalue**コンストラクトを使用して状態値を追加する方法を示しています。 前の例と同様に、これは暗黙的なビン拡張を拡張する効果を持ちます。

```cpp
<Property name="Finishing">
  <Property name="OutputBins">
    <OutputBin name="TopBin" mibName="STANDARD BIN">
       <BinValue name="Status" type="BIDI_INT" valueId="6"/>
    </OutputBin>
  </Property>
</Property>
```

前の例では、次のクエリが実行されます。

```cpp
\Printer.Finishing.OutputBins.TopBin:Status
```

 

 




