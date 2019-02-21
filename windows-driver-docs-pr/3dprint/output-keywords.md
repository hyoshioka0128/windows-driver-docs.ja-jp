---
title: 出力キーワード
description: これらのキーワードを使用して、特定の 3D 製造ジョブの実際の出力のプロセスを記述します。
ms.assetid: FBCE5E9C-8411-46C1-899E-A6C8FE27D947
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2191cc564de1a13331d9185b9c4d161ab31b6d35
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550217"
---
# <a name="output-keywords"></a>出力キーワード


これらのキーワードを使用して、特定の 3D 製造ジョブの実際の出力のプロセスを記述します。

## <a name="41-job3dquality"></a>4.1. Job3DQuality


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
<td>psk3d:Job3DQuality</td>
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
<p><strong>子:</strong>オプション psk3d:Draft</p>
<p><strong>説明 :</strong>このオプションは、デバイスはデバイスの可能な最も低い解像度の最も高速な出力である必要がありますを指定します。</p>
<p><strong>子:</strong>オプション psk3d:Medium</p>
<p><strong>説明 :</strong>このオプションは、デバイスが出力と出力解像度の高速化に同じ優先順位を指定する必要がありますを指定します。</p>
<p><strong>子:</strong>オプション psk3d:High</p>
<p><strong>説明 :</strong>このオプションは、デバイスが速度に関係なく、出力の解像度に最も高い優先順位を指定する必要がありますを指定します。</p></td>
</tr>
</tbody>
</table>

 

Job3DQuality キーワードの使用状況

```xml
<psf:Feature name="psk3d:Job3DQuality">
    <psf:Property name="SelectionType">
        <psf:Value xsi:type="xsd:QName">psk:PickOne</psf:Value>
    </psf:Property>
    <psf:Option name="psk3d:Draft" />
    <psf:Option name="psk3d:Medium" />
    <psf:Option name="psk3d:High" />
</psf:Feature>
```

## <a name="42-job3ddensity"></a>4.2. Job3DDensity


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
<td>psk3d:Job3DDensity</td>
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
<p><strong>子:</strong>オプション psk3d:Hollow</p>
<p><strong>説明 :</strong>このオプションは、デバイスがない内部のサポート (中空) を持つジョブを出力する必要がありますを指定します。</p>
<p><strong>子:</strong>オプション psk3d:Low</p>
<p><strong>説明 :</strong>このオプションは、デバイスが約 10 %infill のサポートを持つジョブを出力する必要がありますを指定します。</p>
<p><strong>子:</strong>オプション psk3d:Medium</p>
<p><strong>説明 :</strong>このオプションは、デバイスが約 25 %infill のサポートを持つジョブを出力する必要がありますを指定します。</p>
<p><strong>子:</strong>オプション psk3d:High</p>
<p><strong>説明 :</strong>このオプションは、デバイスが約 50 %infill のサポートを持つジョブを出力する必要がありますを指定します。</p>
<p><strong>子:</strong>オプション psk3d:Solid</p>
<p><strong>説明 :</strong>このオプションの指定が、デバイスを出力する 100% 使用されたジョブします。</p></td>
</tr>
</tbody>
</table>

 

Job3DDensity キーワードの使用状況

```xml
<psf:Feature name="psk3d:Job3DDensity">
    <psf:Property name="SelectionType">
        <psf:Value xsi:type="xsd:QName">psk:PickOne</psf:Value>
    </psf:Property>
    <psf:Option name="psk3d:Hollow"/>
    <psf:Option name="psk3d:Low"/>
    <psf:Option name="psk3d:Medium"/>
    <psf:Option name="psk3d:High"/>
    <psf:Option name="psk3d:Solid"/>
</psf:Feature>
```

## <a name="43-job3dsliceheight"></a>4.3. Job3DSliceHeight


Psk3d:Job3DQuality パラメーターが不十分と見なされた場合、各スライスの太さを通信するために使用してこのパラメーターください。

