---
title: NDIS_STATUS_PM_OFFLOAD_REJECTED
description: NDIS_STATUS_PM_OFFLOAD_REJECTED 状態は、重なってドライバーの電源管理のプロトコルのオフロードが拒否されたことを示します。
ms.assetid: 54922e70-2b56-4141-b79b-73418c7553e3
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PM_OFFLOAD_REJECTED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 73216049c05c419e1d3129483b9819531d0aa14b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368525"
---
# <a name="ndisstatuspmoffloadrejected"></a>NDIS\_状態\_PM\_オフロード\_拒否済み


NDIS\_状態\_PM\_オフロード\_拒否状態が電源管理のプロトコルのオフロードが拒否されたことをドライバーに関連することを示します。

<a name="remarks"></a>注釈
-------

NDIS ミニポート ドライバーは、NDIS を生成できる\_状態\_PM\_オフロード\_いずれかのオフロードのプロトコルを削除すると拒否の状態を示す値。 **StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造には ULONG プロトコルのオフロード識別子にはが含まれています拒否されたプロトコルの負荷を軽減します。 NDIS のプロトコルのオフロード識別子を提供する、 **ProtocolOffloadId**のメンバー、 [ **NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)構造体。

NDIS 生成、NDIS\_状態\_PM\_オフロード\_以前オフロードされたプロトコル、ネットワーク アダプターから削除する必要があるときに拒否の状態を示す値。 たとえば、NDIS より高い優先順位プロトコル オフロード用の無料のリソースへのプロトコルのオフロードを削除する可能性があります。 NDIS は、拒否されたプロトコル、オフロードのオフロードは、その他のバインディングには送信されませんが、バインディングに、状態を示す値を送信します。

ミニポート ドライバーでは、以前に受け入れられたプロトコルのオフロードを拒否するには、この状態表示を報告します。 たとえば、WiFi WOL の場合、ミニポート ドライバー行う必要があります、NDIS\_状態\_PM\_オフロード\_拒否状態の表示/GTK される辞書の回転は (ためベンダー固有 WOL をサポートするために必要ない場合インフラストラクチャのサポート)。

プロトコルの負荷を軽減し、インフラストラクチャの間でローミングするインフラストラクチャの要素を使用するワイヤレス ネットワーク アダプターでは、新しいインフラストラクチャ要素が 1 つ前と同じ機能をサポートしていないことことができます。 ここでは、ミニポート ドライバーは、NDIS の状態の表示を発行できます NDIS を発行する NDIS および\_状態\_PM\_オフロード\_固有のエラー コードで拒否されます。

WiFi ドライバー プロトコル オフロード要求をローカルでのキャッシュ可能性があります。 ドライバーを追加または削除プロトコル オフロード OID を処理するときにのみ、ローカル キャッシュを更新するドライバーを選択できます。 受信するまで、ドライバーは、インフラストラクチャの更新を遅らせることができます、 [OID\_PM\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters) OID。

インフラストラクチャに対応するすべてのプロトコルの負荷を軽減するための十分なリソースがないです。 この場合は、インフラストラクチャでは、プロトコルの一覧の一部をオフロードを使用できます。 ミニポート ドライバーが、OID が完了したとき\_PM\_パラメーターが要求を設定、ミニポート ドライバーは、NDIS を行う必要があります\_状態\_PM\_オフロード\_ごとの拒否状態のインジケータープロトコルは、AP を拒否したことをオフロードします。

たとえば、ネットワーク アダプターでは、ARP オフロードをサポートするために、アジア太平洋のプロキシ ARP を使用できます。

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
<td><p>以降では、NDIS 6.20 が動作をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[OID\_PM\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)

 

 




