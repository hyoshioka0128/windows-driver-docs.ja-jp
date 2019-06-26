---
title: OID_GEN_ISOLATION_PARAMETERS
description: NDIS および上にあるドライバーは、マルチ テナント機能の構成の VM ネットワーク アダプターのポートに設定されている (分離) パラメーターを取得する OID_GEN_ISOLATION_PARAMETERS のオブジェクト識別子 (OID) 要求を発行します。
ms.assetid: 68E89349-4907-4241-9C50-B13C75273F0D
ms.date: 08/08/2017
keywords: -OID_GEN_ISOLATION_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c997b7b8e61bce6ae3f08b6fceace4af5352dc24
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369090"
---
# <a name="oidgenisolationparameters"></a>OID\_GEN\_分離\_パラメーター


NDIS および上にあるドライバーは、OID のオブジェクト識別子 (OID) 要求を発行\_GEN\_分離\_パラメーター (分離) パラメーターを VM に設定されているマルチ テナント機能の構成を取得するネットワーク アダプターのポート。

各ルーティング ドメインは、ポートで個別に構成が、この OID は 1 つのクエリ、ルーティング ドメインのすべてのパラメーターを返します。

上にある、ドライバーは、2 つの手順でこの OID を発行する必要があります。

1.  Io クエリ、必要なバッファー サイズ、OID を使用してクエリを発行する、**サイズ**のメンバー、**ヘッダー**のメンバー、 [ **NDIS\_分離\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_isolation_parameters)構造体を設定**NDIS\_SIZEOF\_NDIS\_分離\_パラメーター\_リビジョン\_1**. (を参照してください**NDIS\_状態\_無効な\_長さ**以下です)。
2.  発行の OID、 **InformationBuffer**必要なサイズ。

OID のクエリ要求が正常に完了した場合、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体バッファーへのポインターが含まれています。 このバッファーには、次の順序でデータが含まれています。

1.  [ **NDIS\_分離\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_isolation_parameters)構造体

2.  1 つまたは複数[ **NDIS\_ルーティング\_ドメイン\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_routing_domain_entry)各ルーティング ドメインに 1 つの構造

3.  1 つまたは複数[ **NDIS\_ルーティング\_ドメイン\_分離\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_routing_domain_isolation_entry)ルーティング ドメインでグループ化、構造体

各[ **NDIS\_ルーティング\_ドメイン\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_routing_domain_entry)構造、 **FirstIsolationInfoEntryOffset**メンバーが含まれています、OID 情報バッファーの先頭からのオフセット (つまり、バッファーの先頭を**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造へのポインター)、最初に[ **NDIS\_ルーティング\_ドメイン\_分離\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_routing_domain_isolation_entry)そのルーティング ドメインの。 内のオフセット、 **NextIsolationInfoEntryOffset**一覧の最後の構造体のメンバーは 0 になります。

VM のネットワーク アダプターでマルチ テナント機能の構成パラメーターが設定されていない場合、ネットワーク アダプターのミニポート ドライバーの設定、**データ。クエリ\_情報。BytesWritten**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体をゼロを返す**NDIS\_の状態\_成功**します。 この場合は、データ内で、**データ。クエリ\_INFORMATION.InformationBuffer**ミニポート ドライバーによってメンバーが変更されていません。

<a name="remarks"></a>注釈
-------

### <a name="return-status-codes"></a>リターン状態コード

VM ネットワーク アダプターのミニポート ドライバーでは、この OID 要求の状態コードの次のいずれかを返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状態コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>OID 要求は正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>要求された情報を返す情報バッファーの長さが小さすぎます。 VM ネットワーク アダプターのミニポート ドライバーの設定、<strong>データ。METHOD_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>最小バッファー サイズ (バイト単位) に必要な構造体。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_FAILURE</strong></p></td>
<td><p>他の理由から、要求が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p>NDIS 6.40 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_分離\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_isolation_parameters)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_ルーティング\_ドメイン\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_routing_domain_entry)

[**NDIS\_ルーティング\_ドメイン\_分離\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_routing_domain_isolation_entry)

[**NDIS\_状態\_分離\_パラメーター\_変更**](ndis-status-isolation-parameters-change.md)

 

 




