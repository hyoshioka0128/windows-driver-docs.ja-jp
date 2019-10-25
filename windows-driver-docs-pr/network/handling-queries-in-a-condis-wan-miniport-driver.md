---
title: CoNDIS WAN ミニポート ドライバーのクエリの処理
description: CoNDIS WAN ミニポート ドライバーのクエリの処理
ms.assetid: 634618ce-3168-4729-b74a-e69f27b62ef4
keywords:
- CoNDIS WAN ドライバー WDK ネットワーク、クエリ処理
- OID_WAN_CO_GET_INFO
- OID_WAN_CO_GET_LINK_INFO
- OID_WAN_CO_GET_STATS_INFO
- WDK のクエリクエリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e76abd96d7319b5995cb2134763b3067c21c2e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842564"
---
# <a name="handling-queries-in-a-condis-wan-miniport-driver"></a>CoNDIS WAN ミニポート ドライバーのクエリの処理





このトピックでは、CoNDIS WAN ミニポートドライバーでクエリを処理するための要件の概要について説明します。 上位層ドライバーは、クエリ要求を使用して[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)を呼び出し、wan 固有の機能と、condis wan ミニポートドライバーとミニポートドライバーの NIC の現在の状態を確認します。

NDISWAN 中間ドライバーがクエリ要求を転送した後、NDIS はミニポートドライバーの[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数を呼び出します。 Condis WAN ミニポートドライバーでは、この機能は接続指向のミニポートドライバーの場合と同じですが、condis wan ミニポートドライバーでは[CONDIS Wan オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/index)がサポートされている点が異なります。

*MINIPORTCOOIDREQUEST*ステータス\_保留中\_の状態を返すことによって、CONDIS WAN ミニポートドライバーが非同期に完了した場合は、後で[**NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)を呼び出してクエリを完了する必要があります。

NDIS が*MiniportCoOidRequest*を呼び出すと、ndis は、クエリ oid を含む要求構造とミニポートドライバーから取得した情報を格納するバッファーを含む、 [**ndis\_oid\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)のポインターを渡します。 ミニポートドライバーは、要求が完了するまでこのバッファーを制御します。 NDIS\_OID\_要求の**Informationbufferlength**メンバーに指定されたバイト数が oid で必要な情報に対して十分でない場合、ミニポートドライバーはクエリ要求を失敗させて、**必要な bytesneeded**設定します。oid\_OID のメンバーは、OID が必要とするバイト数に\_要求します。

現在のクエリ要求が完了するまで、他の要求は特定の WAN ミニポートドライバーに送信されません。

次の表は、CoNDIS WAN ミニポートドライバーの動作特性を取得または設定するために使用される Oid をまとめたものです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">名前</th>
<th align="left">省略可能または必須</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p></p>
<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-info" data-raw-source="[OID_WAN_CO_GET_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-info)">OID_WAN_CO_GET_INFO</a>仮想接続 (VCs) に関する情報を取得します。</td>
<td align="left"><p>必須かどうか</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-link-info" data-raw-source="[OID_WAN_CO_GET_LINK_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-link-info)">OID_WAN_CO_GET_LINK_INFO</a>VC に関する情報を取得します。</td>
<td align="left"><p>必須かどうか</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-stats-info" data-raw-source="[OID_WAN_CO_GET_STATS_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-stats-info)">OID_WAN_CO_GET_STATS_INFO</a>VC の統計情報を取得します。</td>
<td align="left"><p>オプション</p></td>
</tr>
</tbody>
</table>

 

CoNDIS WAN ミニポートドライバーは、すべての NDIS[一般オブジェクト](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546510(v=vs.85))をサポートできます。 CoNDIS ミニポートドライバーでの情報の設定の詳細については、「[情報の照会または設定](querying-or-setting-information.md)」を参照してください。

 

 





