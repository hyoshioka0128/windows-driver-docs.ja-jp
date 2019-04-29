---
title: ImageInformation 要素
description: 必要な ImageInformation 要素には、現在検証されている ScanTicket 要素を使用したスキャンから結果として得られるイメージ データに関する情報が含まれています。
ms.assetid: 58a5dc09-07fa-4e31-93f1-7370dace3263
keywords:
- ImageInformation 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ImageInformation
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2629817079e25d5787f9be7ac64098b88f93aeed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327876"
---
# <a name="imageinformation-element"></a>ImageInformation 要素


必要な**ImageInformation**要素には使用したスキャンから結果として得られるイメージ データに関する情報が含まれています、 [ **ScanTicket** ](scanticket.md)現在の要素検証されます。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ImageInformation>
  child elements
</wscn:ImageInformation>
```

<a name="attributes"></a>属性
----------

属性はありません。

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
<td><p><a href="mediabackimageinfo.md" data-raw-source="[&lt;strong&gt;MediaBackImageInfo&lt;/strong&gt;](mediabackimageinfo.md)"><strong>MediaBackImageInfo</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="mediafrontimageinfo.md" data-raw-source="[&lt;strong&gt;MediaFrontImageInfo&lt;/strong&gt;](mediafrontimageinfo.md)"><strong>MediaFrontImageInfo</strong></a></p></td>
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
<td><p><a href="createscanjobresponse.md" data-raw-source="[&lt;strong&gt;CreateScanJobResponse&lt;/strong&gt;](createscanjobresponse.md)"><strong>CreateScanJobResponse</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="validationinfo.md" data-raw-source="[&lt;strong&gt;ValidationInfo&lt;/strong&gt;](validationinfo.md)"><strong>ValidationInfo</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

WSD スキャン サービスを返します、 **ImageInformation**要素を通じて、 [ **CreateScanJobResponse** ](createscanjobresponse.md)操作の要素。 スキャン アプリケーション内で指定されているデータを使用できます**ImageInformation**イメージ ファイル内のイメージをデコードします。

## <a name="see-also"></a>関連項目


[**CreateScanJobResponse**](createscanjobresponse.md)

[**MediaBackImageInfo**](mediabackimageinfo.md)

[**MediaFrontImageInfo**](mediafrontimageinfo.md)

[**ValidationInfo**](validationinfo.md)

 

 






