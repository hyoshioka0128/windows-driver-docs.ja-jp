---
title: 素材のキーワード
description: これらのキーワードでは、3 D オブジェクトの作成に使用するデバイスに原材料について説明します。
ms.assetid: B2264CA8-64F9-4A20-AC55-46A0C48EDF3C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74f88783c5db8e98e14689876652c7349bc24d53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551881"
---
# <a name="material-keywords"></a>素材のキーワード


これらのキーワードでは、3 D オブジェクトの作成に使用するデバイスに原材料について説明します。

## <a name="31-job3dmaterialcount"></a>3.1. Job3DMaterialCount


このパラメーターは、資料の 1 つのジョブで使用できるデバイスに現在読み込まれての数を定義する必要があります。 デバイスに素材が読み込まれるときに知らない場合このパラメーターは、1 つのジョブに使われる材料の数である必要があります。 プリンターにのみ、1 つの不明な資料がある場合は、その他のすべての素材キーワードと共に、このパラメーターは省略できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td>psk3d:Job3DMaterialCount</td>
</tr>
<tr class="even">
<td>に対して有効です。</td>
<td>PrintCapabilities ドキュメント</td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>プロパティ</td>
</tr>
<tr class="even">
<td>目次</td>
<td><p>1 つのみを含む&lt;値&gt;次のように、子要素。</p>
<p><strong>子:</strong>Value</p>
<p><strong>xsi:type:</strong> xsd:integer</p>
<p><strong>値:</strong>JobMaterialCountText</p>
<p><strong>説明 :</strong>JobMaterialCountText、このプロパティが指定されている場合がこのデバイスで利用できる資料の数を指定する正の整数を含める必要があります。</p></td>
</tr>
</tbody>
</table>



Job3DMaterialCount キーワードの使用状況

```cpp
<psf:Property name="psk3d:Job3DMaterialCount">
    <psf:Value xsi:type="xsd:integer">2</psf:Value>
</psf:Property>
```

## <a name="32-job3dmaterials"></a>3.2. Job3DMaterials


このプロパティは、デバイスに読み込まれた資料の説明を含んでいる必要があります。 またはこれが、不明の場合は、マテリアルを読み込むことが可能な場所の列挙体を含める必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td>psk3d:Job3DMaterials</td>
</tr>
<tr class="even">
<td>に対して有効です。</td>
<td>PrintCapabilities ドキュメント</td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>プロパティ</td>
</tr>
<tr class="even">
<td>目次</td>
<td><p>次のように、1 つ以上の子プロパティ要素が含まれます。</p>
<p><strong>子:</strong>プロパティの一覧</p>
<p><strong>xsi:type:</strong>なし</p>
<p><strong>値:</strong>MaterialsList</p>
<p><strong>説明 :</strong>MaterialsList には、一連子プロパティにはが含まれています。</p></td>
</tr>
</tbody>
</table>



### <a name="321-materialslist-properties"></a>3.2.1. MaterialsList プロパティ

ベンダーは、自分のデバイスに読み込まれた印刷物を列挙する、独自の素材を作成する必要があります。 これらの資料の名前を使用して、ベンダー定義は、デバイスが読み込まれた素材カートリッジからこのような情報を読み取ることができる場合は、株価の説明を表す必要があります。 デバイスがこの情報を所有していない場合、ベンダーする必要があります (たとえば、"左 Extruder") このマテリアルが読み込まれる場所のわかりやすいとして数量単価型の名前を定義します。

各資料は、次の子プロパティを指定します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>数量単価型の名前</th>
<th>xsi:type</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>psk:DisplayName</td>
<td>xsd:string</td>
<td>このプロパティは、ローカライズされた表示名を含む psf:Value 要素を含める必要があります。</td>
</tr>
<tr class="even">
<td>psk3d:MaterialColor</td>
<td>xsd:string</td>
<td><p>デバイスは、マテリアルの色を指定するには、このプロパティを定義できます。 指定する場合は、以下の説明に準拠している、sRGB 色である必要があります、値。</p>
<div class="code">
<code>cpp
sRGBColorText = &quot;#&quot; hR hG hB hA
hR = hG = hB = hA = hexpair
hexpair = hexdigit hexdigit
hexdigit = &quot;0&quot; / &quot;1&quot; / &quot;2&quot; / &quot;3&quot; /
           &quot;4&quot; / &quot;5&quot; / &quot;6&quot; / &quot;7&quot; /
           &quot;8&quot; / &quot;9&quot; / &quot;A&quot; / &quot;B&quot; /
           &quot;C&quot; / &quot;D&quot; / &quot;E&quot; / &quot;F&quot; /
           &quot;a&quot; / &quot;b&quot; / &quot;c&quot; / &quot;d&quot; /
           &quot;e&quot; / &quot;f&quot;</code>
