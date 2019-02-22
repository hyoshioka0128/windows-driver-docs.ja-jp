---
title: 一覧
description: 一覧
ms.assetid: 4cf1c1ea-f890-4f9d-96ea-b79790f6bc60
keywords:
- リスト構造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9504c0a185eec59f7eab3593153eec0d00b67a26
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548904"
---
# <a name="list"></a>一覧


Web Services for Devices (WSD)`List`コンストラクトが XPath フィルターのクエリで指定された値のコンマ区切りの一覧を作成する文字列型。 `List` WsdBidi.xsd でコンス トラクターが定義されています。

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
<td><p><strong>フィルター</strong></p></td>
<td><p>WSD モニターは、クエリで指定された XML ドキュメントに適用される XPath クエリ。 このトピックで後述を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>name</strong></p></td>
<td><p>スキーマの値の名前。</p></td>
</tr>
<tr class="even">
<td><p><strong>クエリ</strong></p></td>
<td><p>WSD モニターを実行するクエリの型。</p></td>
</tr>
</tbody>
</table>

 

Windows の先頭で Microsoft XML (MSXML) 2.6 で実装された、XPath 言語は、XML ファイルに要素を指定する便利な方法を提供します。 Windows SDK に、XML 開発者のガイドを参照してくださいと[XPath リファレンス](https://go.microsoft.com/fwlink/p/?linkid=33165)詳細についてはします。

`List` WsdBidi.xsd でコンス トラクターが定義されています。

### <a name="code-example"></a>コード例

次のコード例では、1 枚、たとえば「1,2,4」n-up 印刷用ページのイメージの許容数を含むコンマ区切りのリストを構成します。

```cpp
<Property name='Layout'>
  <Property name='NumberUp'>
    <Property name='PagesPerSheet'>
      <List name='Supported
        query='wprt:PrinterCapabilities'
        filter='wprt:PrinterCapabilites/wprt:JobValues/wprt:DocumentProcessing/wprt:NumberUp/wprt:NUpPagesPerSheet/wprt:AllowedValue'/>
    </Property>
  </Property>
</Property>
```

前の例は、次のクエリ結果します。

```cpp
\Printer.Layout.NumberUp.PagesPerSheet:Supported
```

 

 




