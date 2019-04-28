---
title: ScanData 要素
description: 必要な ScanData 要素には、スキャンした画像を表すバイナリ データが含まれています。
ms.assetid: 9b29224c-b1e1-4c64-8a4a-476f9d6eea45
keywords:
- ScanData 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScanData
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cffda2d8858992c2a73fbaeaa1d4dee1e2346a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364390"
---
# <a name="scandata-element"></a>ScanData 要素


必要な**ScanData**要素には、スキャンした画像を表すバイナリ データが含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScanData/>
```

<a name="attributes"></a>属性
----------

属性はありません。

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
<td><p><a href="retrieveimageresponse.md" data-raw-source="[&lt;strong&gt;RetrieveImageResponse&lt;/strong&gt;](retrieveimageresponse.md)"><strong>RetrieveImageResponse</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**ScanData**要素が含まれています、 **xop: 含める**基準とした、SOAP エンベロープ/本文のスキャン データの場所を指定する要素を[ **RetrieveImageResponse** ](retrieveimageresponse.md)操作の要素。 実際のスキャン データは、バイナリの添付ファイルとして SOAP エンベロープと本文には追加されます。

## <a name="see-also"></a>関連項目


[**RetrieveImageResponse**](retrieveimageresponse.md)

 

 






