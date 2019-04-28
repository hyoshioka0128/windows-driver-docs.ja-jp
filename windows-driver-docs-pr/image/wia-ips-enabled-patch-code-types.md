---
title: WIA\_IP\_有効\_PATCH\_コード\_型
description: WIA\_IP\_有効\_PATCH\_コード\_型のプロパティを使用して、修正プログラム コード リーダーは 現在のセッションで検索が有効な修正プログラム コードを選択します。
ms.assetid: 278C93EF-661E-41B2-8882-DF05A2FB9723
keywords:
- WIA_IPS_ENABLED_PATCH_CODE_TYPES イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_ENABLED_PATCH_CODE_TYPES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89e9612720111b0c14109bb880dbb8ddd5c94355
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370688"
---
# <a name="wiaipsenabledpatchcodetypes"></a>WIA\_IP\_有効\_PATCH\_コード\_型


**WIA\_IP\_有効\_PATCH\_コード\_型**プロパティを使用して、修正プログラム コード リーダーは 現在の検索が有効な修正プログラム コードを選択します。セッションです。 これらの修正プログラム コードで一部またはすべて、値の WIA ミニドライバーを報告する[ **WIA\_IP\_サポートされている\_パッチ\_コード\_型**](wia-ips-supported-patch-code-types.md). 配列内の値の順序では、それぞれの修正プログラム コードが検索対象の優先順位を指定します。




プロパティの種類:VT\_I4 |VT\_ベクター

有効な値 :WIA\_PROP\_NONE (1 つの 'array'/値のベクトル)

アクセス権:[読み取り/書き込み]

<a name="remarks"></a>注釈
-------

有効な値、 **WIA\_IP\_有効\_PATCH\_コード\_型**プロパティには同じ WIA\_修正プログラムを適用\_コード\_に対して定義されている値、 [ **WIA\_IP\_サポートされている\_PATCH\_コード\_型**](wia-ips-supported-patch-code-types.md)プロパティ。

このプロパティは、修正プログラム コード リーダーのすべての項目に必要です。

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

 

 





