---
title: CoNDIS WAN ミニポート ドライバー情報の設定
description: CoNDIS WAN ミニポート ドライバー情報の設定
ms.assetid: 950cb2cb-7f02-4f3c-924a-0d1e7bb19b55
keywords:
- CoNDIS WAN ドライバー WDK ネットワーク、情報設定
- OID_WAN_CO_SET_LINK_INFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b1cb23df349f54cb98c735e9c6b4cc6296a07ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841946"
---
# <a name="setting-condis-wan-miniport-driver-information"></a>CoNDIS WAN ミニポート ドライバー情報の設定





このトピックでは、CoNDIS WAN ミニポートドライバーで情報を設定するための要件の概要について説明します。 上層のドライバーは、set 要求を使用して[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)を呼び出し、CONDIS WAN ミニポートドライバーとミニポートドライバーの NIC で保持される情報を変更します。

NDISWAN 中間ドライバーがセット要求を転送した後、NDIS は WAN ミニポートドライバーの[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数を呼び出します。 Condis WAN ミニポートドライバーでは、この機能はすべての CoNDIS ドライバーと同じですが、condis wan ミニポートドライバーでは[CONDIS Wan オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/index)がサポートされている点が異なります。

現在のセット要求が完了するまで、他の要求は CoNDIS WAN ミニポートドライバーに送信されません。 ミニポートドライバーが set 要求をすぐに完了しない場合、NDIS\_STATUS\_*MiniportCoOidRequest*から返され、後で[**NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)を呼び出して要求を完了する必要があります。

Condis WAN ミニポートドライバーは、次の CoNDIS WAN Oid に対して認識し、適切に応答する必要があります。

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
<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-set-link-info" data-raw-source="[OID_WAN_CO_SET_LINK_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-set-link-info)">OID_WAN_CO_SET_LINK_INFO</a>VC の情報を設定します。</td>
<td align="left"><p>必須かどうか</p></td>
</tr>
</tbody>
</table>

 

CoNDIS WAN ミニポートドライバーは、NDIS[全般オブジェクト](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546510(v=vs.85))もサポートしています。 CoNDIS ミニポートドライバーでの情報の設定の詳細については、「[情報の照会または設定](querying-or-setting-information.md)」を参照してください。

 

 





