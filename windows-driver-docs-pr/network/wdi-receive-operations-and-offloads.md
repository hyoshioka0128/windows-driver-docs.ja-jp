---
title: WDI 受信操作とオフロード
description: 操作のオフロードのこれらの主なカテゴリは、構成できます。MSDU レベルでは、プロトコル/タスク オフロード (転送の決定と作動) を転送 operationsFrame を受信します。
ms.assetid: 7D2648BC-05F2-4F75-BA01-E0385C83E0E8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46e307638dcbfdd6648a801560c2eb1b3f86d62f
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463787"
---
# <a name="wdi-receive-operations-and-offloads"></a>WDI 受信操作とオフロード


操作のオフロードのこれらの主なカテゴリは、構成できます。

-   受信操作で MSDU レベル
-   (転送意思決定および作動) フレームの転送
-   プロトコル/タスク オフロード

次に RX 操作とオフロードの一覧を示します。

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
<th align="left">メモ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>暗号化解除</p></td>
<td align="left"><p>セキュリティの種類と、送信者に指定したセキュリティ キーを使用してフレーム内のコンテンツを復号化します。</p></td>
<td align="left"><p>移行先</p></td>
<td align="left"><p>ホスト実装の FIPS モードでは、復号化は、ホスト ソフトウェア内で行われます。 ターゲットの暗号化解除がバイパスされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>A MPDU deaggregation</p></td>
<td align="left"><p>個々 の MPDUs RX A MPDU に分解します。</p></td>
<td align="left"><p>移行先</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>A MSDU deaggregation</p></td>
<td align="left"><p>個々 の MSDUs RX A MSDU に分解します。</p></td>
<td align="left"><p>ターゲット/ですか?</p></td>
<td align="left"><p>各 RX MSDU は、別のバッファーに格納されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MSDU セキュリティ decap de MIC と</p></td>
<td align="left"><p>MSDU レベル MIC に関連するセキュリティの種類、受信した MIC を確認します。 カプセル化解除、セキュリティ ヘッダーとフッターです。</p></td>
<td align="left"><p>ターゲット/ですか?</p></td>
<td align="left"><p>オペレーティング システムは、必要な場合の対策を実行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Rx decap します。</p></td>
<td align="left"><p>非初期 A MSDU subframe ヘッダーを適切な初期 A MSDU subframe から 802.11 ヘッダー フィールドを使用して、802.11 ヘッダーに置き換えます。</p></td>
<td align="left"><p>ターゲット/ですか?</p></td>
<td align="left"><p>A MSDU deaggregation、中には、A MSDU の非初期 MSDUs には、汎用の 802.11 ヘッダーに置き換え、802.3 ヘッダーが必要があります。 WDI は、802.11 ヘッダーを常に要求します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Rx の並べ替えロジック</p></td>
<td align="left"><p>各 RX MPDU になった配列の並べ替え Rx のスロットを決定します。 一連の順序でフレームが存在する場合を決定します。 前のフレームが到着していない場合でも保留中のフレームを解放する時期を決定します。</p></td>
<td align="left"><p>ターゲット/ですか?</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>Rx の破棄ロジック</p></td>
<td align="left"><p>破棄されるどの Rx フレームの必要性を確認します。</p>
<ol>
<li>場合は、受信パケット フィルターが一致しません。</li>
<li>場合は、フレームが暗号化されている場合を破棄します。
<ul>
<li>暗号キーは、パケットの暗号化を解除するご利用いただけません。</li>
<li>パケットのペイロードは、正常に復号化に失敗します。</li>
<li>パケットのペイロードでは、MIC 検証が失敗します。</li>
<li>パケットが定義されている暗号アルゴリズムの再生のメカニズム (Rx PN/再生確認を参照してください)。</li>
<li>指定するパケットのイーサ型のプライバシーの除外対象が定義されている、<strong>常に WDI_EXEMPT_</strong>アクション。</li>
</ul></li>
<li>場合は、フレームが暗号化されていない場合を破棄します。
<ul>
<li>暗号キーは、パケットを復号化に使用できるとプライバシーの除外対象を指定するパケットの Ethertype が定義されている、 <strong>WDI_EXEMPT_ON_ KEY_UNAVAILABLE</strong>アクション。</li>
<li>Dot11ExcludeUnencrypted MIB の設定を true にします。</li>
</ul></li>
</ol></td>
<td align="left"><p>すべてのターゲット/話してでは、意思決定を破棄します。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>Rx PN/再生チェック</p></td>
<td align="left"><p>各 MPDU に PNs が以前よりも大きいが個別のパケット数がいることを確認します。</p></td>
<td align="left"><p>これは、並べ替えのキューに関連付けられているストリームを除く、必須で、常に有効になっているオフロードし、キュー管理の並べ替えが完全にオフロードされず、ターゲットにします。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>Chatter オフロード</p></td>
<td align="left"><p>Rx フレームごとに遅延可能な「ノイズ」ホストを中断しないようにします。 代わりに、Rx ノイズのフレームをグループ化し、1 つの割り込みを使用して、このようなすべてのフレームを配信します。</p></td>
<td align="left"><p>移行先</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>最適化</p></td>
<td align="left"><p>802.11 フラグメントの元の MSDU に再構成します。</p></td>
<td align="left"><p>ターゲット/ですか?</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>Rx 並べ替えキュー</p></td>
<td align="left"><p>フローから不足している以前 MPDUs が到着するまでは、順序の Rx MPDUs を格納します。</p></td>
<td align="left"><p>ターゲット/ですか?</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>Rx 破棄作動</p></td>
<td align="left"><p>Rx 破棄のロジックが、ターゲットで実行してフラグが設定された仕様に基づく Rx フレームを破棄します。</p></td>
<td align="left"><p>ターゲット/ですか?</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>高度なプロトコル (タスク) の負荷を軽減します。</p></td>
<td align="left"><p>チェックサム</p></td>
<td align="left"><p>チェックサム。起動時に必要な場合にオフロードを構成できます。</p></td>
<td align="left"><p>チェックサム。ターゲットそのチェックサム オフロード機能の一部として渡すデバイス キャップ WDI に持ち込むアップ時にします。 機能の詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567878" data-raw-source="[&lt;strong&gt;NDIS_TCP_IP_ CHECKSUM_OFFLOAD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567878)"> <strong>NDIS_TCP_IP_ CHECKSUM_OFFLOAD</strong></a>します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="receive-operations-in-host-implemented-fips-mode"></a>Host-Implemented FIPS モードで受信操作


