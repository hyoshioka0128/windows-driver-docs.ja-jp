---
title: WDI 送信操作とオフロード
description: WDI は、2 つの Tx モード ポート キューと PeerTID キューのいずれかで動作します。
ms.assetid: 9ADBDAD5-4AFA-4AFA-A829-96EB28CEBAA1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30d215fbc9906b339d82d4d734636fb0472eed49
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349543"
---
# <a name="wdi-transmit-operations-and-offloads"></a>WDI 送信操作とオフロード


WDI は、2 つの Tx モードのいずれかで動作します。ポートのキューおよび PeerTID キューします。 ターゲット TargetPriorityQueueing 機能モードの設定 (WDI ポートのキューを = true、false = WDI PeerTID キュー)。

ホストは、次の操作を実行します。

-   TX 分類 (場合にのみ**TargetPriorityQueueing** = false)
-   TX (かポート レベルまたは PeerTID レベルで) キュー
-   (ターゲットにスケジューリング フレームのダウンロード) のスケジュール設定を転送します。
-   ホスト ターゲットの送信フロー制御

次に TX 操作とオフロードの一覧を示します。

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
<th align="left">所有者/該当の負荷を軽減します。</th>
<th align="left">メモ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>高度なプロトコル (タスク) の負荷を軽減します。</p></td>
<td align="left"><p>チェックサムは、LSO します。</p></td>
<td align="left"><p>チェックサムは、起動時の構成可能なオフロードです。 各フレームでは、適用可能なチェックサム演算を指定するフラグには。</p>
<p>WDI は、該当する場合ですか?/ターゲットから透過的に LSO セグメント化を処理します。</p></td>
<td align="left"><p>チェックサム。ターゲット WDI にそのチェックサム オフロード機能の一部として渡すデバイス キャップ bringup 中にします。 機能については、<a href="https://msdn.microsoft.com/library/windows/hardware/ff567878" data-raw-source="[&lt;strong&gt;NDIS_TCP_IP_CHECKSUM_OFFLOAD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567878)"> <strong>NDIS_TCP_IP_CHECKSUM_OFFLOAD</strong></a>を参照してください。</p>
<p>WDI は、該当する場合ですか?/ターゲットから透過的に LSO セグメント化を処理します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>TX 全て</p></td>
<td align="left"><p>802.11 フレーム ヘッダーの適切な型とジェネリック 802.11 ヘッダーを更新/置換します。</p></td>
<td align="left"><p>ターゲット/ですか?</p></td>
<td align="left"><p>フレームの連続する最初のバッファーでは、(ヘッダーの前に、MAC) の先頭に使用可能な領域を持ちます。 この領域は、デバイスのパラメーターで指定された BackfillSize によって決定されます。</p>
<p>非 EAPOL パケットの場合は、最初のバッファーには、MAC および LLC/スナップインのヘッダーがペイロードではありませんが含まれます。 パケットの EAPOL 連続する最初のバッファーには、ペイロードの一部 (またはすべて) を含めることができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>TX 分類</p></td>
<td align="left"><p>TID を確認します。 ユニキャスト RA または DA に基づいて受信者を判断します。</p></td>
<td align="left"><p>WDI 分類を実行するときに<strong>TargetPriorityQueueing</strong>は false です。 WDI が分類を実行していない場合は<strong>TargetPriorityQueueing</strong>は true。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>送信キュー</p></td>
<td align="left"><p>別のキューでのストアの TX フレームです。</p></td>
<td align="left"><p>WDI は、必要な場合に TX フレームをキューします。</p></td>
<td align="left"><p>WDI キュー ポートによって TX フレーム (<strong>TargetPriorityQueueing</strong> = true) または受信者とトラフィックの種類 (記録した、PeerId, TID) (<strong>TargetPriorityQueueing</strong> = false)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>送信フロー制御</p></td>
<td align="left"><p>TIL のオーバーランを回避または TX フレーム バッファーをターゲットします。</p></td>
<td align="left"><p>WDI/TIL/ターゲット</p></td>
<td align="left"><p>ホスト ターゲットのフロー制御のセクションを参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>転送のスケジュール設定</p></td>
<td align="left"><p>複数のバックログ キューがある場合、話してとタイルのフレームを転送元となる送信キューを選択します。</p></td>
<td align="left"><p>WDI キュー TX フレームが必要な場合。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>A MSDU 集計</p></td>
<td align="left"><p>再送信中に維持する必要があります A MSDU 集計にグループ化するフレームを決定します。</p></td>
<td align="left"><p>話して/ターゲット</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>断片化</p></td>
<td align="left"></td>
<td align="left"><p>話して/ターゲット</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>WLAN のスケジュール設定</p></td>
<td align="left"><p>次に転送するトラフィックを送信、および送信するフレームの数を入力受信者を決定します。</p></td>
<td align="left"><p>移行先</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>暗号化</p></td>
<td align="left"><p>セキュリティの種類と受信者 (またはマルチキャストのフレームの送信者) の指定したセキュリティ キーを使用してフレームの内容を暗号化します。 該当する場合は、セキュリティのカプセル化を追加します。</p></td>
<td align="left"><p>移行先</p></td>
<td align="left"><p>FIPS をサポートするシステム、暗号化は、ホスト ソフトウェア内で行われます。 ターゲットの暗号化がバイパスされます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>A MPDU 集計</p></td>
<td align="left"><p>A MPDU 集計にグループと、再送信中に変更できますにフレームを決定します。</p></td>
<td align="left"><p>移行先</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>再試行</p></td>
<td align="left"><p>再送信の MPDUs nacked または受信者がいない確認済みであります。</p></td>
<td align="left"><p>移行先</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="operation-in-host-implemented-fips-mode"></a>Host-Implemented FIPS モードでの操作