</div>
<p>人事、hG、hB、hA、赤、緑、青、およびアルファのコンポーネントの 16 進数の 1 バイト値をそれぞれ指定、00 ~ FF 範囲とします。 デバイスは、FF の既定値 (完全に不透明) にどの大文字と小文字のアルファのアルファ (つまり #hRhGhB) を省略することもできます。</p></td>
</tr>
</tbody>
</table>



Job3DMaterials キーワードの使用状況

```cpp
<psf:Property name="psk3d:Job3DMaterials">
    <psf:Property name="vnd:ABS_RED">
        <psf:Property name="psk:DisplayName">
            <psf:Value xsi:type="xsd:string">Red ABS Plastic</psf:Value>
        </psf:Property>
        <psf:Property name="psk3d:MaterialColor">
            <psf:Value xsi:type="xsd:string">#FF0000</psf:Value>
        </psf:Property>
    </psf:Property>
    <psf:Property name="vnd:PLA_TEAL">
        <psf:Property name="psk:DisplayName">
            <psf:Value xsi:type="xsd:string">Teal PLA Plastic</psf:Value>
        </psf:Property>
        <psf:Property name="psk3d:MaterialColor">
            <psf:Value xsi:type="xsd:string">#00FFFF</psf:Value>
        </psf:Property>
    </psf:Property>
</psf:Property>
```

## <a name="33-job3dsupports"></a>3.3. Job3DSupports


Psk3d:Job3DSupports キーワードは、このジョブを含めるかどうかを指定します*サポート*デバイスまたはドライバーによって生成されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td>psk3d:Job3DSupports</td>
</tr>
<tr class="even">
<td>に対して有効です。</td>
<td><p>PrintCapabilities ドキュメント</p>
<p>PrintTicket ドキュメント</p></td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>機能</td>
</tr>
<tr class="even">
<td>SelectionType</td>
<td>psk:PickOne</td>
</tr>
<tr class="odd">
<td>目次</td>
<td><p>3D の製造業のため印刷スキーマ キーワードで定義されているオプションは次のとおりです。</p>
<p><strong>子:</strong>オプション psk3d:SupportsIncluded</p>
<p><strong>説明 :</strong>このオプションは、デバイスが、モデルの外部のサポートを生成する必要がありますを指定します。</p>
<p><strong>子:</strong>オプション psk3d:SupportsExcluded</p>
<p><strong>説明 :</strong>このオプションは、デバイスが、モデルの外部のサポートを生成しないことを指定します。</p></td>
</tr>
</tbody>
</table>



Job3DSupports キーワードの使用状況

```cpp
<psf:Feature name="psk3d:Job3DSupports">
    <psf:Property name="SelectionType">
        <psf:Value xsi:type="xsd:QName">psk:PickOne</psf:Value>
    </psf:Property>
    <psf:Option name="psk3d:SupportsIncluded" />
    <psf:Option name="psk3d:SupportsExcluded" />
</psf:Feature>
```

### <a name="331-job3dsupportsmaterial"></a>3.3.1. Job3DSupportsMaterial

オプション psk3d:SupportsIncluded を選択すると、デバイスが 1 つ以上の素材をサポートして、このパラメーターには、サポート構造体に使用する主な材料が示されます。 このパラメーターは、名前付きの子 psk3d:Job3DMaterials プロパティのプロパティへの参照として解釈する必要があります。

Job3DSupportsMaterial キーワード プロファイル

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td>psk3d:Job3DSupportsMaterial</td>
</tr>
<tr class="even">
<td>に対して有効です。</td>
<td>PrintCapabilities ドキュメント</td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>ParameterDef</td>
</tr>
<tr class="even">
<td>目次</td>
<td><p>§2.1.3.1、」の説明に従って、psk3d:Job3DSupportsMaterial は、の QNameParamType &quot; &lt;psf:ParameterDef&gt; &quot;印刷スキーマ仕様で。</p>
<p><strong>子:</strong>QNameParamType</p>
<p><strong>説明 :</strong></p>
<p>プロパティ値が必要があります psf:MinLength 整数 1 以上であります。</p>
<p>Psf:MaxLength プロパティの値は、ベンダーによって定義することがあり、psf:MinLength プロパティの値以上にする必要があります。 1024 になります。</p>
<p>プロパティ値が必要があります psf:Mandatory する psk: 省略可能です。</p>
<p>プロパティ値が必要があります psf:UnitType 文字にします。</p></td>
</tr>
</tbody>
</table>



Job3DSupportsMaterial 初期化プロファイル

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td>psk3d:Job3DSupportsMaterial</td>
</tr>
<tr class="even">
<td>に対して有効です。</td>
<td>PrintTicket ドキュメント</td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>ParameterInit</td>
</tr>
<tr class="even">
<td>目次</td>
<td><p>1 つのみを含む&lt;値&gt;次のように、子要素。</p>
<p><strong>子:</strong>Value</p>
<p><strong>xsi:type:</strong> xsd:QName</p>
<p><strong>値:</strong>MaterialName</p>
<p><strong>説明 :</strong>Psk3D:Job3DMaterials プロパティの子として識別された資料を参照 MaterialName 必要があります。</p></td>
</tr>
</tbody>
</table>



Job3DSupportsMaterial キーワードの使用状況

パラメーターの定義は次のとおりです。

```cpp
<psf:ParameterDef name="psk3d:Job3DSupportsMaterial">
    <psf:Property name="psf:DataType">
        <psf:Value xsi:type="xsd:QName">xsd:QName</psf:Value>
    </psf:Property>
    <psf:Property name="psf:DefaultValue">
        <psf:Value xsi:type="xsd:QName">vnd:ABS_RED</psf:Value>
    </psf:Property>
    <psf:Property name="psf:MaxLength">
        <psf:Value xsi:type="xsd:integer">1024</psf:Value>
    </psf:Property>
    <psf:Property name="psf:MinLength">
        <psf:Value xsi:type="xsd:integer">1</psf:Value>
    </psf:Property>
    <psf:Property name="psf:Mandatory">
        <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
    </psf:Property>
    <psf:Property name="psf:UnitType">
        <psf:Value xsi:type="xsd:string">characters</psf:Value>
    </psf:Property>
</psf:ParameterDef>
```

このパラメーターは、次のように初期化されます。

```cpp
<psf:ParameterInit name="psk3d:Job3DSupportsMaterial">
    <psf:Value xsi:type="xsd:QName">vnd:PLA_TEAL</psf:Value>
</psf:ParameterInit>
```

## <a name="34-job3draft"></a>3.4. Job3DRaft


Psk3d:Job3DRaft キーワードは、このジョブを含めるかどうかを指定します、*ラフト*デバイスまたはドライバーによって生成されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td>psk3d:Job3DRaft</td>
</tr>
<tr class="even">
<td>に対して有効です。</td>
<td><p>PrintCapabilities ドキュメント</p>
<p>PrintTicket ドキュメント</p></td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>機能</td>
</tr>
<tr class="even">
<td>SelectionType</td>
<td>psk:PickOne</td>
</tr>
<tr class="odd">
<td>目次</td>
<td><p>3D の製造業のため印刷スキーマ キーワードで定義されているオプションは次のとおりです。</p>
<p><strong>子:</strong>オプション psk3d:RaftIncluded</p>
<p><strong>説明 :</strong>このオプションは、デバイスが、モデルにまつわるを生成する必要がありますを指定します。</p>
<p><strong>子:</strong>オプション psk3d:RaftExcluded</p>
<p><strong>説明 :</strong>このオプションは、デバイスが、モデルにまつわるを生成しないことを指定します。</p></td>
</tr>
</tbody>
</table>



Job3DRaft キーワードの使用状況

```cpp
<psf:Feature name="psk3d:Job3DRaft">
    <psf:Property name="SelectionType">
        <psf:Value xsi:type="xsd:QName">psk:PickOne</psf:Value>
    </psf:Property>
    <psf:Option name="psk3d:RaftIncluded" />
    <psf:Option name="psk3d:RaftExcluded" />
</psf:Feature>
```

### <a name="341-job3draftmaterial"></a>3.4.1. Job3DRaftMaterial

オプション psk3d:RaftIncluded を選択すると、デバイスが 1 つ以上の素材をサポートして、このパラメーターには、ラフトに使用する主な材料が示されます。 このパラメーターは、名前付きの子 psk3d:Job3DMaterials プロパティのプロパティへの参照として解釈する必要があります。

Job3DRaftMaterial キーワード プロファイル

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td>psk3d:Job3DRaftMaterial</td>
</tr>
<tr class="even">
<td>に対して有効です。</td>
<td>PrintCapabilities ドキュメント</td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>ParameterDef</td>
</tr>
<tr class="even">
<td>目次</td>
<td><p>§2.1.3.1、」の説明に従って、psk3d:Job3DRaftMaterial は、の QNameParamType &quot; &lt;psf:ParameterDef&gt; &quot;印刷スキーマ仕様で。</p>
<p><strong>子:</strong>QNameParamType</p>
<p><strong>説明 :</strong></p>
<p>プロパティ値が必要があります psf:MinLength 整数 1 以上であります。</p>
<p>Psf:MaxLength プロパティの値は、ベンダーによって定義することがあり、psf:MinLength プロパティの値以上にする必要があります。 1024 になります。</p>
<p>プロパティ値が必要があります psf:Mandatory する psk: 省略可能です。</p>
<p>プロパティ値が必要があります psf:UnitType 文字にします。</p></td>
</tr>
</tbody>
</table>



Job3DRaftMaterial 初期化プロファイル

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td>psk3d:Job3DRaftMaterial</td>
</tr>
<tr class="even">
<td>に対して有効です。</td>
<td>PrintTicket ドキュメント</td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>ParameterInit</td>
</tr>
<tr class="even">
<td>目次</td>
<td><p>1 つのみを含む&lt;値&gt;次のように、子要素。</p>
<p><strong>子:</strong>Value</p>
<p><strong>xsi:type:</strong> xsd:QName</p>
<p><strong>値:</strong>MaterialName</p>
<p><strong>説明 :</strong>Psk3D:Job3DMaterials プロパティの子として識別された資料を参照 MaterialName 必要があります。</p></td>
</tr>
</tbody>
</table>



Job3DRaftMaterial キーワードの使用状況

パラメーターの定義は次のとおりです。

```cpp
<psf:ParameterDef name="psk3d:Job3DRaftMaterial">
    <psf:Property name="psf:DataType">
        <psf:Value xsi:type="xsd:QName">xsd:QName</psf:Value>
    </psf:Property>
    <psf:Property name="psf:DefaultValue">
        <psf:Value xsi:type="xsd:QName">vnd:ABS_RED</psf:Value>
    </psf:Property>
    <psf:Property name="psf:MaxLength">
        <psf:Value xsi:type="xsd:integer">1024</psf:Value>
    </psf:Property>
    <psf:Property name="psf:MinLength">
        <psf:Value xsi:type="xsd:integer">1</psf:Value>
    </psf:Property>
    <psf:Property name="psf:Mandatory">
        <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
    </psf:Property>
    <psf:Property name="psf:UnitType">
        <psf:Value xsi:type="xsd:string">characters</psf:Value>
    </psf:Property>
</psf:ParameterDef>
```

このパラメーターは、次のように初期化されます。

```cpp
<psf:ParameterInit name="psk3d:Job3DRaftMaterial">
    <psf:Value xsi:type="xsd:QName">vnd:PLA_TEAL</psf:Value>
</psf:ParameterInit>
```

## <a name="35-material-mapping-parameter"></a>3.5. マッピングの素材パラメーター


デバイスは、1 つ以上の素材をサポートする場合、このパラメーターは basematerials (ID:index) 特定の出力のマテリアルにマップするペイロード ファイルからの一覧を示す必要があります。 他の素材の種類をマッピングすることはできません、ペイロード ファイルで basematerials 要素を参照して、Id 必要があります。 (Job3DMaterialSelected によって指定された) 出力マテリアルは psk3d:Job3DMaterials プロパティの子である必要があります。 マテリアルのマッピング パラメーターありますの名前は、"Job3D"で始まるし、"Map"の末尾に追加すると、psk3d:Job3DMaterialSelected プロパティの値を追加しました。 この方法では、同じの資料では、する可能性が他のプリンターへの移植性が異なる順序で読み込まれたジョブの許可、印刷機能を必要としない全体の素材のマップの印刷チケットを解析できます。

素材のパラメーターのマップ キーワード プロファイル

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td><em>仕入先の指定</em></td>
</tr>
<tr class="even">
<td>に対して有効です。</td>
<td>PrintCapabilities ドキュメント</td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>ParameterDef</td>
</tr>
<tr class="even">
<td>目次</td>
<td><p>このドキュメントの「1.8.1」の説明に従って、素材のマッピングのパラメーターは MaterialMapParamType、。</p>
<p><strong>子:</strong>MaterialMapParamType</p>
<p><strong>説明 :</strong></p>
<p>プロパティ値が必要があります psf:MinLength 整数 1 以上であります。</p>
<p>Psf:MaxLength プロパティの値は、ベンダーによって定義することがあり、psf:MinLength プロパティの値以上にする必要があります。 1024 になります。</p>
<p>プロパティ値が必要があります psf:Mandatory する psk: 省略可能です。</p>
<p>プロパティ値が必要があります psf:UnitType materialMapUnitType をします。</p>
<p>プロパティ値が必要があります psk3d:Job3DMaterialSelected Job3DMaterials プロパティの子の名前を参照します。</p></td>
</tr>
</tbody>
</table>



Job3DRaftMaterial 初期化プロファイル

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td><em>仕入先の指定</em></td>
</tr>
<tr class="even">
<td>に対して有効です。</td>
<td>PrintTicket ドキュメント</td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>ParameterInit</td>
</tr>
<tr class="even">
<td>目次</td>
<td><p>1 つのみを含む&lt;値&gt;子要素として次のとおりです。</p>
<p><strong>子:</strong>Value</p>
<p><strong>xsi:type:</strong>Psk3d:MaterialMapUnitType</p>
<p><strong>値:</strong>素材のリスト</p>
<p><strong>説明 :</strong>資料一覧する必要があります、素材 ID:index 値のセミコロンで区切られたリスト basematerials モデル ペイロード内の参照します。</p></td>
</tr>
</tbody>
</table>



素材のパラメーターのマッピングのキーワードの使用方法

パラメーターの定義は次のとおりです。

```cpp
   <psf:ParameterDef name="vnd:Job3DABS_REDMap">
       <psf:Property name="psf:DataType">
          <psf:Value xsi:type="xsd:QName">xsd:string</psf:Value>
       </psf:Property>
       <psf:Property name="psf:MinLength">
          <psf:Value xsi:type="xsd:integer">1</psf:Value>
       </psf:Property>
       <psf:Property name="psf:MaxLength">
          <psf:Value xsi:type="xsd:integer">1024</psf:Value>
       </psf:Property>
       <psf:Property name="psf:Mandatory">
          <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
       </psf:Property>
       <psf:Property name="psf:UnitType">
          <psf:Value xsi:type="xsd:string">characters</psf:Value>
       </psf:Property>
       <psf:Property name="psk3d:Job3DMaterialSelected">
          <psf:Value xsi:type="xsd:QName">vnd:ABS_RED</psf:Value>
       </psf:Property>
   </psf:ParameterDef>
   <psf:ParameterDef name="vnd:Job3DPLA_TEALMap">
       <psf:Property name="psf:DataType">
          <psf:Value xsi:type="xsd:QName">xsd:string</psf:Value>
       </psf:Property>
       <psf:Property name="psf:MinLength">
          <psf:Value xsi:type="xsd:integer">1</psf:Value>
       </psf:Property>
       <psf:Property name="psf:MaxLength">
          <psf:Value xsi:type="xsd:integer">1024</psf:Value>
       </psf:Property>
       <psf:Property name="psf:Mandatory">
          <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
       </psf:Property>
       <psf:Property name="psf:UnitType">
          <psf:Value xsi:type="xsd:string">characters</psf:Value>
       </psf:Property>
       <psf:Property name="psk3d:Job3DMaterialSelected">
          <psf:Value xsi:type="xsd:QName">vnd:PLA_TEAL</psf:Value>
       </psf:Property>
   </psf:ParameterDef>
```

このパラメーターは、次のように初期化されます。

```cpp
   psf:ParameterInit name="vnd:Job3DABS_REDMap">
      <psf:Value xsi:type="xsd:string">1:0;1:2</psf:Value>
   </psf:ParameterInit>
   <psf:ParameterInit name="vnd:Job3DPLA_TEALMap">
      <psf:Value xsi:type="xsd:string">1:1</psf:Value>
   </psf:ParameterInit>
```








