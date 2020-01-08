---
title: デバイス制御のキーワード
description: これらのキーワードは、3D 製造デバイスを制御するために使用されます。
ms.assetid: 1F0CBFC4-F641-4D82-9173-C89218E822B5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42941f7056e87d85962a123cccb5692a0baeea84
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652784"
---
# <a name="device-control-keywords"></a>デバイス制御のキーワード


これらのキーワードは、3D 製造デバイスを制御するために使用されます。

## <a name="21-job3doutputarea"></a>2.1. Job3DOutputArea


Psk3d: Job3DOutputArea プロパティは、デバイスが実際に印刷できる領域のサイズを定義するために使用する必要があります。 Job3DOutputArea の左下隅は、(0, 0, 0) として定義されています。 Job3DOutputAreaWidth、Job3DOutputAreaDepth、および Job3DOutputAreaHeight の各プロパティは印刷ボリュームの境界ボックスを定義しますが、印刷ボリュームが cuboid でない場合は、必要に応じて境界ボックス内の正確な印刷ボリュームを定義します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細情報</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td>psk3d:Job3DOutputArea</td>
</tr>
<tr class="even">
<td>有効期間</td>
<td>PrintCapabilities ドキュメント</td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>プロパティ</td>
</tr>
<tr class="even">
<td>目次</td>
<td><p>には、Job3DOutputAreaWidth、Job3DOutputAreaDepth、Job3DOutputAreaHeight の各プロパティを含み、Job3DOutputAreaMesh を含むことができる、子要素を1つだけ含む &lt;&gt; 値が含まれています。</p>
<p><strong>子:</strong>数値</p>
<p><strong>xsi: type:</strong>該当なし</p>
<p><strong>値:</strong>OutputDimensions</p>
<p><strong>説明:</strong>OutputDimensions には、各出力領域のサイズを構成する3つのプロパティのセットが含まれています。</p></td>
</tr>
</tbody>
</table>

 

Job3DOutputArea キーワードの使用法

```xml
<psf:Property name="psk3d:Job3DOutputArea">
    <psf:Property name="psk3d:Job3DOutputAreaWidth">
        <psf:Value xsi:type="xsd:integer">285000</psf:Value>
    </psf:Property>
    <psf:Property name="psk3d:Job3DOutputAreaDepth">
        <psf:Value xsi:type="xsd:integer">153000</psf:Value>
    </psf:Property>
    <psf:Property name="psk3d:Job3DOutputAreaHeight">
        <psf:Value xsi:type="xsd:integer">155000</psf:Value>
    </psf:Property>
     <psf:Property name="psk3d:Job3DOutputAreaMesh">
         <psf:Value xsi:type="xsd:string">
          <![CDATA[
            <mesh xmlns="https://schemas.microsoft.com/3dmanufacturing/mesh/2014/11" unit="millimeter">
             <vertices>
                <vertex x="0" y="0" z="0" />
                <vertex x="0" y="153000" z="0" />
                <vertex x="285000" y="0" z="0" />
                <vertex x="0" y="0" z="155000" />
             </vertices>
             <triangles>
                <triangle v1="0" v2="1" v3="2" />
                <triangle v1="0" v2="2" v3="3" />
                <triangle v1="0" v2="3" v3="1" />
                <triangle v1="2" v2="1" v3="3" />
             </triangles>
          </mesh>
          ]]></psf:Value>
    </psf:Property>
</psf:Property>
```

### <a name="211-job3doutputareawidth"></a>2.1.1. Job3DOutputAreaWidth

X 軸に沿った出力領域の幅 (ミクロン単位) を記述します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細情報</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td>psk3d:Job3DOutputAreaWidth</td>
</tr>
<tr class="even">
<td>有効期間</td>
<td>PrintCapabilities ドキュメント</td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>プロパティ</td>
</tr>
<tr class="even">
<td>目次</td>
<td><p>次のように、子要素&gt; 1 つの &lt;値を格納します。</p>
<p><strong>子:</strong>数値</p>
<p><strong>xsi: type:</strong> xsd: integer</p>
<p><strong>値:</strong>OutputWidth</p>
<p><strong>説明:</strong>OutputWidth には、X 軸に沿った出力領域の幅 (ミクロン単位) と等しい、0より大きい整数を含める必要があります。</p></td>
</tr>
</tbody>
</table>

 

