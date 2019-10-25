---
title: OID_PD_CLOSE_PROVIDER
description: NDIS プロトコルまたはフィルタードライバーは、OID_PD_CLOSE_PROVIDER のオブジェクト識別子 (OID) メソッド要求を PDPI プロバイダーに送信して、PDPI プロバイダーオブジェクトの PD 機能にアクセスできるようにします。
ms.assetid: 8A504A81-6DC8-415C-9FDC-F03657A0EB87
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_PD_CLOSE_PROVIDER ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: a4febedd19324fa449ca53630aaa9b8da0d8a0e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844069"
---
# <a name="oid_pd_close_provider"></a>OID\_PD\_\_プロバイダーを閉じる


NDIS プロトコルまたはフィルタードライバーは、オブジェクト識別子 (OID) メソッド要求を OID\_PD\_終了\_プロバイダーに送信して、pdpi プロバイダーオブジェクトの PD 機能にアクセスできるようにします。

NDIS プロトコルまたはフィルタードライバーは、バインド解除通知、一時停止通知、低電力イベント、または pd がバインドで無効になっていることを示す PD 構成変更イベントを受信するときに、この OID を呼び出す必要があります。

この OID を呼び出す前に、NDIS プロトコルまたはフィルタードライバーが、PD プロバイダーインスタンスに対して作成されたキュー、カウンター、フィルターなどのすべての PD オブジェクトを閉じて解放しておく必要があります。 NDIS プロトコルまたはフィルタードライバーは、この OID を発行する前に、PD プロバイダーディスパッチテーブル関数のいずれかに対して実行中の呼び出しがないことを保証する必要があります。

<a name="requirements"></a>要件
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
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)

[**NDIS\_PD\_\_プロバイダー\_パラメーターを閉じる**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_close_provider_parameters)

[NDIS\_の状態\_PD\_現在の\_構成](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pd-current-config)

[OID\_PD\_オープン\_プロバイダー](oid-pd-open-provider.md)

 

 




