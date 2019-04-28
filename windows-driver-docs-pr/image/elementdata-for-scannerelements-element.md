---
title: ElementData ScannerElements 要素
description: 必要な ElementData 要素には、スキャナーに関連するスキーマの要求に対して返されるデータが含まれています。
ms.assetid: 852a7f8a-cd87-467b-8793-8a7d7943f2a9
keywords:
- ElementData ScannerElements 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ElementData Name "" Valid ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: df93a1b4bbc408cff1de244b816cdc714a45eae9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364462"
---
# <a name="elementdata-for-scannerelements-element"></a>ElementData ScannerElements 要素


必要な**ElementData**要素には、スキャナーに関連するスキーマの要求に対して返されるデータが含まれています。

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
<p>必須。 次の QNames:xmlns:ScannerDescriptionReturn currentScannerDescription schema.xmlns:ScannerConfigurationReturn 現在 ScannerConfiguration schema.xmlns:ScannerStatusReturn 現在 ScannerStatus schema.xmlns:D のいずれかefaultScanTicketReturn 現在 DefaultScanTicket schema.xmlns:VendorSectionReturn WSD スキャン サービスにベンダー定義の拡張機能の特定のセクション。</p></td>
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
<td><p><a href="defaultscanticket.md" data-raw-source="[&lt;strong&gt;DefaultScanTicket&lt;/strong&gt;](defaultscanticket.md)"><strong>DefaultScanTicket</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scannerconfiguration.md" data-raw-source="[&lt;strong&gt;ScannerConfiguration&lt;/strong&gt;](scannerconfiguration.md)"><strong>ScannerConfiguration</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scannerdescription.md" data-raw-source="[&lt;strong&gt;ScannerDescription&lt;/strong&gt;](scannerdescription.md)"><strong>ScannerDescription</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scannerstatus.md" data-raw-source="[&lt;strong&gt;ScannerStatus&lt;/strong&gt;](scannerstatus.md)"><strong>ScannerStatus</strong></a></p></td>
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
<td><p><a href="scannerelements.md" data-raw-source="[&lt;strong&gt;ScannerElements&lt;/strong&gt;](scannerelements.md)"><strong>ScannerElements</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

クライアントが呼び出す[ **GetScannerElementsRequest** ](getscannerelementsrequest.md)スキャナーに関連する要素の値を決定します。 WSD スキャン サービスには、この情報が返されます、 **ElementData**要素を通じて、 [ **GetScannerElementsResponse** ](getscannerelementsresponse.md)操作。

値は、QName、**名前**属性は、クライアントが情報を要求する対象の WSD スキャン サービス内で最上位レベルのセクションを表すスキーマ キーワードである必要があります。 スキャン サービスには、名前空間プレフィックスと、コロンで区切られた有効な要素名の両方を指定する必要があります。

**有効**属性では、クライアントによって提供されるスキーマのキーワードが有効かどうかを示します。 WSD スキャン サービスでは、この属性を設定**true**にそのスキーマの有効なセクションに、要求されたスキーマのキーワードをマップできる場合は、それ以外の場合、設定がありますこの属性**false**します。

## <a name="see-also"></a>関連項目


[**DefaultScanTicket**](defaultscanticket.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**GetScannerElementsResponse**](getscannerelementsresponse.md)

[**ScannerConfiguration**](scannerconfiguration.md)

[**ScannerDescription**](scannerdescription.md)

[**ScannerElements**](scannerelements.md)

[**ScannerStatus**](scannerstatus.md)

 

 






