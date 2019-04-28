---
title: ContentType 要素
description: 省略可能な ContentType 要素には、元のドキュメントの主な特徴を指定します。
ms.assetid: 0e91e4ec-5569-452f-b929-9d2923f3147d
keywords:
- ContentType 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ContentType wscn MustHonor "" wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 716d82d6fdfae30d3be268f50c5620954837697d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368566"
---
# <a name="contenttype-element"></a>ContentType 要素


省略可能な**ContentType**要素は、元のドキュメントの主な特徴を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ContentType wscn:MustHonor=""                  wscn:Override=""                  wscn:UsedDefault=""
  MustHonor = "xs:string"
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:ContentType wscn:MustHonor=""                  wscn:Override=""                  wscn:UsedDefault="">
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
<p>任意。 ブール値 false、0 にする必要がある、1 または true です。</p></td>
</tr>
<tr class="even">
<td><p><strong><strong>上書き</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>(省略可能)。 ブール値 false、0 にする必要がある、1 または true です。</p></td>
</tr>
<tr class="odd">
<td><p><strong><strong>UsedDefault</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>任意。 ブール値 false、0 にする必要がある、1 または true です。</p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>テキスト値
----------

必須。 次のいずれかの値です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>用語</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="Auto"></span><span id="auto"></span><span id="AUTO"></span>自動</p></td>
<td><p>デバイスのスキャンでは、元の型を自動的に検出されます。</p></td>
</tr>
<tr class="even">
<td><p><span id="Text"></span><span id="text"></span><span id="TEXT"></span>テキスト</p></td>
<td><p>ドキュメントは主に、バック グラウンドで厳密には対照的です。 個別のテキストで構成されます。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Photo"></span><span id="photo"></span><span id="PHOTO"></span>写真</p></td>
<td><p>元は主に、写真の画像、階調が段階的に変更して、エッジは個別ではない場所で構成されます。</p></td>
</tr>
<tr class="even">
<td><p><span id="Halftone"></span><span id="halftone"></span><span id="HALFTONE"></span>ハーフトーン</p></td>
<td><p>元は主に、ハーフトーン イメージで構成されます。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Mixed"></span><span id="mixed"></span><span id="MIXED"></span>混合</p></td>
<td><p>1 つ以上特定 DocumentType の特性を持つマルチページ ドキュメントです。</p></td>
</tr>
</tbody>
</table>

 

両方を拡張して、この要素の値のサブセット。

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

クライアントは、省略可能な指定できます**MustHonor**属性の場合にのみ、 **ContentType**要素に含まれる、 **CreateScanJobRequest**階層。 詳細については**MustHonor**と使用状況を参照してください[ **CreateScanJobRequest**](createscanjobrequest.md)します。

WSD スキャン サービスを指定できます、省略可能な**オーバーライド**と**UsedDefault**属性の場合にのみ、 **ContentType**要素に含まれる、 **DocumentFinalParameters**階層。 詳細については**オーバーライド**と**UsedDefault**とその用途を参照してください[ **DocumentFinalParameters**](documentfinalparameters.md)します。

## <a name="see-also"></a>関連項目


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

 

 






