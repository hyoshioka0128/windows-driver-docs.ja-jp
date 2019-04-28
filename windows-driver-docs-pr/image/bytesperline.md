---
title: BytesPerLine 要素
description: 必要な BytesPerLine 要素では、結果のイメージ ファイルにスキャン ラインあたりのバイト数を指定します。
ms.assetid: 026187db-16b7-48fc-a9e4-fa32cdc73d98
keywords:
- BytesPerLine 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn BytesPerLine
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a80f6388de8c74bf8c66b8ac7b2d8329c4f2d4f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373305"
---
# <a name="bytesperline-element"></a>BytesPerLine 要素


必要な**BytesPerLine**要素は、スキャン ラインあたりのバイト数を結果のイメージ ファイルを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:BytesPerLine>
  text
</wscn:BytesPerLine>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 0 ~ 2147483647 の整数値。

## <a name="child-elements"></a>子要素


子要素はありません。

## <a name="parent-elements"></a>親要素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mediabackimageinfo.md" data-raw-source="[&lt;strong&gt;MediaBackImageInfo&lt;/strong&gt;](mediabackimageinfo.md)"><strong>MediaBackImageInfo</strong></a></p></td>
<td><p></p>
<p>MediaBackImageInfo</p></td>
</tr>
<tr class="even">
<td><p><a href="mediafrontimageinfo.md" data-raw-source="[&lt;strong&gt;MediaFrontImageInfo&lt;/strong&gt;](mediafrontimageinfo.md)"><strong>MediaFrontImageInfo</strong></a></p></td>
<td><p></p>
<p>MediaFrontImageInfo</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

WSD スキャン サービスが返す整数値は、データのピクセルと各スキャン ラインにスキャナーを追加する埋め込みの両方に必要な合計バイト数です。

[**書式設定**](format.md)

**BytesPerLine**要素が有効な場合にのみ、要求された[**形式**](format.md)値は、圧縮されていないファイル形式。 ファイル形式に圧縮が示されている場合、スキャン サービスがゼロの値を返す必要があります**BytesPerLine**します。

## <a name="see-also"></a>関連項目


[**書式設定**](format.md)

[**MediaBackImageInfo**](mediabackimageinfo.md)

[**MediaFrontImageInfo**](mediafrontimageinfo.md)

 

 






