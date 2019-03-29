---
title: 回転要素
description: 省略可能な回転要素には、スキャンしたドキュメントの各イメージを回転する量を指定します。
ms.assetid: df12cd79-7c3e-4be5-9d7c-237ec014e9c1
keywords:
- デバイスのイメージの回転要素
topic_type:
- apiref
api_name:
- wscn Rotation wscn MustHonor "" wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcc9c81fd9830486dab1d9fdeced1fcc9705e117
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575113"
---
# <a name="rotation-element"></a>回転要素


省略可能な**回転**要素は、スキャンしたドキュメントの各イメージを回転する量を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:Rotation wscn:MustHonor=""               wscn:Override=""               wscn:UsedDefault=""
  MustHonor = "xs:string"
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:Rotation wscn:MustHonor=""               wscn:Override=""               wscn:UsedDefault="">
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
<th>型</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>MustHonor</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>いいえ</p></td>
<td><p></p>
<p>任意。 ブール値 false、0 にする必要がある、1 または true です。<strong>falsetrue</strong></p></td>
</tr>
<tr class="even">
<td><p><strong><strong>上書き</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>いいえ</p></td>
<td><p></p>
<p>任意。 ブール値 false、0 にする必要がある、1 または true です。<strong>falsetrue</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong><strong>UsedDefault</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>いいえ</p></td>
<td><p></p>
<p>任意。 ブール値 false、0 にする必要がある、1 または true です。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>テキスト値
----------

必須。 0、90、180、または 270 の 1 つ。

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

<a name="remarks"></a>コメント
-------

整数値、**回転**要素は、スキャンしたドキュメントの各イメージに適用する時計回りの回転を指定します。 すべての WSD スキャン サービスには、値 0 (つまり、回転なし) をサポートする必要があります。

クライアントは、省略可能な指定できます**MustHonor**属性の場合にのみ、**回転**要素に含まれる、 **CreateScanJobRequest**階層。 詳細については**MustHonor**と使用状況を参照してください[ **CreateScanJobRequest**](createscanjobrequest.md)します。

WSD スキャン サービスを指定できます、省略可能な**オーバーライド**と**UsedDefault**属性の場合にのみ、**回転**要素に含まれる、 **DocumentFinalParameters**階層。 詳細については**オーバーライド**と**UsedDefault**とその用途を参照してください[ **DocumentFinalParameters**](documentfinalparameters.md)します。

## <a name="see-also"></a>関連項目


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

 

 






