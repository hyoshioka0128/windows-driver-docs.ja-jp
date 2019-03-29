---
title: 指定の要素
description: 省略可能な指定の要素では、スキャン デバイスを元のドキュメントのソースを指定します。
ms.assetid: a49ed5d8-6d49-4997-9704-de1cd6c7d0c7
keywords:
- 指定要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn InputSource wscn MustHonor "" wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 868b76d778ef1860c8a35e4a04751ae2548078d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581903"
---
# <a name="inputsource-element"></a>指定の要素


省略可能な**指定**要素は、スキャン デバイスで、元のドキュメントのソースを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:InputSource wscn:MustHonor=""                  wscn:Override=""                  wscn:UsedDefault=""
  MustHonor = "xs:string"
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:InputSource wscn:MustHonor=""                  wscn:Override=""                  wscn:UsedDefault="">
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

必須。 次のいずれかの値です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>項目</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="ADF"></span><span id="adf"></span>ADF</p></td>
<td><p>ドキュメントは、供給デバイス、前面にある各ページののみをスキャンするためのドキュメントを配信する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><span id="ADFDuplex"></span><span id="adfduplex"></span><span id="ADFDUPLEX"></span>ADFDuplex</p></td>
<td><p>ドキュメントは、供給デバイス、各ページの両方の側をスキャンするためのドキュメントを配信する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Film"></span><span id="film"></span><span id="FILM"></span>フィルム</p></td>
<td><p>スキャン オプション フィルムを使用して、ドキュメントをスキャンする必要があります。</p></td>
</tr>
<tr class="even">
<td><p><span id="Platen"></span><span id="platen"></span><span id="PLATEN"></span>プラテン</p></td>
<td><p>スキャナー プラテンからドキュメントをスキャンする必要があります。</p></td>
</tr>
</tbody>
</table>

 

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

クライアントは、省略可能な指定できます**MustHonor**属性の場合にのみ、**指定**要素に含まれる、 **CreateScanJobRequest**階層。 詳細については**MustHonor**と使用状況を参照してください[ **CreateScanJobRequest**](createscanjobrequest.md)します。

WSD スキャン サービスを指定できます、省略可能な**オーバーライド**と**UsedDefault**属性の場合にのみ、**指定**要素に含まれる、 **DocumentFinalParameters**階層。 詳細については**オーバーライド**と**UsedDefault**とその用途を参照してください[ **DocumentFinalParameters**](documentfinalparameters.md)します。

両方を拡張して一部この要素に使用できる値。

## <a name="see-also"></a>関連項目


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

 

 






