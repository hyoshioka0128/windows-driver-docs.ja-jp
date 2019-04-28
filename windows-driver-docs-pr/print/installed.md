---
title: Installed (WSD)
description: Devices (WSD) のインストール済みのコンストラクトの Web サービスでは、指定された一連の条件に一致するプリンターの機能がインストールされているかどうかを示します。
ms.assetid: f05add2a-d37e-4eb5-8408-dd5eeef4b13c
keywords:
- インストールされているコンス トラクター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7940468d4083e31ffaee5c7dfd1ff6fa60a8dd6c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362760"
---
# <a name="installed-wsd"></a>Installed (WSD)


Devices (WSD) のインストール済みのコンストラクトの Web サービスでは、指定された一連の条件に一致するプリンターの機能がインストールされているかどうかを示します。 このアルゴリズムを返しますのかどうか、XPath フィルターは、指定された条件に適用する場合は、有効な XML 結果を取得する**TRUE**します。 インストールされているコンス トラクターは、WsdBidi.xsd で定義されます。

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
<td><p>WSD モニターは、クエリで指定された XML ドキュメントに適用される XPath クエリ。 このトピックで後述を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>name</strong></p></td>
<td><p>スキーマの値の名前。</p></td>
</tr>
<tr class="even">
<td><p><strong>query</strong></p></td>
<td><p>WSD モニターを実行するクエリの型。</p></td>
</tr>
</tbody>
</table>

 

Windows の先頭で Microsoft XML (MSXML) 2.6 で実装された、XPath 言語は、XML ファイルに要素を指定する便利な方法を提供します。 Windows SDK に、XML 開発者のガイドを参照してくださいと[XPath リファレンス](https://go.microsoft.com/fwlink/p/?linkid=33165)詳細についてはします。

インストール済みのコンス トラクターの動作は、その親ノードの定義に依存します。 パラメーターを使用せず、インストール済みのコンストラクトを指定すると照会されたときに、スキーマは常に存在します。 パラメーターを使用して、インストールされているコンストラクトが指定されている場合、スキーマは WSD デバイスの現在のクエリで関連するパラメーター値が見つかった場合にのみ存在します。 クエリを行っているソフトウェアは、インストール済みのスキーマが返されていないケースを処理できる必要があります。

インストールされているコンス トラクターは、WsdBidi.xsd で定義されます。

### <a name="code-example"></a>コード例

次のコード例では、フィルター検索アルゴリズムは、ハード_ディスクがインストールされていることを確認するのに XPath クエリを使用します。

```cpp
<Schema>
  <Property name='Printer'>
    <Property name='Configuration'>
      <Property name='HardDisk'>
        <Installed name='Installed'
            query='wprt:PrinterConfiguration'
            filter='wprt:PrinterConfiguration/wprt:Storage/wprt:StorageEntry[wprt:Type="HardDisk"]'/>
      </Property>
    </Property>
  </Property>
</Schema>
```

前の例は、次のクエリ結果します。

```cpp
\Printer.Configuration.HardDisk:Installed
```

 

 




