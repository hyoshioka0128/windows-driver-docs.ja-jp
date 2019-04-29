---
title: WIA\_IPA\_項目\_時間
description: WIA\_IPA\_項目\_時のプロパティには、イメージが最初にキャプチャされた時間が含まれています。
ms.assetid: 30e29169-7a1a-412e-858a-a467d6f1b44e
keywords:
- WIA_IPA_ITEM_TIME イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPA_ITEM_TIME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51c7ccc26e7194a9ecae08e7cb40172f5a53ac6f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388779"
---
# <a name="wiaipaitemtime"></a>WIA\_IPA\_項目\_時間


WIA\_IPA\_項目\_時のプロパティには、イメージが最初にキャプチャされた時間が含まれています。

## <span id="ddk_wia_ipa_item_time_si"></span><span id="DDK_WIA_IPA_ITEM_TIME_SI"></span>


プロパティの種類:VT\_UI2 |VT\_ベクター

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り/書き込みまたは読み取り専用

<a name="remarks"></a>注釈
-------

WIA ミニドライバーを作成し、維持、WIA\_IPA\_項目\_時のプロパティ。 このプロパティは、(これは、Microsoft Windows SDK ドキュメントで説明されている) SYSTEMTIME 構造体の形式で 8 つの WORD 値のベクターとして報告する必要があります。

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

 

 





