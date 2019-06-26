---
title: CoNDIS WAN ミニポート ドライバーのクエリの処理
description: CoNDIS WAN ミニポート ドライバーのクエリの処理
ms.assetid: 634618ce-3168-4729-b74a-e69f27b62ef4
keywords:
- ドライバー WDK のいる CoNDIS WAN ネットワーク接続、クエリ処理
- OID_WAN_CO_GET_INFO
- OID_WAN_CO_GET_LINK_INFO
- OID_WAN_CO_GET_STATS_INFO
- WDK いる CoNDIS WAN クエリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 940af1a1fadd00782d3c3bc86834cb4f8c452122
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366644"
---
# <a name="handling-queries-in-a-condis-wan-miniport-driver"></a>CoNDIS WAN ミニポート ドライバーのクエリの処理





このトピックでは、いる CoNDIS WAN ミニポート ドライバーでのクエリを処理するための要件の概要を示します。 上位層、ドライバーは呼び出し[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest) WAN 固有の機能といる CoNDIS WAN ミニポート ドライバーと、ミニポート ドライバーの NIC の現在の状態を確認するクエリ要求

NDISWAN 中間ドライバーでは、クエリ要求を転送する NDIS 呼び出してミニポート ドライバーの[ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)関数。 いる CoNDIS WAN ミニポート ドライバーでは、この関数は、接続指向のミニポート ドライバーの場合と同様、いる CoNDIS WAN ミニポート ドライバーがサポートする点を除いて[いる CoNDIS WAN オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/index)します。

いる CoNDIS WAN ミニポート ドライバーが完了すると*MiniportCoOidRequest* NDIS の状態を返すことによって非同期的に\_状態\_保留中、その必要がありますはクエリを完了後で呼び出すことによって[ **NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequestcomplete)します。

NDIS を呼び出すと*MiniportCoOidRequest*、NDIS へのポインターを渡す、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request) OID のクエリを含む構造体ミニポート ドライバーから取得した情報を保持するバッファー。 ミニポート ドライバーは、要求が完了するまで、このバッファーを制御します。 内のバイト数が指定されている場合、 **InformationBufferLength**の NDIS メンバー\_OID\_要求は、OID に必要な情報で十分ですが、ミニポート ドライバーには、クエリ要求が失敗します。設定と、 **BytesNeeded**の NDIS メンバー\_OID\_OID が必要なバイト数を要求します。

他の要求は送信できず、特定の WAN ミニポート ドライバーに現在のクエリ要求が完了するまでです。

次の表は、Oid を取得またはいる CoNDIS WAN ミニポート ドライバーの運用上の特性を設定するために使用します。

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
<td align="left"><p>必須</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-link-info" data-raw-source="[OID_WAN_CO_GET_LINK_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-link-info)">OID_WAN_CO_GET_LINK_INFO</a> VC に関する情報を取得します。</td>
<td align="left"><p>必須</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-stats-info" data-raw-source="[OID_WAN_CO_GET_STATS_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-stats-info)">OID_WAN_CO_GET_STATS_INFO</a> VC の統計情報を取得します。</td>
<td align="left"><p>省略可能</p></td>
</tr>
</tbody>
</table>

 

いる CoNDIS WAN ミニポート ドライバーは、NDIS のすべてをサポートできる[全般オブジェクト](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546510(v=vs.85))します。 いる CoNDIS ミニポート ドライバーでは情報の設定の詳細については、次を参照してください。[クエリの実行または情報を設定する](querying-or-setting-information.md)します。

 

 





