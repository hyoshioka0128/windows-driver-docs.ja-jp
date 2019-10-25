---
title: WDI 受信操作とオフロード
description: 操作のオフロードの主なカテゴリは構成可能です。MSDU レベルの受信操作フレーム転送 (転送の決定と操作) プロトコル/タスクのオフロード。
ms.assetid: 7D2648BC-05F2-4F75-BA01-E0385C83E0E8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee3060c7b2dd40fed8dfccd65cc3d21f39d689d4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842910"
---
# <a name="wdi-receive-operations-and-offloads"></a>WDI 受信操作とオフロード


操作のオフロードの主なカテゴリは構成可能です。

-   MSDU レベルの受信操作
-   フレームの転送 (意思決定とその転送)
-   プロトコル/タスクのオフロード

RX 操作とオフロードの一覧を次に示します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
<th align="left">所有権</th>
<th align="left">注意</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>暗号化解除</p></td>
<td align="left"><p>送信者に対して指定されたセキュリティの種類とセキュリティキーを使用して、フレームの内容の暗号化を解除します。</p></td>
<td align="left"><p>対象</p></td>
<td align="left"><p>ホストによって実装される FIPS モードでは、ホストソフトウェア内で暗号化解除が行われます。 ターゲットの復号化はバイパスされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>A-MPDU deaggregation</p></td>
<td align="left"><p>RX A-MPDU を個々の Mpdu に分解します。</p></td>
<td align="left"><p>対象</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>A-MSDU deaggregation</p></td>
<td align="left"><p>RX A-MSDU を個々の Msdu に分解します。</p></td>
<td align="left"><p>ターゲット/TAL</p></td>
<td align="left"><p>各 RX MSDU は個別のバッファーに配置されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MSDU セキュリティ decap および de MIC</p></td>
<td align="left"><p>MSDU レベルの MIC を含むセキュリティの種類については、受信した MIC を確認してください。 セキュリティヘッダーとフッターをカプセル化解除します。</p></td>
<td align="left"><p>ターゲット/TAL</p></td>
<td align="left"><p>必要に応じて、オペレーティングシステムが対応策を実行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Rx decap</p></td>
<td align="left"><p>最初の-MSDU subframe の802.11 ヘッダーフィールドを適宜使用して、初期の MSDU サブフレームヘッダーを802.11 ヘッダーに置き換えます。</p></td>
<td align="left"><p>ターゲット/TAL</p></td>
<td align="left"><p>-Msdu deaggregation では、MSDU の初期以外の Msdu には、802.3 ヘッダーが汎用802.11 ヘッダーに置き換えられている必要があります。 WDI は常に802.11 ヘッダーを必要とします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Rx 並べ替えロジック</p></td>
<td align="left"><p>各 RX MPDU に対して、受信する配列の順序を並べ替えるスロットを決定します。 一連の順序付けられた一連のフレームが存在するかどうかを判断します。 前のフレームが到着していない場合でも、保留中のフレームを解放するタイミングを決定します。</p></td>
<td align="left"><p>ターゲット/TAL</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>Rx 破棄ロジック</p></td>
<td align="left"><p>破棄する必要がある Rx フレームを決定します。</p>
<ol>
<li>受信パケットフィルターのいずれにも一致しない場合はです。</li>
<li>フレームが暗号化されている場合は、次の場合に破棄します。
<ul>
<li>暗号化キーを使用してパケットの暗号化を解除することはできません。</li>
<li>パケットペイロードの暗号化解除に失敗しました。</li>
<li>パケットペイロードが MIC 検証に失敗した場合。</li>
<li>このパケットは、暗号アルゴリズム用に定義されている再生メカニズムを使用できません (「Rx PN/replay check」を参照してください)。</li>
<li>プライバシーに関する除外は、 <strong>WDI_EXEMPT_ ALWAYS</strong>アクションを指定するパケットのイーサの種類に対して定義されています。</li>
</ul></li>
<li>フレームが暗号化されていない場合は、次の場合に破棄します。
<ul>
<li>暗号化キーを使用してパケットの暗号化を解除できます。また、 <strong>WDI_EXEMPT_ON_ KEY_UNAVAILABLE</strong> action を指定するパケットの Ethertype に対して、プライバシーの除外が定義されています。</li>
<li>Dot11ExcludeUnencrypted MIB は true に設定されています。</li>
</ul></li>
</ol></td>
<td align="left"><p>Target/TAL は、すべての決定を破棄します。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>Rx PN/replay チェック</p></td>
<td align="left"><p>各 MPDU に、以前の PNs よりも大きい個別のパケット番号があることを確認します。</p></td>
<td align="left"><p>これは必須で、常に有効になります。ただし、順序変更キューに関連付けられているストリームと、キュー管理の順序変更はターゲットに完全にオフロードされません。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>Chatter オフロード</p></td>
<td align="left"><p>遅延が発生する "ノイズ" Rx フレームごとにホストを中断しないようにします。 代わりに、Rx ノイズフレームをグループ化し、1つの割り込みを使用してすべてのフレームを配信します。</p></td>
<td align="left"><p>対象</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>最適化</p></td>
<td align="left"><p>802.11 フラグメントを元の MSDU に再組み立てします。</p></td>
<td align="left"><p>ターゲット/TAL</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>Rx 順序変更キュー</p></td>
<td align="left"><p>フローの前に存在しない MPDUs が到着するまで、順序を満たさない Rx MPDUs を格納します。</p></td>
<td align="left"><p>ターゲット/TAL</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>Rx 破棄の候補</p></td>
<td align="left"><p>ターゲットで実行される Rx 破棄ロジックによってフラグが設定された仕様に基づいて Rx フレームを破棄します。</p></td>
<td align="left"><p>ターゲット/TAL</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>上位レベルのプロトコル (タスク) のオフロード</p></td>
<td align="left"><p>チェックサム</p></td>
<td align="left"><p>チェックサム: 必要に応じて、起動時にオフロードを構成できます。</p></td>
<td align="left"><p>チェックサム: ターゲットは、WDI 中にデバイス cap の一部としてチェックサムオフロード機能を渡します。 機能の詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload" data-raw-source="[&lt;strong&gt;NDIS_TCP_IP_ CHECKSUM_OFFLOAD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)"><strong>NDIS_TCP_IP_ CHECKSUM_OFFLOAD</strong></a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

