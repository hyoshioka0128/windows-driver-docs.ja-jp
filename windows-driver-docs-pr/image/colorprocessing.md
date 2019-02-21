---
title: ColorProcessing 要素
description: 省略可能な ColorProcessing 要素は、スキャナーの入力ソースのカラー処理モードを指定します。
ms.assetid: 10170090-d0d2-44b1-bd0d-3b800669f7cf
keywords:
- ColorProcessing 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ColorProcessing wscn MustHonor "" wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f1775e893213420118465aa11df7240c56177c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539718"
---
# <a name="colorprocessing-element"></a>ColorProcessing 要素


省略可能な**ColorProcessing**要素は、スキャナーの入力ソースのカラー処理モードを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ColorProcessing wscn:MustHonor=""                      wscn:Override=""                      wscn:UsedDefault=""
  MustHonor = "xs:string"
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:ColorProcessing wscn:MustHonor=""                      wscn:Override=""                      wscn:UsedDefault="">
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

一覧と処理モードの色の説明では、ColorEntry を参照してください。[ **ColorEntry**](colorentry.md)

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
<td><p><a href="mediafront.md" data-raw-source="[&lt;strong&gt;MediaFront&lt;/strong&gt;](mediafront.md)"><strong>MediaFront</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

クライアントは、省略可能な指定できます**MustHonor**属性の場合にのみ、 **ColorProcessing**要素に含まれる、 [ **CreateScanJobRequest**](createscanjobrequest.md)階層。 詳細については**MustHonor**と使用状況を参照してください**CreateScanJobRequest**します。

WSD スキャン サービスを指定できます、省略可能な**オーバーライド**と**UsedDefault**属性の場合にのみ、 **ColorProcessing**要素に含まれる、 [**DocumentFinalParameters** ](documentfinalparameters.md)階層。 詳細については**オーバーライド**と**UsedDefault**とその用途を参照してください**DocumentFinalParameters**します。

## <a name="see-also"></a>関連項目


[**ColorEntry**](colorentry.md)

[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**MediaFront**](mediafront.md)

 

 






