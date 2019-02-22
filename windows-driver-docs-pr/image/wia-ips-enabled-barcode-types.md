---
title: WIA\_IP\_有効\_バーコード\_型
description: WIA\_IP\_有効\_バーコード\_型のプロパティは、現在のセッションでバー コード リーダーは検索を有効になっているバーコードの選択に使用します。
ms.assetid: 7CB9FE6D-5E22-48ED-B948-01CC906CA46D
keywords:
- WIA_IPS_ENABLED_BARCODE_TYPES イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_ENABLED_BARCODE_TYPES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1aba889669e07288e39425e96ddb00caa31ac378
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553232"
---
# <a name="wiaipsenabledbarcodetypes"></a>WIA\_IP\_有効\_バーコード\_型


**WIA\_IP\_有効\_バーコード\_型**プロパティを使用して、現在のセッションでバー コード リーダーは検索を有効になっているバーコードを選択します。 バーコードは、一部またはすべての値の WIA ミニドライバーを報告する[ **WIA\_IP\_サポートされている\_バーコード\_型**](wia-ips-supported-barcode-types.md)します。 配列内の値の順序では、それぞれのバーコードが検索対象の優先順位を指定します。




プロパティの種類:VT\_I4 |VT\_ベクター

有効な値 :WIA\_PROP\_NONE (1 つの 'array'/値のベクトル)

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

有効な値、 **WIA\_IP\_有効\_バーコード\_型**プロパティには同じ WIA\_バーコード\_に対して定義されている値[**WIA\_IP\_サポートされている\_バーコード\_型**](wia-ips-supported-barcode-types.md)プロパティ。

このプロパティは、バーコード リーダーのすべての項目に必要です。

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

 

 





