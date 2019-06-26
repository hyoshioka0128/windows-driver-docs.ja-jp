---
title: OID_PD_CLOSE_PROVIDER
description: NDIS プロトコルまたはフィルター ドライバーは、おプロバイダー オブジェクトの PD 機能へのアクセスを断念するおプロバイダーに OID_PD_CLOSE_PROVIDER のオブジェクト識別子 (OID) メソッド要求を送信します。
ms.assetid: 8A504A81-6DC8-415C-9FDC-F03657A0EB87
ms.date: 08/08/2017
keywords: -OID_PD_CLOSE_PROVIDER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7f321b3903fe5b21e8ba453db847c6d18f6c3e32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383243"
---
# <a name="oidpdcloseprovider"></a>OID\_PD\_閉じる\_プロバイダー


OID のオブジェクト識別子 (OID) メソッド要求を送信する NDIS プロトコルまたはフィルター ドライバー\_PD\_閉じる\_おプロバイダーおプロバイダー オブジェクトの PD 機能へのアクセスを提供するプロバイダー。

NDIS プロトコルまたはフィルター ドライバーは、バインドの解除通知を一時停止を示す値、省電力イベントの場合、または、バインディング、PD が無効になっているかを示す PD 構成変更イベントを受信すると、この OID を呼び出す必要があります。

この OID を呼び出す前に NDIS プロトコルまたはフィルター ドライバーをする必要があることは、クローズされ、キュー、カウンター、および PD プロバイダーのインスタンスを作成したフィルターなどのすべての PD オブジェクトを解放ことが確認します。 NDIS プロトコルまたはフィルター ドライバーする必要があることを保証しない PD プロバイダーのディスパッチのいずれかに進行中の呼び出しテーブル関数この OID を発行する前にします。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)

[**NDIS\_PD\_閉じる\_プロバイダー\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_close_provider_parameters)

[NDIS\_状態\_PD\_現在\_構成](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pd-current-config)

[OID\_PD\_オープン\_プロバイダー](oid-pd-open-provider.md)

 

 




