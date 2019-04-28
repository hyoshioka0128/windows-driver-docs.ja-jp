---
title: CompressionQualityFactor 要素
description: 省略可能な CompressionQualityFactor 要素では、0 ~ 100 のスケール画質、量が理想的な整数を指定します。
ms.assetid: e66ab41d-3f77-4c60-b0bf-d050f467c6b4
keywords:
- CompressionQualityFactor 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn CompressionQualityFactor wscn MustHonor "" wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae5c6b719bab6d10143944b21870bb9e5f641787
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373189"
---
# <a name="compressionqualityfactor-element"></a>CompressionQualityFactor 要素


省略可能な**CompressionQualityFactor**要素は、0 ~ 100 のスケールで画像の品質、量が理想的な整数を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:CompressionQualityFactor wscn:MustHonor=""                               wscn:Override=""                               wscn:UsedDefault=""
  MustHonor = "xs:string"
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:CompressionQualityFactor wscn:MustHonor=""                               wscn:Override=""                               wscn:UsedDefault="">
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
<tr class="even">
<td><p><strong><strong>上書き</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>(省略可能)。 ブール値 false、0 にする必要がある、1 または true です。<strong>falsetrue</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong><strong>UsedDefault</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>(省略可能)。 ブール値 false、0 にする必要がある、1 または true です。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>テキスト値
----------

必須。 0 ~ 100 の範囲の整数。

## <a name="child-elements"></a>子要素


子要素はありません。

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

任意の非可逆圧縮の種類より高い値が高いイメージ品質ともそれに応じて大きくファイル サイズを示す、許容可能なイメージの損失の量を決定するのに整数値を使用します。 100 の値は、デバイスが、最小限の品質指定できる最大のイメージを生成するためにサポートされる圧縮を使用することを示します。 現時点では、JPEG 圧縮では、唯一サポートされている非可逆圧縮の種類です。

要求されたイメージの圧縮の種類が無損失の場合と**MustHonor**が存在しないか、 **false**、WSD スキャン サービスを無視する必要があります、 **CompressionQualityFactor**要素、100 の値を代わりに使用します。 無損失圧縮の種類の場合と**MustHonor**は**true**、WSD スキャン サービス拒否すべき、 [ **ScanTicket** ](scanticket.md)要素場合、100 以外の値を指定します。

クライアントは、省略可能な指定できます**MustHonor**属性の場合にのみ、 **CompressionQualityFactor**要素に含まれる、 **CreateScanJobRequest**階層。 詳細については**MustHonor**と使用状況を参照してください[ **CreateScanJobRequest**](createscanjobrequest.md)します。

WSD スキャン サービスを指定できます、省略可能な**オーバーライド**と**UsedDefault**属性の場合にのみ、 **CompressionQualityFactor** 内の要素が含まれています。**DocumentFinalParameters**階層。 詳細については**オーバーライド**と**UsedDefault**とその用途を参照してください[ **DocumentFinalParameters**](documentfinalparameters.md)します。

この要素に使用できる値をサブセットすることができます。

## <a name="see-also"></a>関連項目


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

 

 






