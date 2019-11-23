---
title: OID_GEN_SUPPORTED_PACKET_FILTERS
description: NDIS およびそれ以降のドライバーは、ミニポートアダプターが初期化中にフィルター処理できるネットパケットの種類を取得します。
ms.assetid: c19cecf3-ae47-4fd1-b5dc-1f3de469e548
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_GEN_SUPPORTED_PACKET_FILTERS
ms.localizationpriority: medium
ms.openlocfilehash: 6b105a29f91604fe1f64f3960c1e7fb957216753
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844595"
---
# <a name="oid_gen_supported_packet_filters"></a>OID\_GEN\_サポート\_パケット\_フィルター


NDIS およびそれ以降のドライバーは、ミニポートアダプターが初期化中にフィルター処理できるネットパケットの種類を取得します。

この OID は、windows Vista 以降のバージョンの Windows オペレーティングシステムでは実装されていない  に**注意**してください。 詳細については、「解説」を参照してください。

 

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
実装されていません。 (「解説」を参照してください。)

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、初期化中にサポートされているパケットフィルターを提供します。

サポートされているパケットフィルターを指定するために、ミニポートドライバーは、 [**NDIS\_ミニポート\_アダプター\_GENERAL\_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体の**supportedpacketfilters**メンバーを設定し、構造体を[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数に渡します。

NDIS は、 [**ndis\_BIND\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造体の**supportedpacketfilters**メンバーのプロトコルドライバーに情報を渡します。

**Supportedpacketfilters**の値は、フィルターの種類フラグのビットごとの or です。 フィルターの種類のフラグの一覧については、「 [oid\_GEN\_現在の\_パケット\_フィルター](oid-gen-current-packet-filter.md) oid」を参照してください。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[**NDIS\_バインド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[OID\_GEN\_現在の\_パケット\_フィルター](oid-gen-current-packet-filter.md)

 

 




