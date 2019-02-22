---
title: DocumentFinalParameters 要素
description: 必要な DocumentFinalParameters 要素には、画像を取得するデバイスのスキャンを使用する実際の DocumentParameters 要素が含まれています。
ms.assetid: 54e3c96c-70a1-48c5-8718-45b0a71ff9b1
keywords:
- DocumentFinalParameters 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn DocumentFinalParameters
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1771074892d19dbfb3fecbb0c51622b9c52b8d41
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539043"
---
# <a name="documentfinalparameters-element"></a>DocumentFinalParameters 要素


必要な**DocumentFinalParameters**要素が含まれていますが、実際[ **DocumentParameters** ](documentparameters.md)画像を取得するデバイスのスキャンを使用する要素。

<a name="usage"></a>使用方法
-----

```xml
<wscn:DocumentFinalParameters>
  child elements
</wscn:DocumentFinalParameters>
```

<a name="attributes"></a>属性
----------

属性はありません。

## <a name="child-elements"></a>子要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="compressionqualityfactor.md" data-raw-source="[&lt;strong&gt;CompressionQualityFactor&lt;/strong&gt;](compressionqualityfactor.md)"><strong>CompressionQualityFactor</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="contenttype.md" data-raw-source="[&lt;strong&gt;ContentType&lt;/strong&gt;](contenttype.md)"><strong>ContentType</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="exposure.md" data-raw-source="[&lt;strong&gt;Exposure&lt;/strong&gt;](exposure.md)"><strong>公開</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="filmscanmode.md" data-raw-source="[&lt;strong&gt;FilmScanMode&lt;/strong&gt;](filmscanmode.md)"><strong>FilmScanMode</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="format.md" data-raw-source="[&lt;strong&gt;Format&lt;/strong&gt;](format.md)"><strong>書式設定</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="imagestotransfer.md" data-raw-source="[&lt;strong&gt;ImagesToTransfer&lt;/strong&gt;](imagestotransfer.md)"><strong>ImagesToTransfer</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="inputsize.md" data-raw-source="[&lt;strong&gt;InputSize&lt;/strong&gt;](inputsize.md)"><strong>InputSize</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="inputsource.md" data-raw-source="[&lt;strong&gt;InputSource&lt;/strong&gt;](inputsource.md)"><strong>指定</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="mediasides.md" data-raw-source="[&lt;strong&gt;MediaSides&lt;/strong&gt;](mediasides.md)"><strong>MediaSides</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="rotation.md" data-raw-source="[&lt;strong&gt;Rotation&lt;/strong&gt;](rotation.md)"><strong>回転</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scaling.md" data-raw-source="[&lt;strong&gt;Scaling&lt;/strong&gt;](scaling.md)"><strong>スケーリング</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="createscanjobresponse.md" data-raw-source="[&lt;strong&gt;CreateScanJobResponse&lt;/strong&gt;](createscanjobresponse.md)"><strong>CreateScanJobResponse</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="documents.md" data-raw-source="[&lt;strong&gt;Documents&lt;/strong&gt;](documents.md)"><strong>ドキュメント</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**DocumentFinalParameters**要素には、WSD スキャン サービスで使用される実際のスキャン ジョブの値を格納している要素が含まれています。 これらの値のジョブで要求された値が異なる場合があります[ **ScanTicket** ](scanticket.md)さまざまな理由です。 各パラメーターは、この階層が表示され、値がわかっている場合に入力する必要があります。

特定の要素内で、 **DocumentFinalParameters**階層に含めることができます、**オーバーライド**と**UsedDefault**ブール属性。 場合、**オーバーライド**属性が存在し、true の要素で、デバイスのスキャンが指定された値で要求された値をオーバーライドします。 場合、 **UsedDefault**属性が存在し、true の要素で、デバイスのスキャンは、指定した既定値を使用します。

[**明るさ**](brightness.md)[**ColorProcessing**](colorprocessing.md)[**CompressionQualityFactor** ](compressionqualityfactor.md) [**ContentType**](contenttype.md)[**コントラスト**](contrast.md)[**FilmScanMode** ](filmscanmode.md) [**形式**](format.md)[**高さ**](height.md)[**ImagesToTransfer** ](imagestotransfer.md) [**指定**](inputsource.md)[**回転**](rotation.md)[**ScalingHeight** ](scalingheight.md) [**ScalingWidth**](scalingwidth.md)[**ScanRegionHeight**](scanregionheight.md)[**ScanRegionWidth**](scanregionwidth.md) [ **ScanRegionXOffset**](scanregionxoffset.md)[**ScanRegionYOffset** ](scanregionyoffset.md) [**鮮明度**](sharpness.md)[**幅**](width.md)

次の要素を持つことができます、**オーバーライド**と**UsedDefault**属性。[**明るさ**](brightness.md)、 [ **ColorProcessing**](colorprocessing.md)、 [ **CompressionQualityFactor**](compressionqualityfactor.md)、 [**ContentType**](contenttype.md)、 [**コントラスト**](contrast.md)、 [ **FilmScanMode**](filmscanmode.md)、[**形式**](format.md)、 [**高さ**](height.md)、 [ **ImagesToTransfer** ](imagestotransfer.md)、 [**指定**](inputsource.md)、 [**回転**](rotation.md)、 [ **ScalingHeight**](scalingheight.md)、 [ **ScalingWidth**](scalingwidth.md)、 [ **ScanRegionHeight**](scanregionheight.md)、 [ **ScanRegionWidth**](scanregionwidth.md)、 [ **ScanRegionXOffset**](scanregionxoffset.md)、 [ **ScanRegionYOffset** ](scanregionyoffset.md)、 [**鮮明度**](sharpness.md)、および[**幅**](width.md)します。

## <a name="see-also"></a>関連項目


[**明るさ**](brightness.md)

[**ColorProcessing**](colorprocessing.md)

[**CompressionQualityFactor**](compressionqualityfactor.md)

[**ContentType**](contenttype.md)

[**コントラスト**](contrast.md)

[**CreateScanJobResponse**](createscanjobresponse.md)

[**DocumentParameters**](documentparameters.md)

[**ドキュメント**](documents.md)

[**公開**](exposure.md)

[**FilmScanMode**](filmscanmode.md)

[**書式設定**](format.md)

[**Height**](height.md)

[**ImagesToTransfer**](imagestotransfer.md)

[**InputSize**](inputsize.md)

[**指定**](inputsource.md)

[**MediaSides**](mediasides.md)

[**回転**](rotation.md)

[**スケーリング**](scaling.md)

[**ScalingHeight**](scalingheight.md)

[**ScalingWidth**](scalingwidth.md)

[**ScanRegionHeight**](scanregionheight.md)

[**ScanRegionWidth**](scanregionwidth.md)

[**ScanRegionXOffset**](scanregionxoffset.md)

[**ScanRegionYOffset**](scanregionyoffset.md)

[**ScanTicket**](scanticket.md)

[**鮮明度**](sharpness.md)

[**幅**](width.md)

 

 






