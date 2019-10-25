---
title: NDIS_STATUS_LINK_STATE
description: ミニポートドライバーは、NDIS_STATUS_LINK_STATE 状態表示を使用して、媒体の物理的な特性が変更されたことを NDIS およびそれ以降のドライバーに通知します。
ms.assetid: e9953fe5-68d2-47e5-aceb-b35289500262
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_LINK_STATE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: bb4d62f542128b80a59a377e3856dcc8f08ba891
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844206"
---
# <a name="ndis_status_link_state"></a>NDIS\_状態\_リンク\_状態


ミニポートドライバーは、NDIS\_の状態\_リンク\_状態の状態の表示を使用して、媒体の物理的な特性が変更されたことを NDIS およびそれ以降のドライバーに通知します。

<a name="remarks"></a>注釈
-------

リンクの状態を判断するには、関連するドライバーで[oid\_GEN\_リンク\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-state)oid を使用しないでください。 代わりに、[NDIS\_の状態\_] リンクを使用して、リンクの状態の更新について\_状態の状態を示します。

[**Ndis\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**statusbuffer**メンバーには、 [**ndis\_LINK\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)構造体が含まれています。 この構造体は、メディアの物理的な状態を指定します。

ミニポートドライバーは、メディアの物理的な状態が変更されていない場合に、NDIS\_の状態\_リンク\_状態の状態を示すリンクを送信しないようにする必要があります。 ただし、この状態を回避することは必須ではありません。

ミニポートアダプターが低電力状態に移行する場合、NDIS 6.0 以降のミニポートドライバーは**MediaConnectStateUnknown**の接続状態を示す必要があります。 ミニポートアダプターが動作中の電源状態に移行すると、リンクが再確立された後、ミニポートドライバーは**MediaConnectStateConnected**の状態を示す必要があります。 NDIS 6.30 ミニポートドライバーは、wake on リンクの変更とセレクティブサスペンドが無効になっている場合にのみ、低電力の移行中に**MediaConnectStateUnknown**を示す必要があります。 つまり、低電力状態からの接続状態の変化を検出してウェイクアップできない場合は、低電力の移行中に、ミニポートドライバーが**MediaConnectStateUnknown**の接続状態を示す必要があります。

以前に示されたリンク状態で指定されているリンク状態に変更がない場合、NDIS は、後続のドライバーに状態を通知しないことがあります。 ただし、この動作は保証されません。 この状態を示すドライバーがある場合は、その中のどの特性が変更されているかを判断する必要があります。

前のドライバーが NDIS 5 の場合。*x*以前のプロトコルドライバーの場合、NDIS は ndis の\_状態\_リンク\_状態の状態を示すリンクを、適切な ndis 5.1 状態の表示に変換します。 NDIS は、リンク速度の変化を示しています。 [**ndis\_status\_リンク\_速度\_変更**](ndis-status-link-speed-change.md)の状態が表示されます。 NDIS は、 [**ndis\_ステータス\_メディア\_接続**](ndis-status-media-connect.md)と[**ndis\_ステータス\_メディア\_切断**](ndis-status-media-disconnect.md)状態を示す状態での接続状態の変化を示します。

Ndis は、NDIS 5 も変換します。NDIS 6.0 以降のドライバーの*x*ミニポートドライバーの状態。 Ndis は、ndis 5 で特定された状態の確認またはメディアの状態の変更を使用します。NDIS\_状態を作成するための*x* OID クエリ\_状態の状態を示す\_リンク。 NDIS は、次の変換を実行します。

-   [**Ndis の\_ステータス\_メディア\_接続**](ndis-status-media-connect.md)状態の表示は、 [**ndis\_リンクの\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)構造で**MediaConnectStateConnected**に変換されます。

-   [**Ndis の\_ステータス\_メディア\_切断**](ndis-status-media-disconnect.md)の状態の表示は、 [**ndis\_リンクの\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)構造で**MediaConnectStateDisconnected**に変換されます。

-   [**NDIS\_ステータス\_リンク\_速度\_変化**](ndis-status-link-speed-change.md)状態の表示、 [oid\_GEN\_リンク\_速度](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed)oid を使用してリンク速度の状態を生成します。

リンクの状態の詳細については、「 [OID\_GEN\_link\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-state)」を参照してください。

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
<td><p>NDIS 6.0 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)

[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_状態\_リンク\_速度\_変更**](ndis-status-link-speed-change.md)

[**NDIS\_状態\_メディア\_接続**](ndis-status-media-connect.md)

[**NDIS\_ステータス\_メディア\_切断**](ndis-status-media-disconnect.md)

[OID\_GEN\_リンク\_速度](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed)

[OID\_GEN\_LINK\_の状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-state)

 

 




