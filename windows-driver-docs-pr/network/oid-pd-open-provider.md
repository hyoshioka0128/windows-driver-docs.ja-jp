---
title: OID_PD_OPEN_PROVIDER
description: NDIS プロトコルまたはフィルタードライバーは、OID_PD_OPEN_PROVIDER のオブジェクト識別子 (OID) メソッド要求を PD 対応ミニポートドライバーに送信して、ミニポートドライバーの PDPI プロバイダーオブジェクトの PD 機能にアクセスできるようにします。
ms.assetid: B13E0FAC-A179-4785-9B39-CB498064947B
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_PD_OPEN_PROVIDER ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 680b9e6c04827133014c9758c72cab889ea1c1e3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844067"
---
# <a name="oid_pd_open_provider"></a>OID\_PD\_オープン\_プロバイダー


NDIS プロトコルまたはフィルタードライバーは、OID のオブジェクト識別子 (OID) メソッド要求を\_PD\_オープン\_プロバイダーに送信して、ミニポートドライバーの PDPI プロバイダーオブジェクトの PD 機能にアクセスできるようにします。 すべての PD 対応ミニポートドライバーは、この OID 要求を処理する必要があります。

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [**NDIS\_PD\_オープン\_プロバイダー\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_open_provider_parameters)構造体

<a name="remarks"></a>注釈
-------

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

[**NDIS\_PD\_\_プロバイダー\_パラメーターを開く**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_open_provider_parameters)

[NDIS\_の状態\_PD\_現在の\_構成](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pd-current-config)

[OID\_PD\_\_プロバイダーを閉じる](oid-pd-close-provider.md)

 

 




