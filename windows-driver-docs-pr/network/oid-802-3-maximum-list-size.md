---
title: OID_802_3_MAXIMUM_LIST_SIZE
description: OID_802_3_MAXIMUM_LIST_SIZE
ms.assetid: e4288fb3-6bb3-415c-b150-1f258a2fa1a0
ms.date: 08/08/2017
keywords: -OID_802_3_MAXIMUM_LIST_SIZE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a2b7549db10514c21aff28c921ae079a5259761b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553753"
---
# <a name="oid8023maximumlistsize"></a>OID\_802\_3\_最大\_一覧\_サイズ





NDIS と上位のプロトコルのドライバーを使用して、OID\_802\_3\_最大\_一覧\_クエリまたは 6 バイトのマルチキャストの最大数を設定するサイズ OID 要求に対処するミニポート アダプターのマルチキャスト アドレスの一覧を保持できます。

このマルチキャスト アドレスの一覧は、ミニポート アダプターにバインドされているすべてのプロトコル ドライバーで共有されます。 プロトコル ドライバーを受信できるため、共有リソース**NDIS\_状態\_マルチキャスト\_完全**ミニポート アダプターへの応答から、 [OID\_802\_3\_マルチキャスト\_一覧](oid-802-3-multicast-list.md)リスト内の要素の数が NDIS が以前に返した OID の数より少ない場合でも、要求の設定を OID\_802\_3\_最大\_一覧\_クエリ要求のサイズの OID。

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
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_802\_3\_追加\_マルチキャスト\_アドレス](oid-802-3-add-multicast-address.md)

[OID\_802\_3\_削除\_マルチキャスト\_アドレス](oid-802-3-delete-multicast-address.md)

[OID\_802\_3\_マルチキャスト\_一覧](oid-802-3-multicast-list.md)

 

 




