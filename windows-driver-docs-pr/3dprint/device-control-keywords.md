---
title: デバイス制御のキーワード
description: これらのキーワードを使用して、3 D の製造デバイスの制御を提供します。
ms.assetid: 1F0CBFC4-F641-4D82-9173-C89218E822B5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87ec29efb414e47f69866dba34ad695b4763dcb1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571789"
---
# <a name="device-control-keywords"></a>デバイス制御のキーワード


これらのキーワードを使用して、3 D の製造デバイスの制御を提供します。

## <a name="21-job3doutputarea"></a>2.1. Job3DOutputArea


Psk3d:Job3DOutputArea プロパティは、実際に印刷できるデバイス領域のサイズを定義するために使用する必要があります。 Job3DOutputArea の左下隅が (0,0,0) として定義されます。 Job3DOutputAreaWidth、Job3DOutputAreaDepth、および Job3DOutputAreaHeight プロパティ Job3DOutputAreaMesh はその境界ボックス内の正確な印刷量を必要に応じて定義印刷量でない場合がある場合、印刷、ボリュームの境界ボックスを定義します。

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
<td>psk3d:Job3DOutputArea</td>
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
<td><p>1 つのみを含む&lt;値&gt;Job3DOutputAreaWidth、Job3DOutputAreaDepth、および Job3DOutputAreaHeight プロパティを含める必要があるあり、Job3DOutputAreaMesh を含めることができる子要素。</p>
<p><strong>子:</strong>値</p>
<p><strong>xsi:type:</strong>N/A</p>
<p><strong>値:</strong>OutputDimensions</p>
<p><strong>説明 :</strong>OutputDimensions には、各出力領域のサイズを構成する 3 つのプロパティのセットが含まれています。</p></td>
</tr>
</tbody>
</table>

 

Job3DOutputArea キーワードの使用状況

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
            <mesh xmlns="http://schemas.microsoft.com/3dmanufacturing/mesh/2014/11" unit="millimeter">
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

ミクロン、X 軸に沿った出力領域の幅をについて説明します。

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
<td>psk3d:Job3DOutputAreaWidth</td>
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
<p><strong>子:</strong>値</p>
<p><strong>xsi:type:</strong> xsd:integer</p>
<p><strong>値:</strong>OutputWidth</p>
<p><strong>説明 :</strong>ミクロン内の X 軸では、出力領域の幅と同じである 0 より大きい整数を含める OutputWidth 必要があります。</p></td>
</tr>
</tbody>
</table>

 

### <a name="212-job3doutputareadepth"></a>2.1.2. Job3DOutputAreaDepth

ミクロン、Y 軸に沿った出力領域の深さをについて説明します。

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
<td>psk3d:Job3DOutputAreaDepth</td>
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
<p><strong>子:</strong>[値]</p>
<p><strong>xsi:type:</strong> xsd:integer</p>
<p><strong>値:</strong>OutputDepth</p>
<p><strong>説明 :</strong>ミクロン内の Y 軸では、出力領域の深さと同じである 0 より大きい整数を含める OutputDepth 必要があります。</p></td>
</tr>
</tbody>
</table>

 

### <a name="213-job3doutputareaheight"></a>2.1.3. Job3DOutputAreaHeight

ミクロン、Z 軸に沿った出力領域の高さをについて説明します。

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
<td>psk3d:Job3DOutputAreaHeight</td>
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
<p><strong>子:</strong>値</p>
<p><strong>xsi:type:</strong> xsd:integer</p>
<p><strong>値:</strong>OutputHeight</p>
<p><strong>説明 :</strong>ミクロン等しい Z 軸では、出力領域の深さにある、0 より大きい整数を含める OutputHeight 必要があります。</p></td>
</tr>
</tbody>
</table>

 

### <a name="214-job3doutputareamesh"></a>2.1.4. Job3DOutputAreaMesh

四角形の prism でない場合に、出力のボリュームの形状について説明します。 文字列値が次の 3MF 仕様 XML blob が、&lt;メッシュ&gt;要素 (頂点と三角形を格納していると 3MF メッシュの manifoldness 標準に準拠している)。 この多面体は、以前 OutputArea プロパティで説明されている境界ボックス内で完全に含まれる必要があります。

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
<td>psk3d:Job3DOutputAreaMesh</td>
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
<p><strong>子:</strong>値</p>
<p><strong>xsi:type:</strong> xsd:string</p>
<p><strong>値:</strong>OutputMesh</p>
<p><strong>説明 :</strong>出力のボリュームの境界を表す 3MF 仕様のメッシュのセクションで定義されている、頂点と三角形の xml 文字列を含む OutputMesh にする必要があります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="22-job3dappname"></a>2.2. Job3DAppName


