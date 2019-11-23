---
title: Value (TCP/IP)
description: TCP/IP 値の構成体を使用すると、特定の MIB オブジェクトからデータを取得するクエリを使用して、bidi 通信スキーマを拡張できます。
ms.assetid: 46b24830-10a1-405b-9c12-b5804f76d668
keywords:
- 値の構成体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b21c9ac36ddbb26590bea0d3f194e2a0fc6d72b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840397"
---
# <a name="value-tcpip"></a>Value (TCP/IP)


TCP/IP `Value` コンストラクトを使用すると、特定の MIB オブジェクトからデータを取得するクエリを使用して、bidi 通信スキーマを拡張できます。 `Value` コンストラクトは、Tcpbidi で定義されています。

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
<td><p><strong>TRUE</strong>の場合は、関連付けられたアルゴリズムに、指定した OID にデバイスインデックスを含める必要があることを意味するフラグ。<strong>FALSE</strong>の場合、末尾のゼロが OID に追加されます。 既定値は<strong>FALSE</strong>です。 詳細については、この表の後の注を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>drvPrinterEvent</strong></p></td>
<td><p>Optionalポートモニターがドライバーに通知を送信するかどうかを示すブール値です。 <strong>TRUE</strong>の値は、ポートモニターがドライバーに通知を送信することを示します。<strong>FALSE</strong>は、ポートモニターがドライバーに通知を送信しないことを示します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>name</strong></p></td>
<td><p>スキーマ値の名前です。</p></td>
</tr>
<tr class="even">
<td><p><strong>ドーナツ</strong></p></td>
<td><p>オブジェクト ID (OID) としての MIB オブジェクトのアドレス。</p></td>
</tr>
<tr class="odd">
<td><p><strong>refreshInterval</strong></p></td>
<td><p>Optionalポーリング間隔の値 (秒単位)。 既定値は、600 秒です。</p></td>
</tr>
<tr class="even">
<td><p><strong>type</strong></p></td>
<td><p><code> Value</code> コンストラクト内のデータの型。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type" data-raw-source="[&lt;strong&gt;BIDI_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type)"><strong>BIDI_TYPE</strong></a>列挙体の値。</p></td>
</tr>
</tbody>
</table>

 

**注:** SNMP プロトコルをサポートするネットワークデバイスは、プロセッサ、ネットワーク、プリンター、Disk Storage など、さまざまなサブデバイスのホストになることが  ます。 ネットワークプリンターに実装される MIB テーブルには、デバイスインデックスによってインデックスが付けられたエントリがあります。 MIB テーブル (入力ビンの名前など) からデータを取得するには、サブデバイスを正しく識別するデバイスインデックスがクエリに必要です。 標準 TCP/IP ポートモニターでは、デバイスインデックスをポート構成 UI で手動で構成することができます。 **Deviceindex**= "true" の bidi 拡張機能では、ポート構成 UI から取得した適切なデバイスインデックスを使用して OID が生成されます。 また、`Value` コンストラクトがプロパティインスタンスに含まれている場合、OID の末尾にはゼロのインデックスが追加されます。

 

### <a href="" id="code-example"></a>コード例

次のコード例では、 **Printer**プロパティに新しいプロパティ**システム**を追加することによって、bidi 通信スキーマを拡張します。 **システム**プロパティには、**名前**、**型**、および**oid**属性を持つ `Value` コンストラクトがあります。

```cpp
<Property name="Printer">
  <Property name="System">
    <Value name="Name" type="BIDI_STRING" oid="1.3.6.1.2.1.1.5"/>
  </Property>
</Property>
```

前の例では、次のクエリが実行されます。

```cpp
\Printer.System:Name
```

`Value` コンストラクトは IndexedProperty インスタンスではなくプロパティインスタンスに含まれているため、末尾のゼロが自動的に OID に追加されることに注意してください。

 

 




