---
title: ScannerDescription 要素
description: ScannerDescription 要素
ms.assetid: 4429702e-18de-4b7c-83a2-ac405517e730
keywords:
- ScannerDescription 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScannerDescription
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbc371b4b0eb3b8f923f3dda3837ee9321685e73
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561106"
---
# <a name="scannerdescription-element"></a>ScannerDescription 要素


<a name="usage"></a>使用方法
-----

```xml
<wscn:ScannerDescription>
  child elements
</wscn:ScannerDescription>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

なし

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
<td><p><a href="scannerinfo.md" data-raw-source="[&lt;strong&gt;ScannerInfo&lt;/strong&gt;](scannerinfo.md)"><strong>ScannerInfo</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scannerlocation.md" data-raw-source="[&lt;strong&gt;ScannerLocation&lt;/strong&gt;](scannerlocation.md)"><strong>ScannerLocation</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scannername.md" data-raw-source="[&lt;strong&gt;ScannerName&lt;/strong&gt;](scannername.md)"><strong>ScannerName</strong></a></p></td>
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
<td><p><a href="elementchanges.md" data-raw-source="[&lt;strong&gt;ElementChanges&lt;/strong&gt;](elementchanges.md)"><strong>ElementChanges</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="elementdata-for-scannerelements-element.md" data-raw-source="[&lt;strong&gt;ElementData for parent ScannerElements&lt;/strong&gt;](elementdata-for-scannerelements-element.md)"><strong>親 ScannerElements ElementData</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

**ScannerDescription**要素には、スキャナーをほとんどまたはまったく変更に関する情報が含まれています。 クライアントが呼び出すことでこの情報を取得、 [ **GetScannerElementsRequest** ](getscannerelementsrequest.md)操作の要素。

## <a name="see-also"></a>関連項目


[**ElementChanges**](elementchanges.md)

[**親 ScannerElements ElementData**](elementdata-for-scannerelements-element.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**ScannerInfo**](scannerinfo.md)

[**ScannerLocation**](scannerlocation.md)

[**ScannerName**](scannername.md)

 

 