### <a name="212-job3doutputareadepth"></a>2.1.2. Job3DOutputAreaDepth

Y 軸に沿った出力領域の深さをミクロン単位で記述します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細情報</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td>psk3d:Job3DOutputAreaDepth</td>
</tr>
<tr class="even">
<td>有効期間</td>
<td>PrintCapabilities ドキュメント</td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>プロパティ</td>
</tr>
<tr class="even">
<td>目次</td>
<td><p>次のように、子要素&gt; 1 つの &lt;値を格納します。</p>
<p><strong>子:</strong>数値</p>
<p><strong>xsi: type:</strong> xsd: integer</p>
<p><strong>値:</strong>OutputDepth</p>
<p><strong>説明:</strong>OutputDepth には、Y 軸に沿った出力領域の深さ (ミクロン) と同じ、0より大きい整数を含める必要があります。</p></td>
</tr>
</tbody>
</table>

 

### <a name="213-job3doutputareaheight"></a>2.1.3. Job3DOutputAreaHeight

Z 軸に沿った出力領域の高さをミクロン単位で表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細情報</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td>psk3d:Job3DOutputAreaHeight</td>
</tr>
<tr class="even">
<td>有効期間</td>
<td>PrintCapabilities ドキュメント</td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>プロパティ</td>
</tr>
<tr class="even">
<td>目次</td>
<td><p>次のように、子要素&gt; 1 つの &lt;値を格納します。</p>
<p><strong>子:</strong>数値</p>
<p><strong>xsi: type:</strong> xsd: integer</p>
<p><strong>値:</strong>OutputHeight</p>
<p><strong>説明:</strong>OutputHeight には、Z 軸に沿った出力領域の深さ (ミクロン) に等しい、0より大きい整数を含める必要があります。</p></td>
</tr>
</tbody>
</table>

 

### <a name="214-job3doutputareamesh"></a>2.1.4. Job3DOutputAreaMesh

四角形の prism がない場合の出力ボリュームの形状について説明します。 文字列値は、&lt;メッシュ&gt; 要素 (頂点と三角形を含む) の3MF 仕様に従った XML blob であり、3MF メッシュの manifoldness 標準に準拠しています。 この多面体は、前の OutputArea プロパティで記述された境界ボックス内に完全に含まれている必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細情報</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td>psk3d:Job3DOutputAreaMesh</td>
</tr>
<tr class="even">
<td>有効期間</td>
<td>PrintCapabilities ドキュメント</td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>プロパティ</td>
</tr>
<tr class="even">
<td>目次</td>
<td><p>次のように、子要素&gt; 1 つの &lt;値を格納します。</p>
<p><strong>子:</strong>数値</p>
<p><strong>xsi: type:</strong> xsd: string</p>
<p><strong>値:</strong>OutputMesh</p>
<p><strong>説明:</strong>OutputMesh には、出力ボリュームの境界を表す3MF 仕様のメッシュセクションで定義されているように、頂点と三角形の xml 文字列を含める必要があります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="22-job3dappname"></a>2.2. Job3DAppName


デバイスは、このプリンターが選択されたときに [印刷] ダイアログで呼び出される既定のワークフローアプリ (例では、既定のワークフローが含まれています) を識別できません。 このワークフローアプリでは、このデバイスの3D 印刷ジョブを最適に設定するために必要な、または必要なカスタム UI を使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細情報</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td>psk3d:Job3DAppName</td>
</tr>
<tr class="even">
<td>有効期間</td>
<td>PrintCapabilities ドキュメント</td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>プロパティ</td>
</tr>
<tr class="even">
<td>目次</td>
<td><p>次のように、子要素&gt; 1 つの &lt;値を格納します。</p>
<p><strong>子:</strong>数値</p>
<p><strong>xsi: type:</strong> xsd: string</p>
<p><strong>値:</strong></p>
<p><strong>説明:</strong>最新の [印刷] ダイアログでこのプリンターに使用するワークフローアプリのパッケージ名</p></td>
</tr>
</tbody>
</table>

 

Job3DAppName キーワードの使用法

```xml
<psf:Property name="psk3d:Job3DAppName">
    <psf:Value xsi:type="xsd:string">Microsoft.3DBuilder_8wekyb3d8bbwe</psf:Value>
</psf:Property>
```

