---
title: PixelsPerLine 要素
description: 必要な PixelsPerLine 要素には、最終的な出力画像のピクセル単位で正確な幅がについて説明します。
ms.assetid: aad46ca7-025e-4f50-9bc5-7f584a7bf684
keywords:
- PixelsPerLine 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn PixelsPerLine
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: beb284b4f16157c775febd4ede0838f122f43f81
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375852"
---
# <a name="pixelsperline-element"></a>PixelsPerLine 要素


必要な**PixelsPerLine**要素には、最終的な出力画像のピクセル単位で正確な幅がについて説明します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:PixelsPerLine>
  text
</wscn:PixelsPerLine>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 1 ~ 2,147, 483,647 の範囲内で整数値。

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
<td><p><a href="mediabackimageinfo.md" data-raw-source="[&lt;strong&gt;MediaBackImageInfo&lt;/strong&gt;](mediabackimageinfo.md)"><strong>MediaBackImageInfo</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="mediafrontimageinfo.md" data-raw-source="[&lt;strong&gt;MediaFrontImageInfo&lt;/strong&gt;](mediafrontimageinfo.md)"><strong>MediaFrontImageInfo</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

指定した値には、現在を使用して生成される最終的な出力画像のピクセル単位で正確な幅がについて説明します[ **ScanTicket** ](scanticket.md)設定が検証されています。 この幅には、回転と調整をクライアントに転送する前に、スキャンしたイメージでスキャナーが実行可能性がありますが含まれます。

## <a name="see-also"></a>関連項目


[**MediaBackImageInfo**](mediabackimageinfo.md)

[**MediaFrontImageInfo**](mediafrontimageinfo.md)

[**ScanTicket**](scanticket.md)

 

 






