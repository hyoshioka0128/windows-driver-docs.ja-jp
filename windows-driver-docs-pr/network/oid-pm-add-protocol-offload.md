---
title: OID_PM_ADD_PROTOCOL_OFFLOAD
description: セットとしては、NDIS プロトコル ドライバーは、ネットワーク アダプターに電源管理のためのプロトコルのオフロードを追加するのに OID_PM_ADD_PROTOCOL_OFFLOAD OID を使用します。
ms.assetid: 418f4ce8-64af-4e1e-877a-4cc606f63747
ms.date: 08/08/2017
keywords: -OID_PM_ADD_PROTOCOL_OFFLOAD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e04155e5118fd1971cdd753cba629235da9d1644
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560530"
---
# <a name="oidpmaddprotocoloffload"></a>OID\_PM\_追加\_プロトコル\_オフロード


NDIS プロトコル ドライバーが、OID を使用し、セットとして\_PM\_追加\_プロトコル\_プロトコルを追加する OID のオフロードが電源管理ネットワーク アダプターにオフロードします。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_PM\_プロトコル\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566760)構造体。

<a name="remarks"></a>注釈
-------

NDIS 6.20 が動作し、後でプロトコル ドライバーを使用して、OID\_PM\_追加\_プロトコル\_プロトコルを追加する OID のオフロードが電源管理ネットワーク アダプターにオフロードします。 要求が成功した場合は、ネットワーク アダプターは生成し、ネットワーク アダプターが低電力状態にする場合に、オフロードされたプロトコルのために必要な応答パケットを送信する必要があります。

プロトコル ドライバーは、基になるネットワーク アダプター、およびプロトコルの負荷を軽減する必要があるインターフェイスの IP アドレス) など、必要なデータとすぐに正常にバインドした後に、プロトコルをオフロードできます。 プロトコル ドライバーには、通知に応答していくつかその他の電源管理イベント、以前に追加された WOL パターンまたはオフロードのプロトコルの拒否などのプロトコルもオフロードできます。

NDIS およびその他のネットワーク アダプターを低電力状態に設定する NDIS の開始後に、同じミニポート アダプタにバインドされているプロトコル ドライバーでの競合状態を避けるためには、そのネットワーク アダプターに別のプロトコルの負荷を軽減しようとすると失敗になります。 NDIS プロトコル ドライバーの処理のコンテキストでのプロトコルの負荷を軽減しようとする場合など、 **NetEventSetPower** NDIS そのネットワーク アダプターのイベント通知には、要求が失敗します。

NDIS は、NDIS ドライバーは、基になるまでこの OID 要求を送信または上にあるドライバーへの要求が完了すると、前に設定、ULONG **ProtocolOffloadId**のメンバー、 [ **NDIS\_PM\_プロトコル\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566760)を一意の値構造体。 プロトコル ドライバーおよび NDIS でこのプロトコルのオフロード識別子を使用して、 [OID\_PM\_削除\_プロトコル\_オフロード](oid-pm-remove-protocol-offload.md)OID 要求からプロトコル オフロードを削除する、基になるネットワーク アダプター。

**注**  プロトコルのオフロード識別子は、各ネットワーク アダプターに設定されているプロトコルのオフロードの一意の値。 ただし、プロトコル オフロード識別子はグローバルに一意なすべてのネットワーク アダプターです。

 

生成 NDIS または基になるネットワーク アダプターに、オフロードが拒否された場合、 [ **NDIS\_状態\_PM\_オフロード\_REJECTED** ](https://msdn.microsoft.com/library/windows/hardware/ff567412)状態示します。 これは NDIS が返された後に発生\_状態\_OID の成功します。 **StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体には ULONG プロトコル オフロード識別子が含まれています、プロトコルのオフロードが拒否されます。

ネイティブの 802.11 ワイヤレス LAN のミニポート ドライバーでこの OID を使用する方法については、次を参照してください。[の追加および削除する低電力プロトコルをオフロード](https://msdn.microsoft.com/library/windows/hardware/ff543707)します。

ミニポート ドライバーでは、要求の状態コードの次のいずれかを返します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求されたプロトコルのオフロードが正常に追加されました。 **ProtocolOffloadId**のメンバー、 [ **NDIS\_PM\_プロトコル\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566760)構造体には、プロトコルのオフロードが含まれています。識別子です。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_PENDING  
完了待ちになっています。 NDIS では、要求が完了した後、最終的な状態コードと結果を呼び出し元の OID 要求完了ハンドラーに渡すは。

<a href="" id="ndis-status-pm-protocol-offload-list-full"></a>NDIS\_状態\_PM\_プロトコル\_オフロード\_一覧\_完全  
プロトコル リストをオフロードするために失敗しました要求が完全なネットワーク アダプターが別のプロトコルのオフロードを追加することはできません。

<a href="" id="ndis-status-resources"></a>NDIS\_状態\_リソース  
NDIS または基になるネットワーク アダプターを追加できなかったため新しいプロトコル オフロード リソースが不足しています。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状態\_無効な\_パラメーター  
1 つまたは複数のパラメーターで、 [ **NDIS\_PM\_プロトコル\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566760)構造が無効です。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状態\_バッファー\_すぎます\_短い  
情報バッファーが小さすぎます。 NDIS セット、**データ。設定\_情報。BytesNeeded** NDIS でメンバー\_OID\_構造体を最小バッファー サイズを要求が必要です。

<a href="" id="ndis-status-not-supported"></a>NDIS\_状態\_いない\_サポートされています。  
ネットワーク アダプターは、要求されたプロトコルのオフロードをサポートしていません。

<a href="" id="ndis-status-failure"></a>NDIS\_状態\_エラー  
上記の理由以外の理由、要求が失敗しました。

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
<td><p>以降では、NDIS 6.20 が動作をサポートします。 ミニポート ドライバーには必須です。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_PM\_プロトコル\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566760)

[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_状態\_PM\_オフロード\_拒否済み**](https://msdn.microsoft.com/library/windows/hardware/ff567412)

[OID\_PM\_削除\_プロトコル\_オフロード](oid-pm-remove-protocol-offload.md)

[追加と削除の省電力プロトコルのオフロード](https://msdn.microsoft.com/library/windows/hardware/ff543707)

 

 