デバイス可能性があります (例では、既定のワークフローが含まれています)、既定以外のワークフロー アプリケーションを識別するこのプリンターを選択すると、印刷ダイアログ ボックスで起動されます。 このワークフロー アプリケーションは、可能性があるために必要なまたは必要な 3D 印刷ジョブを最適なセットをこのデバイスのカスタム ui できます。

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
<td>psk3d:Job3DAppName</td>
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
<p><strong>子:</strong>[値]</p>
<p><strong>xsi:type:</strong> xsd:string</p>
<p><strong>値:</strong></p>
<p><strong>説明 :</strong>最新の印刷 ダイアログ ボックスでこのプリンターを使用するワークフロー アプリのパッケージ名</p></td>
</tr>
</tbody>
</table>

 

Job3DAppName キーワードの使用状況

```xml
<psf:Property name="psk3d:Job3DAppName">
    <psf:Value xsi:type="xsd:string">Microsoft.3DBuilder_8wekyb3d8bbwe</psf:Value>
</psf:Property>
```

## <a name="23-job3dwsdapackagefamilyname"></a>2.3. Job3DWSDAPackageFamilyName


デバイスは、印刷ダイアログを起動する UWP デバイス アプリで見つかる場合があります、**詳細設定**ユーザーがボタンをクリックします。 このアプリでは、プリンターの保守、素材のセットアップ、調整などの操作の UI が表示されます。既定値が指定されていないため、このキーワードを省略すると、ありません**詳細設定**ボタンが表示されます。

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
<td>psk3d:Job3DWSDAPackageFamilyName</td>
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
<p><strong>子:</strong>[値]</p>
<p><strong>xsi:type:</strong> xsd:string</p>
<p><strong>値:</strong></p>
<p><strong>説明 :</strong>このプリンターを使用する UWP デバイス アプリのパッケージ名には、設定を詳細します。</p></td>
</tr>
</tbody>
</table>

 

Job3DWSDAPackageFamilyName キーワードの使用状況

```xml
<psf:Property name="psk3d:Job3DWSDAPackageFamilyName">
    <psf:Value xsi:type="xsd:string"> </psf:Value>
</psf:Property>
```

## <a name="24-job3d3mfversion"></a>2.4. Job3D3MFVersion


デバイスは、Windows の印刷システムから受信する 3MF ファイルのバージョンを識別する必要があります。 バージョンは、適切なバージョンのコア仕様から URI 名前空間によって指定されます。 下位互換性、このキーワードを省略した場合と見なされますの既定値を取得"<http://schemas.microsoft.com/3dmanufacturing/2013/01”>3MF、非推奨のレガシ 0.93 バージョンを示します。

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
<td>psk3d:Job3D3MFVersion</td>
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
<p><strong>子:</strong>値</p>
<p><strong>xsi:type:</strong> xsd:string</p>
<p><strong>値:</strong></p>
<p><strong>説明 :</strong>入力として、デバイスでサポートされている 3MF core バージョンを定義する URI 名前空間。</p></td>
</tr>
</tbody>
</table>

 

Job3D3MFVersion キーワードの使用状況

```xml
<psf:Property name="psk3d:Job3D3MFVersion">
    <psf:Value xsi:type="xsd:string"> http://schemas.microsoft.com/3dmanufacturing/core/2015/02</psf:Value>
</psf:Property>
```

## <a name="25-job3d3mfextensions"></a>2.5. Job3D3MFExtensions


デバイスは (名前空間、スペースで区切られたリストを形成) によって 3MF 拡張機能を指定することがあります、認識、たとえば、印刷システム使用可能な場合は、スライスのデータを送信することができます。

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
<td>psk3d:Job3D3MFExtensions</td>
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
<p><strong>子:</strong>[値]</p>
<p><strong>xsi:type:</strong> xsd:string</p>
<p><strong>値:</strong></p>
<p><strong>説明 :</strong>入力として、デバイスでサポートされている 3MF 拡張機能を定義する URI 名前空間のスペースで区切られたリスト。</p></td>
</tr>
</tbody>
</table>

 

Job3D3MFExtensions キーワードの使用状況

```xml
<psf:Property name="psk3d:Job3D3MFExtensions">
    <psf:Value xsi:type="xsd:string"> http://schemas.microsoft.com/3dmanufacturing/material/2015/02</psf:Value>
</psf:Property>
```

 

 




