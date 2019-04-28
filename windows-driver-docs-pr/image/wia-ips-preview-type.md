---
title: WIA\_IP\_プレビュー\_型
description: WIA\_IP\_プレビュー\_TYPE プロパティは、場合ことを示します。 WIA\_IPA\_データ型および WIA\_IPA\_新しいプレビューのスキャンを要求することなくの深さを変更します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 2d4f1052-da7a-404e-b462-9a7c2e2caf80
keywords:
- WIA_IPS_PREVIEW_TYPE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PREVIEW_TYPE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 437810cba29f462a053a8e648ae5dbedb3afa999
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366789"
---
# <a name="wiaipspreviewtype"></a>WIA\_IP\_プレビュー\_型


WIA\_IP\_プレビュー\_TYPE プロパティを示す場合[ **WIA\_IPA\_DATATYPE** ](wia-ipa-datatype.md)と[ **WIA\_IPA\_深さ**](wia-ipa-depth.md)新しいプレビューのスキャンを要求することがなく変更されます。 WIA ミニドライバーは、作成し、このプロパティを保持します。

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

次の表は、WIA で有効な定数\_IP\_プレビュー\_型プロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_ADVANCED_PREVIEW</p></td>
<td><p>ライブ プレビューの更新はサポートされてください。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BASIC_PREVIEW</p></td>
<td><p>プレビュー イメージは、新しいプレビュー スキャンでのみ更新できます。</p></td>
</tr>
</tbody>
</table>

 

**注**   WIA\_IP\_プレビュー\_型を記述する必要がありますのみ、 [ **WIA\_IPA\_DATATYPE** ](wia-ipa-datatype.md)と[ **WIA\_IPA\_深さ**](wia-ipa-depth.md)プロパティ。

 

<a name="requirements"></a>必要条件
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

## <a name="see-also"></a>関連項目


[**WIA\_IPA\_データ型**](wia-ipa-datatype.md)

[**WIA\_IPA\_深さ**](wia-ipa-depth.md)

 

 






