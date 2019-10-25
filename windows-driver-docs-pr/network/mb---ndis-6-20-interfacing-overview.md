---
title: MB/NDIS 6.20 のインターフェイスの概要
description: MB/NDIS 6.20 のインターフェイスの概要
ms.assetid: 6abde9b4-8ac2-4757-8db3-4f563fc5ed24
keywords:
- NDIS 6.20 WDK、モバイルブロードバンド (MB) インターフェイス
- モバイルブロードバンド (MB) WDK
- モバイルブロードバンド (MB) WDK、NDIS 6.20 インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93ae3bd906d0da5be28e21538910dd0f11fc14be
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844301"
---
# <a name="mb--ndis-620-interfacing-overview"></a>MB/NDIS 6.20 のインターフェイスの概要


このトピックでは、MB ドライバーモデルをパースペクティブに配置するために、 *NDIS 6.20 仕様*に関する十分な背景情報を提供するように設計されています。 NDIS 6.20 のリファレンスとしては想定されていません。 このコンテンツと*ndis 6.20 仕様*の不一致の場合、詳細については、 [ndis 6.20](introduction-to-ndis-6-20.md)のドキュメントを参照してください。

NDIS 6.20 では、MB サービスは[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)を呼び出して、ミニポートドライバーに OID 要求を発行します。 次に、ミニポートドライバーは[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)を呼び出して、データを MB サービスに戻します。

NDIS 6.20 では、次の種類の OID 操作がサポートされています。

-   サービスからミニポートドライバーにデータを送信する操作を*設定*します。

-   サービスにデータを返すようにミニポートドライバーを要求する*クエリ*操作。

-   入力パラメーターと出力パラメーターの両方を持つ、関数呼び出しに相当する*メソッド*操作。

最後に、ミニポートドライバーは、MB デバイスの状態の変化についてサービスに通知するデータを含む*兆候*を送信することがあります。

### <a name="receiving-set-and-query-requests"></a>*Set*要求と*クエリ*要求の受信

MB ミニポートドライバーは、*設定*要求と*クエリ*要求の両方に応答するために、 [*miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) NDIS ハンドラーを実装します。

### <a name="sending-status-indications"></a>送信ステータスの示さ

ミニポートドライバーは、 [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)を呼び出すことによって、MB サービスの状態を示します。 ステータスの表示の詳細については、「 [**NDIS\_status\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)の構造」を参照してください。

### <a name="connection-state-indications"></a>接続状態のインジケーター

Ndis 6.20 ミニポートドライバーでは、 [**ndis\_status\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)の状態の表示を使用して、送信メディアの物理的な特性が変更されたことを ndis およびそれ以降のドライバーに通知する必要があります。

NDIS\_ステータス\_表示構造体の**Statusbuffer**メンバーは、送信メディアの物理的な状態を指定する[**ndis\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)構造です。

MB のミニポートドライバーは、中間状態が変化していない場合は、\_リンク\_状態の状態を示すために、NDIS\_状態の送信を回避する必要があります。 ただし、この状態の表示を避けるために、ミニポートドライバーは必ずしも必要ではありません。

MB ミニポートドライバーは、現在接続されているデータクラスの最大データレートを報告する必要があります。 接続中のデータクラスの変更は、報告された対応するデータレートを使用して接続状態を示す必要があります。 この規則の推奨される実装は次のとおりです。

1.  この仕様に準拠している MB のミニポートドライバーは、 [**ndis\_status\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)を使用して\_状態をリンクする必要があります。これにより、NDIS\_STATUS\_MEDIA\_CONNECT、NDIS\_status の代わりに接続状態の変化を示すことが\_MEDIA\_DISCONNECT、または NDIS\_STATUS\_リンク\_速度\_変更 (NDIS 5.1 のように) 接続状態の情報を示します。

2.  [**Ndis\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)構造体の**XmitLinkSpeed**および**rcvlinkspeed**メンバーは、ndis\_リンクの\_速度\_不明であることをレポートすることはできません。 ミニポートドライバーは、次の表の情報を使用して速度を報告する必要があります。

**GSM ベースの MB のデバイス速度のリンク**

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">データクラス</th>
<th align="left">XmitLinkSpeed</th>
<th align="left">RcvLinkSpeed</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>GPRS</p></td>
<td align="left"><p>8 ~ 48 kbps</p></td>
<td align="left"><p>8 ~ 48 kbps</p></td>
</tr>
<tr class="even">
<td align="left"><p>EDGE</p></td>
<td align="left"><p>8 ~ 220 kbps</p></td>
<td align="left"><p>8 ~ 220 kbps</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UMTS</p></td>
<td align="left"><p>64 ~ 384 kbps</p></td>
<td align="left"><p>64 ~ 384 kbps</p></td>
</tr>
<tr class="even">
<td align="left"><p>HSDPA</p></td>
<td align="left"><p>64 ~ 5.76 mbps</p></td>
<td align="left"><p>1.8 ~ 14.4 mbps</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HSUPA</p></td>
<td align="left"><p>1.4 ~ 5.76 mbps</p></td>
<td align="left"><p>64 kbps ~ 7.2 mbps</p></td>
</tr>
</tbody>
</table>

 

**CDMA ベースのデバイス速度リンクの場合**

| データクラス     | XmitLinkSpeed            | RcvLinkSpeed            |
|----------------|--------------------------|-------------------------|
| 1xRTT          | 115.2 kbps ~ 307.2 kbps | 153.6 kbps ~ 3 mbps    |
| 3xRTT          | 614 kbps ~ 1.04 mbps    | 307.2 kbps ~ 1.04 mbps |
| 1xEV-DO        | 153.6 kbps               | 2.4 mbps                |
| 1xEvDO Rev. A. | 1.8 mbps                 | 3.1 mbps                |
| 1xEV-DV        | 1.8 mbps                 | 3.1 mbps                |
| 1xEvDO Rev. B. | 27 mbps                  | 3.1 mbps ~ 73.5 mbps   |

 

**  MB**のデバイスは、前の表に示されている速度の範囲で速度を報告する必要があります。

 

NDIS 5.1 とは異なり、異なるリンク状態の変更通知は、ndis\_LINK\_STATE データ構造を使用して\_の状態を示す\_リンクされた1つの NDIS\_状態に統合されます。 次の表の情報に従って、NDIS 5.1 の指示をこの構造にマップすることができます。 リンク速度の変更の場合、示されるコンシューマーは、送信速度と受信速度の値を、前に示したように記録したものと比較して、リンク速度の変化が発生したかどうかを判断する必要があります。

**NDIS 5.1 から6.x への接続状態を示すマッピング**

NDIS 5.1 に示されている ndis 6.x\_リンク\_状態データ構造パラメーター値 NDIS\_状態\_メディア\_接続

MediaConnectState

MediaConnectStateConnected

NDIS\_ステータス\_メディア\_切断

MediaConnectState

MediaConnectStateDisconnected

NDIS\_状態\_リンク\_速度\_変更

XmitLinkSpeed

送信速度 (bps)

RcvLinkSpeed

受信速度 (bps)

 

 

 





