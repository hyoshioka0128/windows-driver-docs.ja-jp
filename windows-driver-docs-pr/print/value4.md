---
title: Value (TCP/IP)
description: TCP/IP 値コンス トラクターを使用すると、特定の MIB オブジェクトからデータを取得するクエリで双方向通信スキーマを拡張できます。
ms.assetid: 46b24830-10a1-405b-9c12-b5804f76d668
keywords:
- 値の構造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b81a0fddfe1a0edcf158f6d73a5770f1a7d8894e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354899"
---
# <a name="value-tcpip"></a>Value (TCP/IP)


TCP/IP`Value`コンストラクトでは、MIB の特定のオブジェクトからデータを取得するクエリで双方向通信のスキーマを拡張できます。 `Value` Tcpbidi.xsd でコンス トラクターが定義されています。

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
<td><p><strong>deviceIndex</strong></p></td>
<td><p>フラグを設定するには、A と<strong>TRUE</strong>は、関連付けられているアルゴリズムが指定した OID; で、デバイスのインデックスを含める必要がありますと<strong>FALSE</strong>OID に末尾のゼロが追加されます。 既定値は<strong>FALSE</strong>します。 詳細については、次の表の次の注を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>drvPrinterEvent</strong></p></td>
<td><p>(省略可能)ポート モニターが、ドライバーに通知を送信するかどうかを示すブール値。 A <strong>TRUE</strong>値では、ドライバーをポート モニターが通知を送信することを示します<strong>FALSE</strong>ポート モニター ドライバーに、通知が送信しないことを示します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>name</strong></p></td>
<td><p>スキーマの値の名前。</p></td>
</tr>
<tr class="even">
<td><p><strong>Oid</strong></p></td>
<td><p>オブジェクト ID (OID) として、MIB オブジェクトのアドレス。</p></td>
</tr>
<tr class="odd">
<td><p><strong>refreshInterval</strong></p></td>
<td><p>(省略可能)ポーリング間隔を秒単位の値。 既定値は、600 秒です。</p></td>
</tr>
<tr class="even">
<td><p><strong>type</strong></p></td>
<td><p>内のデータ型、<code> Value</code>で値を構成、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winspool/ne-winspool-bidi_type" data-raw-source="[&lt;strong&gt;BIDI_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winspool/ne-winspool-bidi_type)"> <strong>BIDI_TYPE</strong> </a>列挙体。</p></td>
</tr>
</tbody>
</table>

 

**注**  SNMP プロトコルをサポートするネットワーク デバイスがプロセッサ、ネットワーク、プリンター、およびディスク記憶域などのさまざまなサブデバイスのホストを指定できます。 ネットワーク プリンターで実装された MIB テーブルでは、デバイスのインデックスによってインデックスが作成されるエントリがあります。 (入力ビンの名) などの MIB テーブルからデータを取得するには、クエリは、サブデバイスを正しく識別するデバイスのインデックスが必要です。 標準の TCP/IP ポート モニタでは、ポートの構成 UI から手動で構成するデバイスのインデックスをできます。 Bidi 拡張子**deviceIndex**="true"に、ポートの構成 UI から取得した適切なデバイスのインデックスを持つ OID が生成されます。 さらに場合、`Value`コンストラクトがプロパティのインスタンスに含まれている、OID がゼロのインデックスを末尾に追加されます。

 

### <a href="" id="code-example"></a> コード例

次のコード例は、新しいプロパティを追加することによって双方向通信のスキーマを拡張**システム**を**プリンター**プロパティ。 **システム**プロパティは、`Value`構築で**名前**、**型**、および**oid**属性。

```cpp
<Property name="Printer">
  <Property name="System">
    <Value name="Name" type="BIDI_STRING" oid="1.3.6.1.2.1.1.5"/>
  </Property>
</Property>
```

前の例は、次のクエリ結果します。

```cpp
\Printer.System:Name
```

ため、`Value`コンストラクトが IndexedProperty インスタンスではなく、プロパティのインスタンスに含まれている、末尾のゼロは OID に自動的に追加されます。

 

 




