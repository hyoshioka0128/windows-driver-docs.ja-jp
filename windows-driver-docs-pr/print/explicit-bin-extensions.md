---
title: 明示的なビン拡張機能
description: 明示的なビン拡張機能
ms.assetid: a9f7f290-1af8-4312-b348-c1c98a3fc4a6
keywords:
- 明示的な箱拡張機能の WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eac8b3cf0390662cd5396d79bae8cc59d18ce2ca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371759"
---
# <a name="explicit-bin-extensions"></a>明示的なビン拡張機能


さらに、特別なコンストラクトを使用して暗黙的な箱の拡張機能を拡張できます**BinValue**します。 MIB オブジェクト prtInputTable または prtOutputTable テーブル内には、新しいデータが含まれています。 このオブジェクトを決定します。

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
<td><p>ビンの名前。</p></td>
</tr>
<tr class="even">
<td><p><strong>type</strong></p></td>
<td><p>列挙子、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winspool/ne-winspool-bidi_type" data-raw-source="[&lt;strong&gt;BIDI_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winspool/ne-winspool-bidi_type)"> <strong>BIDI_TYPE</strong> </a>列挙体。</p></td>
</tr>
<tr class="odd">
<td><p><strong>drvPrinterEvent</strong></p></td>
<td><p>(省略可能)ポート モニターが、ドライバーに通知を送信するかどうかを示すブール値。 A <strong>TRUE</strong>値では、ドライバーをポート モニターが通知を送信することを示します<strong>FALSE</strong>ポート モニター ドライバーに、通知が送信しないことを示します。</p></td>
</tr>
<tr class="even">
<td><p><strong>valueId</strong></p></td>
<td><p>いずれかの printmib.prtInput.prtInputTable.prtInputEntry の MIB オブジェクト。<strong>valueId</strong> (入力ビン) または printmib.prtOutput.prtOutputTable.prtOutputEntry <strong>。valueId</strong> (出力ビン)。</p></td>
</tr>
</tbody>
</table>

 

### <a name="code-example"></a>コード例

次のコード例に示す方法、 **BinValue**コンストラクトを使用して、新しいプロパティを追加すること**セキュリティ**します。 暗黙的な箱の拡張機能を拡張するための効果があります。

```cpp
<Property name="Layout">
  <Property name="InputBins">
    <InputBin name="TopBin" mibName="TRAY 1">
      <BinValue name="Security" type="BIDI_INT" valueId="19"/>
    </InputBin>
  </Property>
</Property>
```

前の例は、次のクエリ結果します。

```cpp
\Printer.Layout.InputBins.TopBin:Security
```

次のコード例に示す方法、 **BinValue**コンストラクトを使用して、状態値を追加することです。 上記の例のように、暗黙的な箱の拡張機能を拡張するための効果があります。

```cpp
<Property name="Finishing">
  <Property name="OutputBins">
    <OutputBin name="TopBin" mibName="STANDARD BIN">
       <BinValue name="Status" type="BIDI_INT" valueId="6"/>
    </OutputBin>
  </Property>
</Property>
```

前の例は、次のクエリ結果します。

```cpp
\Printer.Finishing.OutputBins.TopBin:Status
```

 

 