このモードで、ターゲットは、802.11 ヘッダーまたは 802.3 のヘッダーのいずれかで受信したフレームを示す場合があります。 表示する前に、フレームを解読できません必要があります。

破棄ロジックは、ターゲットにオフロードは場合、次の条件を満たしている場合、破棄の受信のフレームをマークする必要があります。

-   不適切な CRC があるフレーム。
-   フレームが重複しています。
-   構成済みのパケット フィルターと一致しないフレームです。

ターゲットは、適切なは、正常に受信したか、ポートによって破棄されたパケットの MAC および PHY 統計情報を増やす必要があります。

さらに、オフロードされた場合は、ターゲットは破棄作動を実行する必要があります。

ターゲットがホスト実装の FIPS モードで動作している場合、802.11 ヘッダーから QoS フラグを RX パスにストリップいない必要があります。 ターゲットは、QoS のヘッダーを変更することがなく、フレームを示す必要があります。

断片化されたパケットの場合は、ペイロードの種類によって報告された、LE FIPS モードが常に**WDI\_フレーム\_MSDU\_フラグメント**ホストは、最適化プロセスを行うことができます。 ただし、非 FIPS モードで、報告されるペイロードの種類は**WDI\_フレーム\_MSDU**ターゲット/話してが最適化を実行するとします。

## <a name="related-topics"></a>関連トピック


[**NDIS\_TCP\_IP\_チェックサム\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff567878)

[WDI データ転送](wdi-data-transfer.md)

[**WDI\_除外\_アクション\_型**](https://msdn.microsoft.com/library/windows/hardware/dn897820)

[**WDI\_フレーム\_ペイロード\_型**](https://msdn.microsoft.com/library/windows/hardware/dn897831)

 

 