Job3DSliceHeight キーワード プロファイル

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
<td>psk3d:Job3DSliceHeight</td>
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
<td><p>§2.1.3.1、」の説明に従って、psk3d:Job3DSliceHeight は、の IntegerParamType &quot; &lt;psf:ParameterDef&gt; &quot;印刷スキーマ仕様でします。</p>
<p><strong>子:</strong>IntegerParamType</p>
<p><strong>説明 :</strong></p>
<p>Psf:MinValue は 0 より大きくなければプロパティ値が必要があります。</p>
<p>Psf:MaxValue プロパティの値は、ベンダーによって定義することがあり、psf:MinValue プロパティの値以上にする必要があります。</p>
<p>プロパティ値が必要があります psf:Multiple 1 であります。</p>
<p>プロパティ値が必要があります psf:Multiple 1 であります。</p>
<p>プロパティ値が必要があります psf:UnitType ミクロンをします。</p></td>
</tr>
</tbody>
</table>

 

Job3DSliceHeight 初期化プロファイル

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
<td>psk3d:Job3DSliceHeight</td>
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
<p><strong>xsi:type:</strong> xsd:integer</p>
<p><strong>値:</strong>SliceHeight</p>
<p><strong>説明 :</strong>ミクロンで目的のスライスの高さに等しいの正の整数を含める SliceHeight 必要があります。</p></td>
</tr>
</tbody>
</table>

 

Job3DSliceHeight キーワードの使用状況

パラメーターの定義は次のとおりです。

```xml
<psf:ParameterDef name="psk3d:Job3DSliceHeight">
    <psf:Property name="psf:DataType">
        <psf:Value xsi:type="xsd:QName">xsd:integer</psf:Value>
    </psf:Property>
    <psf:Property name="psf:DefaultValue">
        <psf:Value xsi:type="xsd:integer">100</psf:Value>
    </psf:Property>
    <psf:Property name="psf:MaxValue">
        <psf:Value xsi:type="xsd:integer">3000</psf:Value>
    </psf:Property>
    <psf:Property name="psf:MinValue">
        <psf:Value xsi:type="xsd:integer">50</psf:Value>
    </psf:Property>
    <psf:Property name="psf:Multiple">
        <psf:Value xsi:type="xsd:integer">1</psf:Value>
    </psf:Property>
    <psf:Property name="psf:Mandatory">
        <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
    </psf:Property>
    <psf:Property name="psf:UnitType">
        <psf:Value xsi:type="xsd:string">microns</psf:Value>
    </psf:Property>
</psf:ParameterDef>
```

このパラメーターは、次のように初期化されます。

```xml
<psf:ParameterInit name="psk3d:Job3DSliceHeight">
    <psf:Value xsi:type="xsd:integer">150</psf:Value>
</psf:ParameterInit>
```

## <a name="44-job3doutputcolor"></a>4.4. Job3DOutputColor


Psk3d:Job3DOutputColor キーワードは、モデルが完全な色、または、単一のモノクロ素材 (基本マテリアルの色) で再現するかどうかを指定します。

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
<td>psk3d:Job3DOutputColor</td>
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
<p><strong>子:</strong>オプション psk3d:Color</p>
<p><strong>説明 :</strong>このオプションは、デバイスが完全な色のジョブを出力するを指定します。</p>
<p><strong>子:</strong>オプション psk3d:Monochrome</p>
<p><strong>説明 :</strong>このオプションは、デバイスが 1 つの色のジョブを出力する必要がありますを指定します。</p></td>
</tr>
</tbody>
</table>

 

Job3DOutputColor キーワードの使用状況

```xml
<psf:Feature name="psk3d:Job3DOutputColor">
    <psf:Property name="SelectionType">
        <psf:Value xsi:type="xsd:QName">psk:PickOne</psf:Value>
    </psf:Property>
    <psf:Option name="psk3d:Color" />
    <psf:Option name="psk3d:Monochrome" />
</psf:Feature>
```

 

 




