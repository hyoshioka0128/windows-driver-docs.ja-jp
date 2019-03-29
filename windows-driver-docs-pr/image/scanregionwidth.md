---
title: ScanRegionWidth 要素
description: 必要な ScanRegionWidth 要素では、高速スキャン方向にスキャン領域の幅を指定します。
ms.assetid: 3fe1933c-f086-453d-a8bd-84903929ed28
keywords:
- ScanRegionWidth 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScanRegionWidth wscn MustHonor "" wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdf72c017619145ae19e7396b16c1cf25f2442e6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572087"
---
# <a name="scanregionwidth-element"></a>ScanRegionWidth 要素


必要な**ScanRegionWidth**要素は、スキャンの領域の幅を高速スキャン方向を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScanRegionWidth wscn:MustHonor=""                      wscn:Override=""                      wscn:UsedDefault=""
  MustHonor = "xs:string"
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:ScanRegionWidth wscn:MustHonor=""                      wscn:Override=""                      wscn:UsedDefault="">
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

必須。 1 ~ InputMediaSize 高さの整数。[ **InputMediaSize**](inputmediasize.md)

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
<td><p><a href="scanregion.md" data-raw-source="[&lt;strong&gt;ScanRegion&lt;/strong&gt;](scanregion.md)"><strong>ScanRegion</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>コメント
-------

スキャンの地域のパラメーターの詳細については、次を参照してください。 [ **ScanRegion**](scanregion.md)します。

クライアントは、省略可能な指定できます**MustHonor**属性の場合にのみ、 **ScanRegionWidth**要素に含まれる、 **CreateScanJobRequest**階層。 詳細については**MustHonor**と使用状況を参照してください[ **CreateScanJobRequest**](createscanjobrequest.md)します。

WSD スキャン サービスを指定できます、省略可能な**オーバーライド**と**UsedDefault**属性の場合にのみ、 **ScanRegionWidth**要素に含まれる、 **DocumentFinalParameters**階層。 詳細については**オーバーライド**と**UsedDefault**とその用途を参照してください[ **DocumentFinalParameters**](documentfinalparameters.md)します。

## <a name="see-also"></a>関連項目


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**InputMediaSize**](inputmediasize.md)

[**ScanRegion**](scanregion.md)

[**ScanRegionHeight**](scanregionheight.md)

 

 






