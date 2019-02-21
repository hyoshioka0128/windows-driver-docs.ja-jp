---
title: Converter
description: Converter
ms.assetid: eadbbaf5-3fe3-484f-b3f1-3d543ddc817f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 662846dc5874f362c4a26852ffc9b411212f44b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552686"
---
# <a name="converter"></a>Converter


TCP/IP コンバーター コンストラクトでは、拡張することができます、[双方向通信](bidirectional-communication.md)MIB (SNMP 管理情報ベース) の特定のオブジェクトからデータを取得し、データを文字列値に変換するクエリを含むスキーマ変換の要素で指定されている値のペアの一覧に基づいています。 コンバーター コンス トラクターは、Tcpbidi.xsd で定義されます。

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
<td><p>(省略可能)ブール値と<strong>TRUE</strong>、関連付けられているアルゴリズムが指定した OID; で、デバイスのインデックスを含める必要がありますを意味ときにこの属性<strong>FALSE</strong>OID に末尾のゼロが追加されます。 既定値は<strong>FALSE</strong>します。 詳細については、次の表の次の注を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>drvPrinterEvent</strong></p></td>
<td><p>(省略可能)ポート モニターが、ドライバーに通知を送信するかどうかを示すブール値。 A <strong>TRUE</strong>値では、ドライバーをポート モニターが通知を送信することを示します<strong>FALSE</strong>ポート モニター ドライバーに、通知が送信しないことを示します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>name</strong></p></td>
<td><p>スキーマ要素の名前を表す文字列値。</p></td>
</tr>
<tr class="even">
<td><p><strong>Oid</strong></p></td>
<td><p>オブジェクト ID (OID) として、MIB オブジェクトのアドレスを表す文字列値。</p></td>
</tr>
<tr class="odd">
<td><p><strong>refreshInterval</strong></p></td>
<td><p>(省略可能)ポーリング間隔を秒単位の整数値。 既定値は、600 秒です。</p></td>
</tr>
<tr class="even">
<td><p><strong>useFirstIndex</strong></p></td>
<td><p>(省略可能)MIB テーブルの最初のエントリの読み取りに設定可能なブール値。 この属性は、コンバーター コンストラクトがプロパティのインスタンス内である場合にのみ使用されます。</p></td>
</tr>
</tbody>
</table>

 

**注**   SNMP プロトコルをサポートするネットワーク デバイスがプロセッサ、ネットワーク、プリンター、およびディスク記憶域などのさまざまなサブデバイスのホストを指定できます。 ネットワーク プリンターに実装されている MIB テーブルでは、デバイスのインデックスによってインデックスが作成されるエントリがあります。 (入力ビンの名) などの MIB テーブルからデータを取得するには、クエリに、デバイスのインデックス、サブデバイスを正しく識別することが必要です。 標準の TCP/IP ポート モニタでは、ポートの構成 UI から手動で構成するデバイスのインデックスをできます。 双方向の拡張機能、 **deviceIndex**属性に設定**TRUE**ポートの構成 UI から取得したデバイスの適切なインデックスを持つ OID が生成されます。 さらに、プロパティのインスタンスで、コンバーター コンストラクトが含まれている場合、 **deviceIndex**属性が不足しているかに設定**FALSE**OID になります 0 個のインデックスを末尾に追加されます。

 

変換ルーチンでは、次の MIB データ型がサポートされています。

整数

Integer32

Gauge32

Counter32

な TimeTicks

Unsigned32

Counter64

非透過

オクテット文字列

オブジェクト識別子

### <a href="" id="conversion-element"></a> 要素の変換

各コンバーター コンストラクト Bidi スキーマの値に MIB 要素から読み取られた値のマッピングを定義する 1 つまたは複数の変換の要素が含まれます。

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
<td><p>mibValue</p></td>
<td><p>(省略可能)MIB から読み取られる 1 つのデータ値を表す文字列値。</p></td>
</tr>
<tr class="even">
<td><p>bidiValue</p></td>
<td><p>(省略可能)データと一致する場合に返される bidi 値を表す文字列値、 <strong>mibValue</strong>この変換の要素の属性.</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="code-example"></a> コード例

次のコード例は、新しいプロパティを追加して双方向通信のスキーマを拡張し、コンバーターを作成します。

```cpp
<Property name="Printer">
  <Property name="Layout">
    <Property name="InputBins">
      <IndexedProperty name="Bin">
        <Converter name="BinType" oid="1.3.6.1.2.1.43.8.2.1.2" deviceIndex="true">
          <Conversion mibValue="2" bidiValue="Unknown"/>
          <Conversion mibValue="3" bidiValue="SheetFeedAutoRemoveableTray"/>
          <Conversion mibValue="4" bidiValue="SheetFeedAutoNonRemovableTray"/>
          <Conversion mibValue="5" bidiValue="SheetFeedManual"/>
          <Conversion mibValue="6" bidiValue="ContinuousRoll"/>
          <Conversion mibValue="7" bidiValue="ContinuousFanFold"/>
        </Converter>
      </IndexedProperty>
    </Property>
    <Property name="Orientation">
      <Converter name="CurrentValue" oid="1.3.6.1.2.1.43.15.1.1.7" deviceIndex="true" useFirstIndex="true">
        <Conversion mibValue="3" bidiValue="Portrait"/>
        <Conversion mibValue="4" bidiValue="Landscape"/>
     </Converter>
   </Property>
 </Property>
 <Property name="Custom">
    <Property name="HostRescourceMIB">
      <Converter name="InterfaceName" oid="1.3.6.1.2.1.2.1">
      <Conversion mibValue="1" bidiValue="InterfaceOne"/>
    <Conversion mibValue="2" bidiValue="InterfaceTwo"/>
     </Converter>
  </Property>
 </Property
</Property>
```

前の例は、次のクエリ結果します。

```cpp
\Printer.Layout.InputBins.Bin###:BinType
\Printer.Layout.Orientation:CurrentValue
\Printer.Custom.HostResourceMIB:InterfaceName
```

コンバーター コンストラクト`BinType`IndexedProperty インスタンスに含まれているし、その結果、MIB テーブル行の現在のエントリは、OID に付加は自動的にします。

コンバーターを構築するため`CurrentValue `プロパティ インスタンスに含まれていると、 **useFirstIndex**属性が"true"、末尾に設定「1」自動的に追加される OID にします。

コンバーター コンストラクト`InterfaceName`プロパティのインスタンスに含まれては OID に自動的に追加されている、末尾のゼロためです。

 

 




