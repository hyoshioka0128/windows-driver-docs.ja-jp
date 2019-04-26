---
title: CompressionQualityFactorSupported 要素
description: 必要な CompressionQualityFactorSupported 要素には、デバイスのスキャンをサポートする圧縮の品質要素の範囲を指定します。
ms.assetid: f82ae450-b948-463e-a6a8-aaea0575ddb9
keywords:
- CompressionQualityFactorSupported 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn CompressionQualityFactorSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad865665dd74739d47577916b8ad33eb228fa393
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354650"
---
# <a name="compressionqualityfactorsupported-element"></a>CompressionQualityFactorSupported 要素


必要な**CompressionQualityFactorSupported**要素は、デバイスのスキャンをサポートする圧縮の品質要素の範囲を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:CompressionQualityFactorSupported>
  child elements
</wscn:CompressionQualityFactorSupported>
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
<td><p><a href="maxvalue.md" data-raw-source="[&lt;strong&gt;MaxValue&lt;/strong&gt;](maxvalue.md)"><strong>MaxValue</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="minvalue.md" data-raw-source="[&lt;strong&gt;MinValue&lt;/strong&gt;](minvalue.md)"><strong>MinValue</strong></a></p></td>
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
<td><p><a href="devicesettings.md" data-raw-source="[&lt;strong&gt;DeviceSettings&lt;/strong&gt;](devicesettings.md)"><strong>DeviceSettings</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

圧縮の品質要因が非可逆圧縮に使用する整数値の圧縮時に許容されるイメージの損失の量を決定する型。 高いほど、要求された fidelity 結果のファイル サイズが大きくなります。

[**MinValue**](minvalue.md)[**MaxValue**](maxvalue.md)

スキャン デバイスをサポートする最小値と最大の圧縮品質要因がで指定された、 [ **MinValue** ](minvalue.md)と[ **MaxValue** ](maxvalue.md)要素では、それぞれします。 **MinValue**と**MaxValue** 1 ~ 100 の整数でなければなりません。 値が 100 にすると、デバイスが最低限の圧縮を使用する必要がありますの最高品質のイメージを生成することをサポートします。 現時点では、JPEG 圧縮では、唯一サポートされている非可逆圧縮の種類です。

## <a name="see-also"></a>関連項目


[**DeviceSettings**](devicesettings.md)

[**MaxValue**](maxvalue.md)

[**MinValue**](minvalue.md)

 

 