## <a name="receive-operations-in-host-implemented-fips-mode"></a>ホストを実装する FIPS モードでの受信操作


このモードでは、ターゲットは802.11 ヘッダーまたは802.3 ヘッダーのいずれかを使用して受信フレームを示すことができます。 示す前に、フレームの暗号化を解除しないでください。

破棄ロジックがターゲットにオフロードされる場合、次のいずれかの条件を満たしている場合は、受信したフレームに破棄のマークを付ける必要があります。

-   無効な CRC があるフレーム。
-   フレームが重複しています。
-   構成されているパケットフィルターと一致しないフレーム。

ターゲットは、正常に受信したパケット、またはポートによって破棄されたパケットに対して、適切な MAC と PHY の統計を増やす必要があります。

また、オフロードされた場合は、ターゲットが破棄を実行する必要があります。

ホストによって実装されている FIPS モードで動作している場合、ターゲットは RX パスの802.11 ヘッダーから QoS フラグを削除しないでください。 ターゲットは、QoS ヘッダーを変更せずにフレームを示す必要があります。

フラグメント化されたパケットの場合、ホストが最適化プロセスを実行しているため、LE for FIPS モードによって報告されたペイロードの種類は常に **\_フレーム\_MSDU\_フラグメント**になります。 ただし、FIPS 以外のモードでは、報告されたペイロードの種類は、ターゲット/TAL が最適化を実行しているときに、 **\_FRAME\_MSDU**である必要があります。

## <a name="related-topics"></a>関連トピック


[**NDIS\_TCP\_IP\_チェックサム\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)

[WDI データ転送](wdi-data-transfer.md)

[**WDI\_除外\_アクション\_の種類**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ne-dot11wdi-_wdi_exemption_action_type)

[**WDI\_FRAME\_PAYLOAD\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ne-dot11wdi-_wdi_frame_payload_type)

 

 






