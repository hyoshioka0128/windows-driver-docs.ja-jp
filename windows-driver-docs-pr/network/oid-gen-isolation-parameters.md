---
title: OID_GEN_ISOLATION_PARAMETERS
description: NDIS およびそれ以降のドライバーは、VM ネットワークアダプターのポートに設定されているマルチテナント構成 (分離) のパラメーターを取得するために、OID_GEN_ISOLATION_PARAMETERS のオブジェクト識別子 (OID) 要求を発行します。
ms.assetid: 68E89349-4907-4241-9C50-B13C75273F0D
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_ISOLATION_PARAMETERS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 8601ee40be6a20a2b4fae64d0d790a2b7d96954f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844623"
---
# <a name="oid_gen_isolation_parameters"></a>OID\_GEN\_分離\_パラメーター


NDIS およびそれ以降のドライバーは、OID\_\_\_GEN のオブジェクト識別子 (OID) 要求を発行して、VM ネットワークアダプターのポートに設定されているマルチテナント構成 (分離) のパラメーターを取得します。

各ルーティングドメインはポートで個別に構成されますが、この OID は1つのクエリ内のすべてのルーティングドメインのパラメーターを返します。

この OID は、次の2つの手順で発行されます。

1.  Io は必要なバッファーサイズを照会し、ndis\_分離の**ヘッダー**メンバーの**サイズ**メンバーで OID クエリを発行します[ **\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_isolation_parameters)構造は NDIS **\_SIZEOF\_ndis\_分離に設定され\_PARAMETERS\_REVISION\_1**です。 (「 **NDIS\_STATUS\_無効な\_の長さ**」を参照してください)。
2.  必要なサイズの**Informationbuffer**を使用して OID を発行します。

OID クエリ要求が正常に完了した場合、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、バッファーへのポインターが含まれます。 このバッファーには、次のデータが順に格納されています。

1.  [**NDIS\_分離\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_isolation_parameters)構造体

2.  1つまたは複数の[**NDIS\_ルーティングドメイン\_のエントリ構造\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_routing_domain_entry)ルーティングドメインごとに1つ

3.  1つまたは複数の[**NDIS\_ルーティング\_ドメイン\_分離\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_routing_domain_isolation_entry)構造をルーティングドメイン別にグループ化します。

各[**NDIS\_ルーティング\_ドメイン\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_routing_domain_entry)構造体では、 **FirstIsolationInfoEntryOffset**メンバーに、OID 情報バッファーの先頭からのオフセット (つまり、**バッファーの先頭から** [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造ポイントを指す) の informationbuffer メンバーは、最初の[**NDIS\_ルーティング\_ドメイン\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_routing_domain_isolation_entry)そのルーティングドメインの分離\_エントリを指します。 リスト内の最後の構造体の**Nextiの Ationinfoentryoffset**メンバーのオフセットが0です。

VM ネットワークアダプターにマルチテナント構成パラメーターが設定されていない場合、ネットワークアダプターのミニポートドライバーはデータを設定し**ます。クエリ\_情報。BytesWritten** OID のメンバーが[ **\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体を0に指定し、 **NDIS\_STATUS\_SUCCESS**を返しました。 この場合、データ内のデータ**です。クエリ\_情報。 InformationBuffer**メンバーはミニポートドライバーによって変更されません。

<a name="remarks"></a>注釈
-------

### <a name="return-status-codes"></a>ステータスコードを返す

VM ネットワークアダプターのミニポートドライバーは、この OID 要求に対して次のいずれかの状態コードを返します。

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
<td><p>OID 要求が正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>情報バッファーの長さが小さすぎて要求された情報を返すことができません。 VM ネットワークアダプターのミニポートドライバーは、データを設定し<strong>ます。METHOD_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズ (バイト単位) に、bytesneeded 必要です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_FAILURE</strong></p></td>
<td><p>他の理由で要求が失敗しました。</p></td>
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
<td><p>NDIS 6.40 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_分離\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_isolation_parameters)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_ルーティング\_ドメイン\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_routing_domain_entry)

[**NDIS\_ルーティング\_ドメイン\_分離\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_routing_domain_isolation_entry)

[**NDIS\_ステータス\_分離\_パラメーター\_変更**](ndis-status-isolation-parameters-change.md)

 

 




