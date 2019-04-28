---
title: WIA\_IPA\_アクセス\_権限
description: WIA\_IPA\_アクセス\_RIGHTS プロパティには、WIA 項目に対するアクセス権が含まれています。
ms.assetid: 5bfa9406-2cb6-4c8b-ab25-6f8f55d941d4
keywords:
- WIA_IPA_ACCESS_RIGHTS イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPA_ACCESS_RIGHTS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3a44d58a143e5b9fbcdff241959e0bcf744ce61
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369574"
---
# <a name="wiaipaaccessrights"></a>WIA\_IPA\_アクセス\_権限


WIA\_IPA\_アクセス\_RIGHTS プロパティには、WIA 項目に対するアクセス権が含まれています。

## <span id="ddk_wia_ipa_access_rights_si"></span><span id="DDK_WIA_IPA_ACCESS_RIGHTS_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_フラグ

アクセス権:読み取り/書き込みまたは読み取り専用 (によってそのアクセス権を変更する機能を項目の)

<a name="remarks"></a>注釈
-------

*アクセス権*WIA 項目のツリー内の項目を削除するアプリケーションの機能を制御します。 WIA ミニドライバーを作成し、維持、WIA\_IPA\_アクセス\_RIGHTS プロパティ。

次の表に、WIA で有効な定数\_IPA\_アクセス\_権限。

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
<td><p>WIA_ITEM_CAN_BE_DELETED</p></td>
<td><p>この WIA 項目を削除することができます。</p></td>
</tr>
<tr class="even">
<td><p>WIA_ITEM_READ</p></td>
<td><p>アイテムへのアクセスとは、読み取り専用です。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_ITEM_WRITE</p></td>
<td><p>アイテムへのアクセスは、読み取り/書き込みです。</p></td>
</tr>
<tr class="even">
<td><p>WIA_ITEM_RD</p></td>
<td><p>WIA_ITEM_READ | WIA_ITEM_CAN_BE_DELETED</p></td>
</tr>
<tr class="odd">
<td><p>WIA_ITEM_RWD</p></td>
<td><p>WIA_ITEM_READ | WIA_ITEM_WRITE | WIA_ITEM_CAN_BE_DELETED</p></td>
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
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





