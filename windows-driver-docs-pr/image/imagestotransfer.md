---
title: ImagesToTransfer 要素
description: 省略可能な ImagesToTransfer 要素には、現在のジョブをスキャンするイメージの数を指定します。
ms.assetid: d3f06104-17a5-41e4-ab80-1228ee342b7d
keywords:
- ImagesToTransfer 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ImagesToTransfer wscn MustHonor "" wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ae87936af242793afcd036876a1a33700edf3bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530043"
---
# <a name="imagestotransfer-element"></a>ImagesToTransfer 要素


省略可能な**ImagesToTransfer**要素を現在のジョブをスキャンするイメージの数を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ImagesToTransfer wscn:MustHonor=""                       wscn:Override=""                       wscn:UsedDefault=""
  MustHonor = "xs:string"
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:ImagesToTransfer wscn:MustHonor=""                       wscn:Override=""                       wscn:UsedDefault="">
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

必須。 0 ~ 2147483648 範囲の整数。

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

**ImagesToTransfer**値は、デバイスのスキャンがあるメディアの現在のジョブよりもより多くのページを含むことのできるドキュメント フィーダー場合に便利です。

デバイスがで指定されている選択した入力ソースに使用できるは複数のページをスキャンして、値が 0 の場合、 [**指定**](inputsource.md)要素。 入力ソースがある場合**プラテン**または**フィルム**、値の 0 に**ImagesToTransfer** 1 つのイメージの取得が生成されます。 入力ソースがある場合**ADF**または**ADFDuplex**、値の 0 に**ImagesToTransfer**フィーダーが空になるまで、そのデバイスでイメージを取得する必要がありますを示します。

デバイスがからイメージを獲得する場合**ADFDuplex**メディアの各側が 1 つのイメージを表します。 奇数の値が指定されている場合**ADFDuplex**デバイスは、メディアの最後のシートの前面にあるのみを取得します。

クライアントは、省略可能な指定できます**MustHonor**属性の場合にのみ、 **ImagesToTransfer**要素に含まれる、 **CreateScanJobRequest**階層。 詳細については**MustHonor**と使用状況を参照してください[ **CreateScanJobRequest**](createscanjobrequest.md)します。

WSD スキャン サービスを指定できます、省略可能な**オーバーライド**と**UsedDefault**属性の場合にのみ、 **ImagesToTransfer** 内の要素が含まれている**DocumentFinalParameters**階層。 詳細については**オーバーライド**と**UsedDefault**とその用途を参照してください[ **DocumentFinalParameters**](documentfinalparameters.md)します。

## <a name="see-also"></a>関連項目


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

[**指定**](inputsource.md)

 

 






