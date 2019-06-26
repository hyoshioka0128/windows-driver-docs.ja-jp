---
title: MB/NDIS 6.20 のインターフェイスの概要
description: MB/NDIS 6.20 のインターフェイスの概要
ms.assetid: 6abde9b4-8ac2-4757-8db3-4f563fc5ed24
keywords:
- NDIS 6.20 WDK では、モバイル ブロード バンド (MB) のインターフェイス
- モバイル ブロード バンド (MB) の WDK
- モバイル ブロード バンド (MB) WDK、NDIS 6.20 インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d32345e58a98c3fddfca3002076cb51c524b3b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374816"
---
# <a name="mb--ndis-620-interfacing-overview"></a>MB/NDIS 6.20 のインターフェイスの概要


このトピックではについて十分な背景を提供するように設計、 *NDIS 6.20 が動作仕様*パースペクティブに MB ドライバー モデルを格納します。 NDIS 6.20 が動作の参照であるものではありません。 このコンテンツの不一致の場合、 *NDIS 6.20 が動作仕様*を参照してください、 [NDIS 6.20](introduction-to-ndis-6-20.md)についてのドキュメント。

MB サービスが呼び出す NDIS 6.20 が動作で[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)ミニポート ドライバーに問題の OID 要求します。 次のミニポート ドライバーを呼び出す[ **NdisMIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex) MB サービスへのデータを返すにします。

NDIS 6.20 が動作には、次の種類の OID の操作がサポートされています。

-   *設定*ミニポート ドライバーに、サービスからデータを送信する操作。

-   *クエリ*ミニポート ドライバーに、サービスにデータを返すを要求する操作。

-   *メソッド*関数と同等の操作を呼び出すことが両方の入力パラメーターと出力パラメーター。

ミニポート ドライバーを最後に、送信することがあります*兆候*MB デバイスの状態の変化について、サービスに通知するデータを含んでいます。

### <a name="receiving-set-and-query-requests"></a>受信*設定*と*クエリ*要求

MB ミニポート ドライバーを実装して、 [ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)両方に対応する NDIS ハンドラー*設定*と*クエリ*要求。

### <a name="sending-status-indications"></a>状態インジケーターを送信します。

ミニポート ドライバー MB サービスを呼び出すことで状態インジケーターを提供する[ **NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)します。 参照してください、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)状態インジケーターの詳細については、構造体。

### <a name="connection-state-indications"></a>接続状態インジケーター

NDIS 6.20 ミニポート ドライバーを使用する必要があります、 [ **NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state) NDIS およびがあった上にあるドライバーに通知する状態を示す値を転送中の物理的な特性を変更します。

**StatusBuffer**の NDIS メンバー\_状態\_を示す値構造体は、 [ **NDIS\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)構造体は、転送中の物理的な状態を指定します。

MB のミニポート ドライバーでは、NDIS が送信されないようにする必要があります\_状態\_リンク\_状態の状態の表示がないメディアの物理的な状態が変更された場合。 ただし、ミニポート ドライバーは、この状態を示す値を送信することを回避するために必ずしもは必要ありません。

MB のミニポート ドライバーには、現在接続されているデータ クラスのデータの最大レートを報告する必要があります。 接続されているデータ クラスでの変更は、報告された対応するデータ レートで接続状態の表示になる必要があります。 このルールの推奨される実装を次に示します。

1.  この仕様に準拠する MB ミニポート ドライバーを使用する必要があります[ **NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state) NDIS ではなく接続状態の変更を示す\_状態\_メディア\_CONNECT、NDIS\_状態\_メディア\_切断、または NDIS\_状態\_リンク\_速度\_接続状態インジケーターの (NDIS 5.1) のように変更します。

2.  **XmitLinkSpeed**と**RcvLinkSpeed**のメンバー、 [ **NDIS\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)必要があります構造体NDIS を報告しない\_リンク\_速度\_不明です。 ミニポート ドライバーでは、次の表の情報を使用して速度を報告する必要があります。

**GSM ベース MB デバイスの速度のリンク**

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">データ クラス</th>
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
<td align="left"><p>8 を 220 kbps</p></td>
<td align="left"><p>8 を 220 kbps</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UMTS</p></td>
<td align="left"><p>384 を 64 kbps</p></td>
<td align="left"><p>384 を 64 kbps</p></td>
</tr>
<tr class="even">
<td align="left"><p>HSDPA</p></td>
<td align="left"><p>64 を 5.76 mbps</p></td>
<td align="left"><p>1.8 に 14.4 mbps</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HSUPA</p></td>
<td align="left"><p>1.4 を 5.76 mbps</p></td>
<td align="left"><p>7\.2 mbps 64 kbps</p></td>
</tr>
</tbody>
</table>

 

**CDMA ベース MB デバイスの速度のリンク**

| データ クラス     | XmitLinkSpeed            | RcvLinkSpeed            |
|----------------|--------------------------|-------------------------|
| 1 xrtt          | 307.2 kbps に 115.2 kbps | 3 mbps 153.6 kbps    |
| 3xRTT          | 1\.04 mbps 614 kbps    | 1\.04 mbps 307.2 kbps |
| 1xEV-DO        | 153.6 kbps               | 2.4 mbps                |
| 1xEvDO Rev. A. | 1.8 mbps                 | 3.1 mbps                |
| 1xEV-DV        | 1.8 mbps                 | 3.1 mbps                |
| 1xEvDO Rev. B. | 27 mbps                  | 3.1 mbps 73.5 mbps   |

 

**注**  MB デバイスは、前の表に示すように速度の範囲で速度を報告する必要があります。

 

NDIS 5.1 とは異なり、別のリンク状態の変更がないが 1 つの NDIS に統合されます\_状態\_リンク\_NDIS を使用して状態を示す値\_リンク\_状態データ構造体。 NDIS 5.1 インジケーターは、次の表の情報に従って、この構造体にマップできます。 場合は、リンク速度を変更案のコンシューマーがかどうか、リンク速度の変更が発生したかどうかを決定する前は、記録されたものでの送信と受信速度の値を比較する必要があります。

**NDIS 5.1 からの接続状態を示す値マッピング 6.x を**

NDIS 5.1 indication NDIS 6.x NDIS\_リンク\_状態データ構造のパラメーター値の NDIS\_状態\_メディア\_接続

MediaConnectState

MediaConnectStateConnected

NDIS\_状態\_メディア\_切断

MediaConnectState

MediaConnectStateDisconnected

NDIS\_状態\_リンク\_速度\_変更

XmitLinkSpeed

送信速度 (bps)

RcvLinkSpeed

受信速度 (bps)

 

 

 





