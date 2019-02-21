---
title: WIA\_IP\_マルチ\_フィード\_と小文字の区別
description: WIA\_IP\_マルチ\_フィード\_と小文字の区別のプロパティを使用して、デバイスでサポートされている最低と最高の感度間下位または上位の値に複数のフィード検出トリガーを変更します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 04AC211B-89D5-417F-9089-1E3F30E22211
keywords:
- WIA_IPS_MULTI_FEED_SENSITIVITY イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_MULTI_FEED_SENSITIVITY
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81709afe5d496b731b495d8195b1e28eb4c4df16
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556721"
---
# <a name="wiaipsmultifeedsensitivity"></a>WIA\_IP\_マルチ\_フィード\_と小文字の区別


**WIA\_IP\_マルチ\_フィード\_感度**最低と最高の感度間下位または上位の値に複数のフィードの検出のトリガーを変更するプロパティを使用デバイスでサポートされています。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

このプロパティは省略可能で、フィーダー付きのデータ ソース アイテムにのみ有効です (で表される、 [ **WIA\_IPA\_項目\_カテゴリ**](wia-ipa-item-category.md)として WIAプロパティ\_カテゴリ\_フィーダー) と[ **WIA\_IP\_マルチ\_フィード**](wia-ips-multi-feed.md) WIAだけでなく他の少なくとも1つの値でサポートされます\_マルチ\_フィード\_検出\_無効になっています。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





