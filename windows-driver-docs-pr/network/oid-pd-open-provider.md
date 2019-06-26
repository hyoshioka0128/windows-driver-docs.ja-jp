---
title: OID_PD_OPEN_PROVIDER
description: NDIS プロトコルまたはフィルター ドライバーは、ミニポート ドライバーのおプロバイダー オブジェクトで PD 機能にアクセスする PD 対応ミニポート ドライバーに OID_PD_OPEN_PROVIDER のオブジェクト識別子 (OID) メソッド要求を送信します。
ms.assetid: B13E0FAC-A179-4785-9B39-CB498064947B
ms.date: 08/08/2017
keywords: -OID_PD_OPEN_PROVIDER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 8e53d716e2eab2b62de7d6c7babe9b82a429d1fe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383239"
---
# <a name="oidpdopenprovider"></a>OID\_PD\_オープン\_プロバイダー


OID のオブジェクト識別子 (OID) メソッド要求を送信する NDIS プロトコルまたはフィルター ドライバー\_PD\_オープン\_PD 対応ミニポート ドライバーにプロバイダーをミニポート ドライバーのおプロバイダー オブジェクトで PD 機能にアクセスするには. PD 対応のすべてのミニポート ドライバーでは、この OID 要求を処理する必要があります。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体には、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [ **NDIS\_PD\_オープン\_プロバイダー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_open_provider_parameters)構造体

<a name="remarks"></a>注釈
-------

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

[**NDIS\_PD\_オープン\_プロバイダー\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_open_provider_parameters)

[NDIS\_状態\_PD\_現在\_構成](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pd-current-config)

[OID\_PD\_閉じる\_プロバイダー](oid-pd-close-provider.md)

 

 




