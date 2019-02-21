---
title: 露出要素
description: 省略可能な公開要素には、ドキュメントの公開設定を指定します。
ms.assetid: 70e02507-106f-45a9-92b1-29707cbbcbab
keywords:
- 露出要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn Exposure wscn MustHonor ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2794de0502c5c4ed40fbe04d79645ad6937b01d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530476"
---
# <a name="exposure-element"></a>露出要素


省略可能な**露出**要素をドキュメントの公開設定を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:Exposure wscn:MustHonor=""
  MustHonor = "xs:string">
  child elements
</wscn:Exposure wscn:MustHonor="">
```

<a name="attributes"></a>属性
----------

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>種類</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>MustHonor</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>(省略可能)。 ブール値 false、0 にする必要がある、1 または true です。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

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
<td><p><a href="autoexposure.md" data-raw-source="[&lt;strong&gt;AutoExposure&lt;/strong&gt;](autoexposure.md)"><strong>AutoExposure</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="exposuresettings.md" data-raw-source="[&lt;strong&gt;ExposureSettings&lt;/strong&gt;](exposuresettings.md)"><strong>ExposureSettings</strong></a></p></td>
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
<td><p><a href="documentfinalparameters.md" data-raw-source="[&lt;strong&gt;DocumentFinalParameters&lt;/strong&gt;](documentfinalparameters.md)"><strong>DocumentFinalParameters</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="documentparameters.md" data-raw-source="[&lt;strong&gt;DocumentParameters&lt;/strong&gt;](documentparameters.md)"><strong>DocumentParameters</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**露出**要素に含めることができます、 [ **AutoExposure** ](autoexposure.md)または[ **ExposureSettings** ](exposuresettings.md)要素が、両方は必要ありません。 **AutoExposure**デバイスする必要があります、白いイメージをドキュメントの背景を低減するイメージ処理手法を使用して自動的にことを指定します。 **ExposureSettings**特定指定**露出**WSD スキャン サービスがイメージ データの取得後に適用される調整の値。

クライアントは、省略可能な指定できます**MustHonor**属性の場合にのみ、**露出**要素に含まれる、 **CreateScanJobRequest**階層。 詳細については**MustHonor**と使用状況を参照してください[ **CreateScanJobRequest**](createscanjobrequest.md)します。

## <a name="see-also"></a>関連項目


[**AutoExposure**](autoexposure.md)

[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

[**ExposureSettings**](exposuresettings.md)

 

 






