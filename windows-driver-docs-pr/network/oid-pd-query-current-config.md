---
title: OID_PD_QUERY_CURRENT_CONFIG
description: NDIS プロトコルまたはフィルタードライバーは、OID_PD_QUERY_CURRENT_CONFIG のオブジェクト識別子 (OID) メソッド要求を PD 対応ミニポートドライバーに送信して、PD の状態と機能を取得します。 すべての PD 対応ミニポートドライバーは、この OID 要求を処理する必要があります。
ms.assetid: 1BF09EAE-9D03-4655-98CD-D3A10BF48A48
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_PD_QUERY_CURRENT_CONFIG ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: c99b86721c23064c6983e5f7a2324162d116fcbd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844066"
---
# <a name="oid_pd_query_current_config"></a>OID\_PD\_クエリ\_現在の\_構成


NDIS プロトコルまたはフィルタードライバーは、OID のオブジェクト識別子 (OID) メソッド要求を\_PD\_クエリ\_現在の\_CONFIG に送信して、pd 対応ミニポートドライバーに送信し、PD の状態と機能を取得します。 すべての PD 対応ミニポートドライバーは、この OID 要求を処理する必要があります。

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [**NDIS\_PD\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pd_config)構造体

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

[**NDIS\_PD\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pd_config)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

 

 




