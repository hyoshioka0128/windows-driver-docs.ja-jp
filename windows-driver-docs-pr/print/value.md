---
title: Value (WSD)
description: WSD 値コンス トラクターを使用すると、特定のスキーマ要素からデータを取得するクエリで双方向通信のスキーマを拡張できます。
ms.assetid: 8930e012-88ee-44ff-9abc-a15367f04ca3
keywords:
- 値の構造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c8724d2049a7417c7b02fb80124012840b48de8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384513"
---
# <a name="value-wsd"></a>Value (WSD)


WSD`Value`コンストラクトでは、Web サービス インターフェイス内の特定のスキーマ要素からデータを取得するクエリで双方向通信のスキーマを拡張できます。

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
<td><p><strong>drvPrinterEvent</strong></p></td>
<td><p>(省略可能)ポート モニターが、ドライバーに通知を送信するかどうかを示すブール値。 A <strong>TRUE</strong>値では、ドライバーをポート モニターが通知を送信することを示します<strong>FALSE</strong>ポート モニター ドライバーに、通知が送信しないことを示します。</p></td>
</tr>
<tr class="even">
<td><p><strong>フィルター (filter)</strong></p></td>
<td><p>WSD モニターがクエリで指定された XML ドキュメントに適用される XPath クエリ。 このトピックで後述を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>name</strong></p></td>
<td><p>スキーマの値の名前。</p></td>
</tr>
<tr class="even">
<td><p>query</p></td>
<td><p>WSD モニターを実行するクエリの型。</p></td>
</tr>
<tr class="odd">
<td><p><strong>type</strong></p></td>
<td><p>内のデータ型、 <code>Value</code> 値を構築、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winspool/ne-winspool-bidi_type" data-raw-source="[&lt;strong&gt;BIDI_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winspool/ne-winspool-bidi_type)"> <strong>BIDI_TYPE</strong> </a>列挙体。</p></td>
</tr>
<tr class="even">
<td><p><strong>xmllang</strong></p></td>
<td><p>(省略可能)ブール値と<strong>TRUE</strong>、関連付けられていることを意味します。 <code>Value</code> コンス トラクターは、ローカライズ可能な文字列値として扱う必要があります。 つまり、上記で定義された XPath クエリは、xml:lang 属性で差別化されたノードの一覧を返すと想定されます。 WSD モニターに最も一致するロケールの値の一覧が検索されます。 既定値は<strong>FALSE</strong>します。</p></td>
</tr>
</tbody>
</table>

 

XPath 言語は、Windows では実装され、XML ファイルに要素を指定する便利な方法を提供します。 Windows SDK に、XML 開発者のガイドを参照してくださいと[XPath リファレンス](https://go.microsoft.com/fwlink/p/?linkid=33165)詳細についてはします。

**Xmllang**属性が使用される場合にのみの型の属性、`Value`コンス トラクターがあるか、"BIDI\_文字列"または"BIDI\_テキスト"。

`Value` WsdBidi.xsd でコンス トラクターが定義されています。

### <a href="" id="example"></a> 例

次のコード例では、WSD モニターは、RAM メモリの整数値として、サイズを決定します。

```cpp
<Schema xmlns:nprt='http://schemas.microsoft.com/windows/2005/05/wdp/print'>
  <Property name='Printer'>
    <Property name='DeviceInfo'>
      <Value name='PrinterString' 
 query='nprt:PrinterDescription'
 filter='nprt:PrinterDescription/nprt:PrinterName' 
 type='BIDI_STRING' 
 xmllang='true'/>
    </Property>
    <Property name='Configuration'>
      <Property name='Memory'>
        <Value name='Size'
          query='wprt:PrinterConfiguration'
          filter='wprt:PrinterConfiguration/wprt:Storage/wprt:StorageEntry[wprt:Type="RAM"]/wprt:Size'
          type='BIDI_INT'/>
      </Property>
    </Property>
   </Property>
</Schema>
```

前の例は、次のクエリ結果します。

```cpp
\Printer.DeviceInfo:PrinterString
\Printer.Configuration.Memory:Size
```

 

 