## <a name="23-job3dwsdapackagefamilyname"></a>2.3. Job3DWSDAPackageFamilyName


デバイスは、ユーザーが **[詳細設定**] ボタンをクリックしたときに印刷ダイアログを起動する UWP デバイスアプリを識別できます。 このアプリは、プリンターのメンテナンス、素材の設定、調整などの操作のための UI を提供します。既定値は指定されていないため、このキーワードを省略すると、 **[詳細設定**] ボタンは表示されません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細情報</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td>psk3d:Job3DWSDAPackageFamilyName</td>
</tr>
<tr class="even">
<td>有効期間</td>
<td>PrintCapabilities ドキュメント</td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>プロパティ</td>
</tr>
<tr class="even">
<td>目次</td>
<td><p>次のように、子要素&gt; 1 つの &lt;値を格納します。</p>
<p><strong>子:</strong>数値</p>
<p><strong>xsi: type:</strong> xsd: string</p>
<p><strong>値:</strong></p>
<p><strong>説明:</strong>このプリンターの詳細設定に使用する UWP デバイスアプリのパッケージ名。</p></td>
</tr>
</tbody>
</table>

 

Job3DWSDAPackageFamilyName キーワードの使用法

```xml
<psf:Property name="psk3d:Job3DWSDAPackageFamilyName">
    <psf:Value xsi:type="xsd:string"> </psf:Value>
</psf:Property>
```

## <a name="24-job3d3mfversion"></a>2.4. Job3D3MFVersion


デバイスは、Windows プリントシステムから受信する必要がある3MF ファイルのバージョンを識別する必要があります。 バージョンは、適切なバージョンのコア仕様の URI 名前空間によって指定されます。 旧バージョンとの互換性を維持するために、このキーワードを省略すると、既定値の "0.93<https://schemas.microsoft.com/3dmanufacturing/2013/01”>を使用することを前提としています。これは推奨されません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細情報</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td>psk3d:Job3D3MFVersion</td>
</tr>
<tr class="even">
<td>有効期間</td>
<td>PrintCapabilities ドキュメント</td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>プロパティ</td>
</tr>
<tr class="even">
<td>目次</td>
<td><p>次のように、子要素&gt; 1 つの &lt;値を格納します。</p>
<p><strong>子:</strong>数値</p>
<p><strong>xsi: type:</strong> xsd: string</p>
<p><strong>値:</strong></p>
<p><strong>説明:</strong>デバイスでサポートされている3MF コアバージョンを入力として定義する URI 名前空間。</p></td>
</tr>
</tbody>
</table>

 

Job3D3MFVersion キーワードの使用法

```xml
<psf:Property name="psk3d:Job3D3MFVersion">
    <psf:Value xsi:type="xsd:string"> https://schemas.microsoft.com/3dmanufacturing/core/2015/02</psf:Value>
</psf:Property>
```

## <a name="25-job3d3mfextensions"></a>2.5. Job3D3MFExtensions


デバイスでは、認識される3つの MF 拡張機能 (名前空間で区切られたリスト) を指定できます。たとえば、使用可能な場合は、印刷システムでスライスデータを送信できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>詳細情報</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名前</td>
<td>psk3d:Job3D3MFExtensions</td>
</tr>
<tr class="even">
<td>有効期間</td>
<td>PrintCapabilities ドキュメント</td>
</tr>
<tr class="odd">
<td>要素型</td>
<td>プロパティ</td>
</tr>
<tr class="even">
<td>目次</td>
<td><p>次のように、子要素&gt; 1 つの &lt;値を格納します。</p>
<p><strong>子:</strong>数値</p>
<p><strong>xsi: type:</strong> xsd: string</p>
<p><strong>値:</strong></p>
<p><strong>説明:</strong>デバイスでサポートされている3MF 拡張機能を入力として定義する URI 名前空間のスペース区切りのリスト。</p></td>
</tr>
</tbody>
</table>

 

Job3D3MFExtensions キーワードの使用法

```xml
<psf:Property name="psk3d:Job3D3MFExtensions">
    <psf:Value xsi:type="xsd:string"> https://schemas.microsoft.com/3dmanufacturing/material/2015/02</psf:Value>
</psf:Property>
```

 

 




