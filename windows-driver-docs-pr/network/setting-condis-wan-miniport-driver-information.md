---
title: CoNDIS WAN ミニポート ドライバー情報の設定
description: CoNDIS WAN ミニポート ドライバー情報の設定
ms.assetid: 950cb2cb-7f02-4f3c-924a-0d1e7bb19b55
keywords:
- ドライバー WDK ネットワーク、WAN いる CoNDIS 情報設定
- OID_WAN_CO_SET_LINK_INFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b73413927e8f3ba8d6a24a849528d877821644de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377022"
---
# <a name="setting-condis-wan-miniport-driver-information"></a>CoNDIS WAN ミニポート ドライバー情報の設定





このトピックでは、いる CoNDIS WAN ミニポート ドライバーに情報を設定するための要件の概要を示します。 上位層、ドライバーは呼び出し[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)いる CoNDIS WAN ミニポート ドライバーと、ミニポート ドライバーの NIC を管理する情報を変更するセットの要求とします。

NDISWAN 中間ドライバーでは、セットの要求を転送する NDIS 呼び出して WAN ミニポート ドライバーの[ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)関数。 いる CoNDIS WAN ミニポート ドライバーでは、この関数はすべている CoNDIS ミニポート ドライバーの場合と同様、いる CoNDIS WAN ミニポート ドライバーがサポートする点を除いて[いる CoNDIS WAN オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/index)します。

その他の要求は送信できずいる CoNDIS WAN ミニポート ドライバーにセットの現在の要求が完了するまでです。 NDIS ミニポート ドライバーがセットの要求がすぐに完了しない場合を返します\_状態\_から PENDING *MiniportCoOidRequest*後で呼び出す必要がありますと[ **NdisCoOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequestcomplete)要求を完了します。

いる CoNDIS WAN ミニポート ドライバーが認識し、次のいる CoNDIS WAN Oid に適切に対応する必要があります。

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
<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-set-link-info" data-raw-source="[OID_WAN_CO_SET_LINK_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-set-link-info)">OID_WAN_CO_SET_LINK_INFO</a> VC の情報を設定します。</td>
<td align="left"><p>必須</p></td>
</tr>
</tbody>
</table>

 

いる CoNDIS WAN ミニポート ドライバーは、NDIS もサポートしています。[全般オブジェクト](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546510(v=vs.85))します。 いる CoNDIS ミニポート ドライバーでは情報の設定の詳細については、次を参照してください。[クエリの実行または情報を設定する](querying-or-setting-information.md)します。

 

 





