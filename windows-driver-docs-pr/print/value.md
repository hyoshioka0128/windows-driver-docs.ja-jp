---
title: Value (WSD)
description: WSD 値構成体を使用すると、特定のスキーマ要素からデータを取得するクエリを使用して、bidi 通信スキーマを拡張できます。
ms.assetid: 8930e012-88ee-44ff-9abc-a15367f04ca3
keywords:
- 値の構成体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f93fd1e12ad8d22ec5daa8b5322c1971421f8772
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652855"
---
# <a name="value-wsd"></a>Value (WSD)


WSD `Value` コンストラクトを使用すると、Web サービスインターフェイスの特定のスキーマ要素からデータを取得するクエリを使用して、bidi 通信スキーマを拡張できます。

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
<td><p><strong>drvPrinterEvent</strong></p></td>
<td><p>Optionalポートモニターがドライバーに通知を送信するかどうかを示すブール値です。 <strong>TRUE</strong>の値は、ポートモニターがドライバーに通知を送信することを示します。<strong>FALSE</strong>は、ポートモニターがドライバーに通知を送信しないことを示します。</p></td>
</tr>
<tr class="even">
<td><p><strong>フィルター (filter)</strong></p></td>
<td><p>クエリで指定された XML ドキュメントに、WSD モニターが適用する XPath クエリ。 このトピックの後半の説明を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>name</strong></p></td>
<td><p>スキーマ値の名前です。</p></td>
</tr>
<tr class="even">
<td><p>クエリ</p></td>
<td><p>WSD モニターが実行するクエリの種類。</p></td>
</tr>
<tr class="odd">
<td><p><strong>type</strong></p></td>
<td><p>のデータの種類 <code>Value</code> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type" data-raw-source="[&lt;strong&gt;BIDI_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type)"><strong>BIDI_TYPE</strong></a>列挙体の値を構築します。</p></td>
</tr>
<tr class="even">
<td><p><strong>xmllang</strong></p></td>
<td><p>Optionalブール値。 <strong>TRUE</strong>の場合は、関連付けられている <code>Value</code> コンストラクトはローカライズ可能な文字列値として扱う必要があります。 これは、上記で定義した XPath クエリで、xml: lang 属性で区別されるノードの一覧を返すことが想定されていることを意味します。 次に、WSD モニタは、値の一覧で最適なロケール一致を検索します。 既定値は<strong>FALSE</strong>です。</p></td>
</tr>
</tbody>
</table>

 

XPath 言語は Windows に実装されており、XML ファイル内の要素を指定する便利な方法を提供します。 詳細については、Windows SDK と[XPath リファレンス](https://go.microsoft.com/fwlink/p/?linkid=33165)の XML 開発者ガイドを参照してください。

**Xmllang**属性は、`Value` コンストラクトの type 属性が "BIDI\_STRING" または "BIDI\_TEXT" の場合にのみ使用されます。

`Value` コンストラクトは、WsdBidi で定義されています。

### <a href="" id="example"></a> 「例」

次のコード例では、WSD モニターによって、RAM メモリのサイズが整数値として決定されます。

```cpp
<Schema xmlns:nprt='https://schemas.microsoft.com/windows/2005/05/wdp/print'>
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

前の例では、次のクエリが実行されます。

```cpp
\Printer.DeviceInfo:PrinterString
\Printer.Configuration.Memory:Size
```

 

 




