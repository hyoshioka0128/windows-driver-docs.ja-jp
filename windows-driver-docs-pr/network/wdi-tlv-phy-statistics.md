---
title: WDI_TLV_PHY_STATISTICS
description: WDI_TLV_PHY_STATISTICS は、OID_WDI_GET_STATISTICS の PHY ごとの統計を含む TLV です。
ms.assetid: 2F27FF4E-54AC-4518-AEB0-3518FBC8BE0F
ms.date: 07/18/2017
keywords:
- WDI_TLV_PHY_STATISTICS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: e2fb5ee4f611ca6f0a9c0a8863ce4edf23d74902
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844808"
---
# <a name="wdi_tlv_phy_statistics"></a>WDI\_TLV\_PHY\_の統計情報


WDI\_TLV\_PHY\_STATISTICS は、 [OID\_WDI\_の統計](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-statistics)情報の取得に関する、phy ごとの統計を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xA7

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>タスクバーの検索ボックスに</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_phy_type" data-raw-source="[&lt;strong&gt;WDI_PHY_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_phy_type)"><strong>WDI_PHY_TYPE</strong></a></td>
<td>この PHY の型。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 ステーションの IEEE PHY 層が正常に送信した MSDU パケットと MMPDU フレームの数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 ステーションの IEEE PHY 層が正常に送信したマルチキャストまたはブロードキャストの MSDU パケットと MMPDU フレームの数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 IEEE dot11ShortRetryLimit または dot11LongRetryLimit MIB カウンターで定義された再試行の制限を超えたために802.11 ステーションが送信できなかった MSDU パケットと MMPDU フレームの数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>1回または複数回試行した後に802.11 ステーションが正常に送信した MSDU パケットと MMPDU フレームの数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 ステーションが複数の再送信を試行した後に正常に送信した MSDU パケットと MMPDU フレームの数。
<p>MSDU パケットの場合、ポートは、MPDU フラグメントの1つ以上の再送信が必要になった後に正常に送信されたパケットごとに、このカウンターを増やす必要があります。</p></td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>IEEE 802.11 dot11MaxTransmitMSDULifetime MIB オブジェクトで定義されているタイムアウトのために802.11 ステーションが送信できなかった MSDU パケットと MMPDU フレームの数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 ステーションが送信し、受信した 802.11 ACK フレームで受信確認した MPDU フレームの数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>RTS (Request To Send) フレームへの応答として、802.11 ステーションが Clear To Send (CTS) フレームを受信した回数。 これを1つのポートで保持できない場合は、チャネルごとに管理できます。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 ステーションが RTS フレームに応答して CTS フレームを受信しなかった回数。 これを1つのポートで保持できない場合は、チャネルごとに管理できます。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 ステーションが必要とし、受信確認 (ACK) フレームを受信しなかった回数。 これを1つのポートで保持できない場合は、チャネルごとに管理できます。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 ステーションが正常に受信した MSDU パケットと MMPDU フレームの数。
<p>MSDU パケットの場合、ポートは MPDU フラグメントを受信し、フレームチェックシーケンス (FCS) 検証と再生検出を受けたパケットごとに、このカウンターをインクリメントする必要があります。 このポートは、受信した MSDU パケットまたは MPDU フラグメントが MAC レイヤー暗号復号化に失敗したかどうかに関係なく、このメンバーを増やす必要があります。</p></td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 ステーションが正常に受信したマルチキャストまたはブロードキャストの MSDU パケットと MMPDU フレームの数。
<p>MSDU パケットの場合、ポートは MPDU フラグメントを受信し、FCS 検証とリプレイ検出を受けたパケットごとに、このカウンターを増やす必要があります。 このポートは、受信した MSDU パケットまたは MPDU フラグメントが MAC レイヤー暗号復号化に失敗したかどうかに関係なく、このメンバーを増やす必要があります。</p></td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>無作為検出パケットフィルターが有効になっている場合に802.11 ステーションによって受信された MSDU パケットまたは MMPDU フレームの数。 これを1つのポートで保持できない場合は、チャネルごとに管理できます。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>IEEE 802.11 dot11MaxReceiveLifetime MIB オブジェクトで定義されているタイムアウトのために、802.11 ステーションが破棄した MSDU パケットと MMPDU フレームが破棄された場合の数値。 これを1つのポートで保持できない場合は、チャネルごとに管理できます。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 ステーションが受信した複製 MPDU フレームの数。 802.11 ステーションは、802.11 MAC ヘッダーのシーケンス制御フィールドで重複するフレームを決定します。 これを1つのポートで保持できない場合は、チャネルごとに管理できます。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>MSDU パケットまたは MMPDU フレームの802.11 ステーションによって受信された MPDU フレームの数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>無作為検出パケットフィルターが有効になっている場合に、MSDU パケットまたは MMPDU フレームの802.11 ステーションによって受信された MPDU フレームの数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 ステーションが FCS エラーで受信した MPDU フレームの数。 これを1つのポートで保持できない場合は、チャネルごとに管理できます。</td>
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
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 