ホストは、特定の接続に対して FIPS を提供する場合 (に設定されているホストの FIPS モードで true [ **WDI\_TLV\_接続\_設定**](https://msdn.microsoft.com/library/windows/hardware/dn926261))、ホストは、パケットを暗号化前に、ターゲットに送信します。 ターゲットは、追加の変更、パケットのデータの整合性に影響を与えることがなく、パケットを送信します。 たとえば、ターゲットを実行する必要がありますいないこのモードで MSDU 集計を転送します。

ホスト FIPS モードがより一般的なケースには (ターゲット実装の暗号化モード) が有効になっていない、ヘッダー 802.11 ヘッダーには、暗号化されていないペイロード データが続きます。 パケットが転送前に、暗号化が必要な場合、ターゲットは、パケットを暗号化します。 パケットの QoS 優先順位付けを実行し、TCP レイヤーのオフロード操作 (チェックサム、多数の送信など) を実行できます。 この送信処理のため、ターゲットは、パケットに追加のヘッダーを追加する必要があります (たとえば、QoS、HT ヘッダー、または IV)。

## <a name="tx-encapsulation-population-of-80211-tx-frame-headers"></a>TX カプセル化します。802.11 TX フレーム ヘッダーの作成


ポート (対象デバイス) の 802.11 パケット形式では、ネットワークのデータが送信されます。 送信した各フレームは、802.11 MAC ヘッダーで開始します。 ホストはターゲットが他のフィールドを設定中にはいくつかの MAC ヘッダーのフィールドを設定します。 次の表には、802.11 MAC ヘッダーと暗号ヘッダーのフィールドが、ホストによって設定され、ターゲット デバイスを設定する必要がありますがについて説明します。

<table>
<tr><th>フィールド名</th><th>サブフィールドの名前</th><th colspan="2">ターゲット実装の暗号化モード</th><th colspan="2">FIPS モードのホスト実装</th>
</tr>
    <tr><th></th><th></th><th>ホストにより設定します。</th><th>ターゲット設定します。</th><th>ホストにより設定します。</th><th>ターゲット設定します。</th></tr>
    <tr><td>Frame コントロール</td><td>プロトコルのバージョン</td><td>x</td><td></td><td>x</td><td></td></tr>
    <tr><td>Frame コントロール</td><td>型</td><td>x</td><td></td><td>x</td><td></td></tr>
    <tr><td>Frame コントロール</td><td>サブタイプ</td><td>x</td><td></td><td>x</td><td></td></tr>
    <tr><td>Frame コントロール</td><td>DS に</td><td>x</td><td></td><td>x</td><td></td></tr>
    <tr><td>Frame コントロール</td><td>DS から</td><td>x</td><td></td><td>x</td><td></td></tr>
    <tr><td>Frame コントロール</td><td>複数のフラグメント</td><td>x</td><td></td><td>x</td><td></td></tr>
    <tr><td>Frame コントロール</td><td>再試行</td><td></td><td>x</td><td></td><td>x</td></tr>
    <tr><td>Frame コントロール</td><td>電源管理</td><td></td><td>x</td><td></td><td>x</td></tr>
    <tr><td>Frame コントロール</td><td>多くのデータ</td><td></td><td>x</td><td></td><td>x</td></tr>
    <tr><td>Frame コントロール</td><td>保護されたフレーム</td><td></td><td>x</td><td>x</td><td></td></tr>
    <tr><td>Frame コントロール</td><td>[オーダー]</td><td>x</td><td></td><td>x</td><td></td></tr>
    <tr><td>実行時間と Id</td><td></td><td></td><td>x</td><td></td><td>x</td></tr>
    <tr><td>住所 1</td><td></td><td>x</td><td></td><td>x</td><td></td></tr>
    <tr><td>住所 2</td><td></td><td>x</td><td></td><td>x</td><td></td></tr>
    <tr><td>住所 3</td><td></td><td>x</td><td></td><td>x</td><td></td></tr>
    <tr><td>シーケンス コントロール</td><td>フラグメントの数</td><td>x</td><td></td><td></td><td>x</td></tr>
    <tr><td>シーケンス コントロール</td><td>シーケンス番号</td><td></td><td>x</td><td></td><td>x</td></tr>
    <tr><td>アドレス 4</td><td></td><td>x</td><td></td><td>x</td><td></td></tr>
    <tr><td>QoS 制御</td><td></td><td></td><td>/設定対象で入力追加します。</td><td></td><td>追加/によって設定されます 11n QoS 関連の場合のターゲット。</td></tr>
    <tr><td>HT コントロール</td><td></td><td></td><td>/設定対象で入力追加します。</td><td></td><td>/設定対象で入力追加します。</td></tr>
</table>

## <a name="related-topics"></a>関連トピック


[**NDIS\_TCP\_IP\_チェックサム\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff567878)

[WDI データ転送](wdi-data-transfer.md)

[**WDI\_TLV\_接続\_設定**](https://msdn.microsoft.com/library/windows/hardware/dn926261)

[**WDI\_TXRX\_機能**](https://msdn.microsoft.com/library/windows/hardware/dn898187)

 

 






