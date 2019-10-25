---
title: WDI 送信操作とオフロード
description: WDI は、2つの Tx モード (ポートキューと PeerTID キュー) のいずれかで動作します。
ms.assetid: 9ADBDAD5-4AFA-4AFA-A829-96EB28CEBAA1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4af98ed7cd522ccbfa6af30248862c8fc3229a72
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841714"
---
# <a name="wdi-transmit-operations-and-offloads"></a>WDI 送信操作とオフロード


WDI は、ポートキューと PeerTID キューの2つの Tx モードのいずれかで動作します。 ターゲットは、Target優先キュー機能 (true = WDI Port queuing、false = WDI PeerTID queuing) を使用してモードを設定します。

ホストは次の操作を実行します。

-   TX 分類 ( **Target優先キュー**が false の場合のみ)
-   TX キュー (ポートレベルまたは PeerTID レベル)
-   転送スケジュール (ターゲットへのフレームのダウンロードのスケジュール設定)
-   ホスト-ターゲット TX フロー制御

TX 操作とオフロードの一覧を次に示します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">処理手順</th>
<th align="left">説明</th>
<th align="left">所有者/適用可能なオフロード</th>
<th align="left">注意</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>高レベルプロトコル (タスク) のオフロード</p></td>
<td align="left"><p>Checksum、LSO。</p></td>
<td align="left"><p>Checksum は起動時に構成可能なオフロードです。 各フレームには、該当するチェックサム操作を指定するフラグがあります。</p>
<p>WDI は、該当する場合、TAL/Target から透過的に LSO セグメントを処理します。</p></td>
<td align="left"><p>Checksum: ターゲットは、bringup 中にデバイス cap の一部としてチェックサムオフロード機能を WDI するためにパスします。 機能の詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload" data-raw-source="[&lt;strong&gt;NDIS_TCP_IP_CHECKSUM_OFFLOAD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)"><strong>NDIS_TCP_IP_CHECKSUM_OFFLOAD</strong></a>」を参照してください。</p>
<p>WDI は、該当する場合、TAL/Target から透過的に LSO セグメントを処理します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>TX encap</p></td>
<td align="left"><p>Generic 802.11 ヘッダーを更新するか、適切な種類の802.11 フレームヘッダーに置き換えます。</p></td>
<td align="left"><p>ターゲット/TAL</p></td>
<td align="left"><p>フレームの最初の連続するバッファーには、(MAC ヘッダーの前に) 先頭で使用可能な領域があります。 この領域は、デバイスパラメーターに指定された BackfillSize によって決定されます。</p>
<p>EAPOL パケット以外のパケットの場合、最初のバッファーには、MAC ヘッダーとのスナップショットが含まれますが、ペイロードは含まれません。 EAPOL パケットの最初の連続するバッファーには、ペイロードの一部 (またはすべて) を含めることができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>TX 分類</p></td>
<td align="left"><p>TID を決定します。 ユニキャスト RA または DA に基づいて受信者を特定します。</p></td>
<td align="left"><p>WDI は、 <strong>Target優先キュー</strong>が false の場合に分類を実行します。 <strong>TARGETWDI queuing</strong>が true の場合、分類は実行されません。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>TX キュー</p></td>
<td align="left"><p>TX フレームを別のキューに格納します。</p></td>
<td align="left"><p>必要に応じて、WDI は TX フレームをキューに置いています。</p></td>
<td align="left"><p>WDI は、ポート (<strong>Target優先キュー</strong> = true) または受信者とトラフィックの種類 (peerid、TID) によって TX フレームをキューに置いています (<strong>target優先キュー</strong> = false)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>TX フロー制御</p></td>
<td align="left"><p>TX フレームを使用して、TIL またはターゲットバッファーのオーバーランを防止します。</p></td>
<td align="left"><p>WDI/TIL/Target</p></td>
<td align="left"><p>ホストターゲットフロー制御に関するセクションを参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>転送スケジュール</p></td>
<td align="left"><p>バックログされたキューが複数ある場合に、フレームを TAL/TIL に転送する TX キューを選択します。</p></td>
<td align="left"><p>WDI が TX フレームをキューに置いている必要がある場合。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>A-MSDU 集計</p></td>
<td align="left"><p>再転送中に管理する必要がある、MSDU 集計にグループ化するフレームを決定します。</p></td>
<td align="left"><p>TAL/Target</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>最適化</p></td>
<td align="left"></td>
<td align="left"><p>TAL/Target</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>WLAN スケジューリング</p></td>
<td align="left"><p>次に送信する受信者、送信するトラフィックの種類、送信するフレームの数を決定します。</p></td>
<td align="left"><p>対象</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>暗号化</p></td>
<td align="left"><p>受信者 (またはマルチキャストフレームの場合は送信者) に指定されたセキュリティの種類とセキュリティキーを使用して、フレームの内容を暗号化します。 該当する場合は、セキュリティカプセル化を追加します。</p></td>
<td align="left"><p>対象</p></td>
<td align="left"><p>FIPS をサポートするシステムでは、暗号化はホストソフトウェア内で行われます。 ターゲットの暗号化はバイパスされます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>A-MPDU 集計</p></td>
<td align="left"><p>A-MPDU 集計にグループ化するフレームを決定します。これは、再送信中に変更できます。</p></td>
<td align="left"><p>対象</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>再試行</p></td>
<td align="left"><p>受信者によって nacked または確認済みされていない MPDUs を再転送します。</p></td>
<td align="left"><p>対象</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="operation-in-host-implemented-fips-mode"></a>ホスト-実装された FIPS モードでの操作


