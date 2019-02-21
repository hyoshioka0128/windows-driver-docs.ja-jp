---
title: NumberOfLines 要素
description: 必要な NumberOfLines 要素には、最終的な出力の画像のピクセルで高さがについて説明します。
ms.assetid: 9f7f96d4-fd88-4d14-b000-7abefe96775f
keywords:
- NumberOfLines 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn NumberOfLines
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 519cacdacbfc62c1c8bbb7be60111b5ddb47d53a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550716"
---
# <a name="numberoflines-element"></a>NumberOfLines 要素


必要な**NumberOfLines**要素には、最終的な出力の画像のピクセルで高さがについて説明します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:NumberOfLines>
  text
</wscn:NumberOfLines>
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

指定した値には、正確な高さ (ピクセル単位) または現在の生成と最終的な出力イメージの行の数がについて説明します[ **ScanTicket** ](scanticket.md)設定が検証されています。 この高さには、回転と調整をクライアントに転送する前に、スキャンしたイメージでスキャナーが実行可能性がありますが含まれます。

## <a name="see-also"></a>関連項目


[**MediaBackImageInfo**](mediabackimageinfo.md)

[**MediaFrontImageInfo**](mediafrontimageinfo.md)

[**ScanTicket**](scanticket.md)

 

 






