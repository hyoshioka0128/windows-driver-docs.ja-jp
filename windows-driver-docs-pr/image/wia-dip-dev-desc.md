---
title: WIA\_DIP\_DEV\_DESC
description: WIA\_DIP\_DEV\_DESC プロパティには、WIA ミニドライバーのデバイスの説明文字列が含まれています。 WIA サービスは、作成し、このプロパティを保持します。
ms.assetid: ce10deb8-7f33-45da-8a0e-cdcd7bf08ff9
keywords:
- WIA_DIP_DEV_DESC イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DIP_DEV_DESC
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71886dc4750c1abc612f0046cfa5b21c6fe3e871
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537688"
---
# <a name="wiadipdevdesc"></a>WIA\_DIP\_DEV\_DESC


WIA\_DIP\_DEV\_DESC プロパティには、WIA ミニドライバーのデバイスの説明文字列が含まれています。 WIA サービスは、作成し、このプロパティを保持します。

## <span id="ddk_wia_dip_dev_desc_si"></span><span id="DDK_WIA_DIP_DEV_DESC_SI"></span>


プロパティの種類:VT\_BSTR

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

デバイスの説明の文字列を WIA\_DIP\_DEV\_DESC プロパティが含まれています、ドライバーの INF ファイルから取得されます。 アプリケーションでは、デバイスの説明を取得するには、このプロパティを読み取ります。

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

 

 





