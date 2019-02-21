---
title: DocumentParameters 要素
description: 省略可能な DocumentParameters 要素には、処理ジョブ内のドキュメントに適用する関数のイメージを指定します。
ms.assetid: 3b76bf47-a674-4925-aa0f-b2310e1ad1ce
keywords:
- DocumentParameters 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn DocumentParameters
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e22989282319b79a428946bec4d5ba1d91447fb9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531092"
---
# <a name="documentparameters-element"></a>DocumentParameters 要素


省略可能な**DocumentParameters**要素は、処理ジョブ内のドキュメントに適用する関数のイメージを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:DocumentParameters>
  child elements
</wscn:DocumentParameters>
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
<td><p><a href="defaultscanticket.md" data-raw-source="[&lt;strong&gt;DefaultScanTicket&lt;/strong&gt;](defaultscanticket.md)"><strong>DefaultScanTicket</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanticket.md" data-raw-source="[&lt;strong&gt;ScanTicket&lt;/strong&gt;](scanticket.md)"><strong>ScanTicket</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**DocumentParameters**要素は、処理関数とその値に対して、ジョブまたはドキュメントに適用されるイメージを指定します。

クライアントは、ドキュメント内のパラメーターを処理を必要に応じて指定できます、 **ScanTicket**中に要素を[ **CreateScanJobRequest** ](createscanjobrequest.md)操作。 WSD スキャン サービスは、各子要素がで指定されている有効な値に設定されていることを確認するクライアントを提供するすべてのデータを検証する必要があります、 [ **ScannerConfiguration** ](scannerconfiguration.md)要素。

WSD スキャン提供がその既定値を使用する必要があります**DocumentParameters**値は、クライアントがいずれかを提供しない場合。

## <a name="see-also"></a>関連項目


[**CompressionQualityFactor**](compressionqualityfactor.md)

[**ContentType**](contenttype.md)

[**CreateScanJobRequest**](createscanjobrequest.md)

[**DefaultScanTicket**](defaultscanticket.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**公開**](exposure.md)

[**FilmScanMode**](filmscanmode.md)

[**書式設定**](format.md)

[**ImagesToTransfer**](imagestotransfer.md)

[**InputSize**](inputsize.md)

[**指定**](inputsource.md)

[**MediaSides**](mediasides.md)

[**回転**](rotation.md)

[**スケーリング**](scaling.md)

[**ScanTicket**](scanticket.md)

[**ScannerConfiguration**](scannerconfiguration.md)

 

 






