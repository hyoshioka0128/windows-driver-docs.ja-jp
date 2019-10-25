---
title: OID_PM_ADD_PROTOCOL_OFFLOAD
description: セットとして、NDIS プロトコルドライバーは OID_PM_ADD_PROTOCOL_OFFLOAD OID を使用して、電源管理のプロトコルオフロードをネットワークアダプターに追加します。
ms.assetid: 418f4ce8-64af-4e1e-877a-4cc606f63747
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_PM_ADD_PROTOCOL_OFFLOAD ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 71afaee5046ece17be585c6ba55b434577d85db7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844063"
---
# <a name="oid_pm_add_protocol_offload"></a>OID\_PM\_\_プロトコル\_オフロードの追加


セットとして、NDIS プロトコルドライバーは OID\_PM\_追加\_プロトコル\_オフロード OID を使用して、電源管理のプロトコルオフロードをネットワークアダプターに追加します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)構造へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

NDIS 6.20 以降のプロトコルドライバーでは、OID\_PM\_\_プロトコル\_オフロード OID を追加して、電源管理のプロトコルオフロードをネットワークアダプターに追加します。 要求が成功した場合、ネットワークアダプターが電力不足状態になると、ネットワークアダプターは、オフロードされたプロトコルに必要な応答パケットを生成して送信する必要があります。

プロトコルドライバーは、基になるネットワークアダプターに正常にバインドされた後、プロトコルをオフロードするために必要なデータ (インターフェイスの IP アドレスなど) があるとすぐにプロトコルをオフロードできます。 プロトコルドライバーは、以前に追加された WOL パターンやオフロードプロトコルの拒否など、他の電源管理イベント通知に応答してプロトコルをオフロードすることもできます。

NDIS および同じミニポートアダプターにバインドされているその他のプロトコルドライバーの競合状態を回避するために、NDIS がネットワークアダプターを低電力状態に設定しようとすると、そのネットワークアダプターに対する別のプロトコルのオフロードは失敗します。 たとえば、NDIS プロトコルドライバーが、そのネットワークアダプターの**NetEventSetPower**イベント通知を処理するコンテキストでプロトコルのオフロードを試みると、ndis は要求を失敗させます。

NDIS がこの OID 要求を基になる NDIS ドライバーに送信するか、またはそれ以降のドライバーへの要求を完了する前に、ndis [ **\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)構造の ULONG **ProtocolOffloadId**メンバーをに設定します。一意の値。 プロトコルドライバーと NDIS は、このプロトコルオフロード識別子を OID\_PM と共に使用して[\_プロトコル\_オフロード oid 要求\_削除](oid-pm-remove-protocol-offload.md)し、基になるネットワークアダプターからプロトコルオフロードを削除します。

**  プロトコル**オフロード識別子は、ネットワークアダプターに設定されているプロトコルオフロードごとに一意の値です。 ただし、プロトコルオフロード識別子は、すべてのネットワークアダプターでグローバルに一意ではありません。

 

NDIS または基になるネットワークアダプターがオフロードを拒否すると、 [**ndis\_ステータス\_PM\_オフロード\_拒否**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-offload-rejected)状態が通知されます。 これは、OID に対して NDIS\_STATUS\_SUCCESS が返された後に発生する可能性があります。 [**NDIS\_ステータス\_示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体の**statusbuffer**メンバーには、拒否されたプロトコルオフロードの ULONG プロトコルオフロード識別子が含まれています。

ネイティブ802.11 ワイヤレス LAN ミニポートドライバーがこの OID を使用する方法の詳細については、「[低電力プロトコルオフロードの追加と削除](https://docs.microsoft.com/windows-hardware/drivers/network/adding-and-deleting-low-power-protocol-offloads)」を参照してください。

ミニポートドライバーは、要求に対して次のいずれかの状態コードを返します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求されたプロトコルオフロードが正常に追加されました。 [**NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)構造体の**ProtocolOffloadId**メンバーには、プロトコルオフロード識別子が含まれています。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_保留中  
要求は完了待ちです。 NDIS は、要求が完了した後に、最終的な状態コードと結果を呼び出し元の OID 要求完了ハンドラーに渡します。

<a href="" id="ndis-status-pm-protocol-offload-list-full"></a>NDIS\_ステータス\_PM\_プロトコル\_オフロード\_リスト\_完全  
プロトコルオフロードリストがいっぱいで、ネットワークアダプターが別のプロトコルオフロードを追加できないため、要求は失敗しました。

<a href="" id="ndis-status-resources"></a>NDIS\_状態\_リソース  
リソースが不足しているため、NDIS または基になるネットワークアダプターで新しいプロトコルオフロードを追加できませんでした。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_の状態\_無効な\_パラメーターです  
[**NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)構造の1つ以上のパラメーターが無効です。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_ステータス\_バッファー\_短すぎる\_  
情報バッファーが短すぎます。 NDIS はデータを設定**します。\_情報を設定します。** 必要な最小バッファーサイズに対して、NDIS\_OID\_要求構造体のメンバーが必要です。

<a href="" id="ndis-status-not-supported"></a>NDIS\_の状態\_\_サポートされていません  
ネットワークアダプターは、要求されたプロトコルオフロードをサポートしていません。

<a href="" id="ndis-status-failure"></a>NDIS\_状態\_エラー  
この要求は、上記の理由以外の理由で失敗しました。

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
<td><p>NDIS 6.20 以降でサポートされています。 ミニポートドライバーの場合は必須です。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_STATUS\_PM\_オフロード\_拒否されました**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-offload-rejected)

[OID\_PM\_\_プロトコル\_オフロードの削除](oid-pm-remove-protocol-offload.md)

[低電力プロトコルオフロードの追加と削除](https://docs.microsoft.com/windows-hardware/drivers/network/adding-and-deleting-low-power-protocol-offloads)

 

 




