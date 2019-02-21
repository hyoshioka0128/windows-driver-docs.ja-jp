---
title: WIA\_IP\_転送\_機能
description: WIA\_IP\_転送\_機能プロパティは、デバイスが親と子項目をまとめて転送できるかどうかを示します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 937e3e54-6ad3-46bb-bd00-e0812c64e539
keywords:
- WIA_IPS_TRANSFER_CAPABILITIES イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_TRANSFER_CAPABILITIES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74beb9d4cb749e5cf8fb9345fbbb4a03515701c6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529486"
---
# <a name="wiaipstransfercapabilities"></a>WIA\_IP\_転送\_機能


WIA\_IP\_転送\_機能プロパティは、デバイスが親と子項目をまとめて転送できるかどうかを示します。 WIA ミニドライバーは、作成し、このプロパティを保持します。

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

次の表は、WIA で有効な定数\_IP\_転送\_機能プロパティ

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_TRANSFER_CHILDREN_SINGLE_SCAN</p></td>
<td><p>デバイスでは、親と子項目をまとめて転送またはデバイスは、各アイテムは、各子項目の個別のスキャンを行う必要があります。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista およびそれ以降のオペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