ホストが特定の接続に対して FIPS を提供している場合 ( [**WDI\_\_\_TLV**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-connection-settings)の [ホスト FIPS モード] が [true] に設定されている場合)、ホストはパケットをターゲットに送信する前に暗号化します。 ターゲットは、パケットのデータの整合性に影響を与える追加の変更を行わずにパケットを転送します。 たとえば、ターゲットでは、このモードでは送信 MSDU 集計を実行できません。

ホスト FIPS モードが有効になっていない一般的なケース (ターゲットで実装された暗号化モード) では、ヘッダー802.11 ヘッダーの後に暗号化されていないペイロードデータが続きます。 パケットが送信前に暗号化を必要とする場合、ターゲットはパケットを暗号化します。 また、パケットの QoS の優先順位付けを行い、TCP レイヤーオフロード操作 (チェックサムや大量の送信など) を実行する場合もあります。 この送信処理では、ターゲットはパケットにヘッダーを追加する必要がある場合があります (QoS、HT ヘッダー、IV など)。

## <a name="tx-encapsulation-population-of-80211-tx-frame-headers"></a>TX カプセル化: 802.11 TX フレームヘッダーの作成


ネットワークデータは、802.11 パケット形式でポート (ターゲットデバイス) に送信されます。 送信された各フレームは、802.11 MAC ヘッダーで始まります。 ホストは MAC ヘッダーの一部のフィールドを設定し、ターゲットは他のフィールドを設定します。 次の表は、802.11 MAC ヘッダーと暗号ヘッダーのどのフィールドがホストによって設定され、ターゲットデバイスによって設定される必要があるかを示しています。

<table>
<tr><th>フィールド名</th><th>サブフィールド名</th><th colspan="2">ターゲット-実装された暗号化モード</th><th colspan="2">ホストに実装された FIPS モード</th>
</tr>
    <tr><th></th><th></th><th>ホストによる設定</th><th>ターゲットによる設定</th><th>ホストによる設定</th><th>ターゲットによる設定</th></tr>
    <tr><td>フレームコントロール</td><td>プロトコルのバージョン</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>フレームコントロール</td><td>タスクバーの検索ボックスに</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>フレームコントロール</td><td>内部</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>フレームコントロール</td><td>DS に</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>フレームコントロール</td><td>DS から</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>フレームコントロール</td><td>その他のフラグメント</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>フレームコントロール</td><td>再試行</td><td></td><td>X</td><td></td><td>X</td></tr>
    <tr><td>フレームコントロール</td><td>Pwr 管理</td><td></td><td>X</td><td></td><td>X</td></tr>
    <tr><td>フレームコントロール</td><td>その他のデータ</td><td></td><td>X</td><td></td><td>X</td></tr>
    <tr><td>フレームコントロール</td><td>保護されたフレーム</td><td></td><td>X</td><td>X</td><td></td></tr>
    <tr><td>フレームコントロール</td><td>[オーダー]</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>期間/Id</td><td></td><td></td><td>X</td><td></td><td>X</td></tr>
    <tr><td>アドレス1</td><td></td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>アドレス2</td><td></td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>アドレス3</td><td></td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>シーケンスコントロール</td><td>フラグメント番号</td><td>X</td><td></td><td></td><td>X</td></tr>
    <tr><td>シーケンスコントロール</td><td>シーケンス番号</td><td></td><td>X</td><td></td><td>X</td></tr>
    <tr><td>アドレス4</td><td></td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>QoS 制御</td><td></td><td></td><td>ターゲットによって追加または設定されます。</td><td></td><td>11n QoS アソシエーションの場合、ターゲットによって追加または設定されます。</td></tr>
    <tr><td>HT コントロール</td><td></td><td></td><td>ターゲットによって追加または設定されます。</td><td></td><td>ターゲットによって追加または設定されます。</td></tr>
</table>

## <a name="related-topics"></a>関連トピック


[**NDIS\_TCP\_IP\_チェックサム\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)

[WDI データ転送](wdi-data-transfer.md)

[**WDI\_TLV\_接続\_の設定**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-connection-settings)

[**WDI\_TXRX\_の機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_txrx_target_capabilities)

 

 






