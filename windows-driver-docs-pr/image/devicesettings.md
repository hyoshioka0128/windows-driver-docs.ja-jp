---
title: DeviceSettings 要素
description: 必要な DeviceSettings 要素には、デバイスのスキャンの基本的な機能について説明します。
ms.assetid: d12d25f0-fa94-4840-bb1a-cc1a5352767c
keywords:
- DeviceSettings 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn DeviceSettings
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9c36595743fb3004ba75f143e447496d8c421df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364548"
---
# <a name="devicesettings-element"></a>DeviceSettings 要素


必要な**DeviceSettings**要素がデバイスのスキャンの基本的な機能について説明します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:DeviceSettings>
  child elements
</wscn:DeviceSettings>
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
<td><p><a href="autoexposuresupported.md" data-raw-source="[&lt;strong&gt;AutoExposureSupported&lt;/strong&gt;](autoexposuresupported.md)"><strong>AutoExposureSupported</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="brightnesssupported.md" data-raw-source="[&lt;strong&gt;BrightnessSupported&lt;/strong&gt;](brightnesssupported.md)"><strong>BrightnessSupported</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="compressionqualityfactorsupported.md" data-raw-source="[&lt;strong&gt;CompressionQualityFactorSupported&lt;/strong&gt;](compressionqualityfactorsupported.md)"><strong>CompressionQualityFactorSupported</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="contenttypessupported.md" data-raw-source="[&lt;strong&gt;ContentTypesSupported&lt;/strong&gt;](contenttypessupported.md)"><strong>ContentTypesSupported</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="contrastsupported.md" data-raw-source="[&lt;strong&gt;ContrastSupported&lt;/strong&gt;](contrastsupported.md)"><strong>ContrastSupported</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="documentsizeautodetectsupported.md" data-raw-source="[&lt;strong&gt;DocumentSizeAutoDetectSupported&lt;/strong&gt;](documentsizeautodetectsupported.md)"><strong>DocumentSizeAutoDetectSupported</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="formatssupported.md" data-raw-source="[&lt;strong&gt;FormatsSupported&lt;/strong&gt;](formatssupported.md)"><strong>FormatsSupported</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="rotationssupported.md" data-raw-source="[&lt;strong&gt;RotationsSupported&lt;/strong&gt;](rotationssupported.md)"><strong>RotationsSupported</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scalingrangesupported.md" data-raw-source="[&lt;strong&gt;ScalingRangeSupported&lt;/strong&gt;](scalingrangesupported.md)"><strong>ScalingRangeSupported</strong></a></p></td>
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
<td><p><a href="scannerconfiguration.md" data-raw-source="[&lt;strong&gt;ScannerConfiguration&lt;/strong&gt;](scannerconfiguration.md)"><strong>ScannerConfiguration</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**DeviceSettings**要素には、サポートされている値にはで設定できるイメージングのオプションの多くが含まれています、 [ **ScanTicket** ](scanticket.md)スキャン操作の要素。 クライアントに返される値が使用できる**DeviceSettings**有効なを作成する**ScanTicket**要素。

## <a name="see-also"></a>関連項目


[**AutoExposureSupported**](autoexposuresupported.md)

[**BrightnessSupported**](brightnesssupported.md)

[**CompressionQualityFactorSupported**](compressionqualityfactorsupported.md)

[**ContentTypesSupported**](contenttypessupported.md)

[**ContrastSupported**](contrastsupported.md)

[**DocumentSizeAutoDetectSupported**](documentsizeautodetectsupported.md)

[**FormatsSupported**](formatssupported.md)

[**RotationsSupported**](rotationssupported.md)

[**ScalingRangeSupported**](scalingrangesupported.md)

[**ScanTicket**](scanticket.md)

[**ScannerConfiguration**](scannerconfiguration.md)

 

 






