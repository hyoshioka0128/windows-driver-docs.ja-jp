---
title: ElementData JobElements 要素
description: 必要な ElementData 要素には、ジョブに関連するスキーマの要求に対して返されるデータが含まれています。
ms.assetid: 6d9724cd-c076-4c87-9c01-ec2c16cd2aac
keywords:
- ElementData JobElements 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ElementData Name "" Valid ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34b2dbef96920aacc59fe924cd3b73b633eeb8fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364464"
---
# <a name="elementdata-for-jobelements-element"></a>ElementData JobElements 要素


必要な**ElementData**要素には、ジョブに関連するスキーマの要求に対して返されるデータが含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ElementData Name="" Valid=""
  Name = "xs:string"
  Valid = "xs:string">
  child elements
</wscn:ElementData Name="" Valid="">
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
<td><p><strong><strong>名</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>必須。 次 QName 値: xmlns:JobStatusReturn 現在 JobStatusschema.xmlns:ScanTicketReturn ScanTicket element.xmlns:DocumentsReturn ドキュメント element.xmlns:VendorSectionGet ベンダ定義の特定のセクションのいずれかWSD スキャン サービスに拡張します。</p></td>
</tr>
<tr class="even">
<td><p><strong><strong>有効です</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>必須。 ブール値 false、0 にする必要がある、1 または true です。</p></td>
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
<td><p>ベンダー定義要素</p></td>
</tr>
<tr class="even">
<td><p><a href="documents.md" data-raw-source="[&lt;strong&gt;Documents&lt;/strong&gt;](documents.md)"><strong>ドキュメント</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanticket.md" data-raw-source="[&lt;strong&gt;ScanTicket&lt;/strong&gt;](scanticket.md)"><strong>ScanTicket</strong></a></p></td>
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
<td><p><a href="jobelements.md" data-raw-source="[&lt;strong&gt;JobElements&lt;/strong&gt;](jobelements.md)"><strong>JobElements</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

WSD スキャン サービスを返します、 **ElementData**内の要素を[ **GetJobElementsResponse** ](getjobelementsresponse.md)操作の要素。

## <a name="see-also"></a>関連項目


[**ドキュメント**](documents.md)

[**GetJobElementsResponse**](getjobelementsresponse.md)

[**JobElements**](jobelements.md)

[**JobStatus**](jobstatus.md)

[**ScanTicket**](scanticket.md)

 

 






