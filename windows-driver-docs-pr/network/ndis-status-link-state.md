---
title: NDIS_STATUS_LINK_STATE
description: ミニポート ドライバーでは、中規模の物理的な特性の変更されたが NDIS と関連付けたドライバーに通知するのに、NDIS_STATUS_LINK_STATE 状態を示す値を使用します。
ms.assetid: e9953fe5-68d2-47e5-aceb-b35289500262
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_LINK_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a2075a3c8677481c81fd7b9444eadda22c3f94db
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368581"
---
# <a name="ndisstatuslinkstate"></a>NDIS\_状態\_リンク\_状態


ミニポート ドライバーを使用して、NDIS\_状態\_リンク\_状態の状態表示にされていると、メディアの物理的な特性の変更の NDIS と関連付けたドライバーを通知します。

<a name="remarks"></a>注釈
-------

後続のドライバーを使用する必要があります、 [OID\_GEN\_リンク\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-state)リンクの状態を判断する OID。 代わりに、使用して、NDIS\_状態\_リンク\_リンク状態の更新の状態の状態の表示。

**StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造に含まれる、 [ **NDIS\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)構造体。 この構造体には、メディアの物理的な状態を指定します。

ミニポート ドライバーでは、NDIS が送信されないようにする必要があります\_状態\_リンク\_状態の状態の表示がないメディアの物理的な状態が変更された場合。 ただし、この状態表示の回避は、要件ではありません。

NDIS 6.0 とそれ以降のミニポート ドライバーでの接続の状態を示す必要がありますミニポート アダプターは、低電力状態に遷移を場合**MediaConnectStateUnknown**します。 ミニポート アダプタの遷移は、作業の電源状態に戻す、ときに、ミニポート ドライバーがの状態を示す必要があります**MediaConnectStateConnected**のリンクを再確立された後です。 NDIS 6.30 ミニポート ドライバーを示す必要があります**MediaConnectStateUnknown**低電力の中に、ウェイク アップ オプションを選択し、リンクの変更を中断する場合にのみの移行が無効になります。 つまり、ミニポート ドライバーが接続状態を示す必要があります**MediaConnectStateUnknown**を検出し、低電力状態からの接続状態の変更にスリープ解除することができない場合、低電力遷移中にします。

以前指定したリンクの状態で指定されたリンクの状態の変更がない場合、NDIS が、状態の表示を上にあるドライバーに渡さない場合があります。 ただし、この動作は保証されません。 この状態を示す値を受け取るドライバーが重なって、メディアの特性が存在する場合がある変更を決定する必要があります。

上にあるドライバーが、NDIS 5 の場合は。*x*または以前のプロトコル ドライバーでは、NDIS 変換、NDIS\_状態\_リンク\_に適切な NDIS 5.1 状態インジケーターの状態の状態表示。 NDIS とリンク速度の変更を示す、 [ **NDIS\_状態\_リンク\_速度\_変更**](ndis-status-link-speed-change.md)状態を示す値。 接続状態で変更を示し、NDIS [ **NDIS\_状態\_メディア\_CONNECT** ](ndis-status-media-connect.md)と[ **NDIS\_状態\_メディア\_切断**](ndis-status-media-disconnect.md)状態インジケーター。

NDIS は、NDIS 5 も変換します。*x* NDIS 6.0 とそれ以降のドライバーを後続のミニポート ドライバーの状態。 状態インジケーターを使用する NDIS またはメディアの状態は、NDIS 5 で識別されるその NDIS を変更します。*x* NDIS を作成するクエリは OID\_状態\_リンク\_状態インジケーターの状態。 NDIS は、次の変換を実行します。

-   [ **NDIS\_状態\_メディア\_CONNECT** ](ndis-status-media-connect.md)に状態を示す値が変換された**MediaConnectStateConnected**で、[ **NDIS\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)構造体。

-   [ **NDIS\_状態\_メディア\_切断**](ndis-status-media-disconnect.md)に状態を示す値が変換された**MediaConnectStateDisconnected**[ **NDIS\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)構造体。

-   [ **NDIS\_状態\_リンク\_速度\_変更**](ndis-status-link-speed-change.md)状態を示す値、および[OID\_GEN\_リンク\_速度](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed)OID を使用して、リンク速度の状態を生成します。

リンクのステータスの詳細については、次を参照してください。 [OID\_GEN\_リンク\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-state)します。

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
<td><p>NDIS 6.0 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)

[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_状態\_リンク\_速度\_変更**](ndis-status-link-speed-change.md)

[**NDIS\_状態\_メディア\_接続**](ndis-status-media-connect.md)

[**NDIS\_状態\_メディア\_切断**](ndis-status-media-disconnect.md)

[OID\_GEN\_リンク\_速度](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed)

[OID\_GEN\_リンク\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-state)

 

 




