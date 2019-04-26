---
title: TCP/IP セグメントの結合規則
description: このセクションでは、ミニポート ドライバーでの TCP/IP セグメントの結合規則を定義します。
ms.assetid: EC3C72EB-20A6-4D48-8E8C-F70EE4483193
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b65e9adced45cbd7a55ca24bbb84ce24005905b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359755"
---
# <a name="rules-for-coalescing-tcpip-segments"></a>TCP/IP セグメントの結合の規則


このセクションでは、セグメント coalescing (RSC) を持つ"を受信するときに指定するルールを定義します。-対応ミニポート ドライバーを特定の TCP 接続のセグメントを結合する必要があります。 規則のいずれかに違反すると、例外が発生すると、し、ミニポート ドライバーは、セグメントの結合を中止する必要があります。

ミニポート ドライバーは、1 つのまとめられた単位 (SCU) の ip アドレスと TCP ヘッダーを更新する必要があります。 ミニポート ドライバーは、SCU 経由で TCP および IPv4 のチェックサムが再計算し、TCP ペイロードをチェーンする必要があります。

次の 2 つのフローチャートの最初の数値では、セグメントの結合と TCP ヘッダーの更新の規則について説明します。 このフローチャートは、有効な重複の Ack およびウィンドウの更新を区別するためのメカニズムを指します。 2 番目のフローチャートでは、これらのメカニズムについて説明します。

これらのフローチャートは、RSC の規則を理解するための参照として提供されます。 ハードウェアの実装は、正確性が保持される限り、フローチャートを最適化できます。

フローチャートで、次の用語が使用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>SEG します。SEQ</strong></p></td>
<td align="left"><p>入力のセグメントのシーケンス番号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>H.SEQ</strong></p></td>
<td align="left"><p>現在追跡されている SCU のシーケンス番号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>SEG.ACK</strong></p></td>
<td align="left"><p>受信のセグメントの受信確認番号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>H.ACK</strong></p></td>
<td align="left"><p>現在追跡されている SCU の受信確認番号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>SEG します。WND</strong></p></td>
<td align="left"><p>受信セグメントによって提供されるウィンドウです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>H.WND</strong></p></td>
<td align="left"><p>現在追跡されている SCU によって提供されるウィンドウです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>SEG.LEN</strong></p></td>
<td align="left"><p>入力のセグメントの TCP ペイロード長。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>H.LEN</strong></p></td>
<td align="left"><p>現在追跡されている SCU の TCP ペイロード長。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>SEG.NXT</strong></p></td>
<td align="left"><p>合計<strong>SEG します。SEQ</strong>と<strong>SEG します。LEN</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>H.NXT</strong></p></td>
<td align="left"><p>合計<strong>H.SEQ</strong>と<strong>H.LEN</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>H.DupAckCount</strong></p></td>
<td align="left"><p>SCU に結合された重複する Ack の数。 この番号は 0 である必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SEG.Tsval</strong></p></td>
<td align="left"><p><strong>タイムスタンプ</strong>受信した現在のセグメントの値。 この値の形式が定義されている<a href="http://www.ietf.org/rfc/rfc1323.txt" data-raw-source="[RFC 1323](http://www.ietf.org/rfc/rfc1323.txt)">RFC 1323</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>H.Tsval</strong></p></td>
<td align="left"><p><strong>タイムスタンプ</strong>現在追跡されている SCU 内の値。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SEG.TSecr</strong></p></td>
<td align="left"><p><strong>タイムスタンプ エコー応答</strong>で受信した現在のセグメント。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>H.TSecr</strong></p></td>
<td align="left"><p><strong>タイムスタンプ エコー応答</strong>現在追跡されている SCU でします。</p></td>
</tr>
</tbody>
</table>

 

![セグメントの結合と tcp ヘッダーの更新の規則を記述するフローチャート](images/rsc-rules1.png)

![有効な重複の ack およびウィンドウの更新を区別するためのメカニズムを示すフローチャート](images/rsc-rules2.png)

フローチャートは、ミニポート ドライバーが ACK 数が異なるセグメントをまとめることがありますを表示します。 ただし、上記の最初のフローチャートで示すように、ミニポート ドライバーは、ACK 番号に関する次の規則に従う必要があります。

-   シーケンス番号の確認を実行した後は、次の条件の一方または両方を満たしている場合に純粋な受信 ACK 現在追跡されている SCU に結合可能性があります。

    -   **H.ACK** == **SEG します。ACK**します。
    -   追跡されている結合されたセグメント内の重複 ACK カウントには 0 です。 つまり、 **H.DupAckCount** 0 を = =。

    つまり、重複した ACK またはウィンドウの更新ではない任意の純粋な ACK は例外をトリガーし、結合しない必要があります。 このようなすべての純粋な Ack は、個々 のセグメントとして指定する必要があります。 この規則により、RSC は、動作や Windows TCP 輻輳制御のアルゴリズムのパフォーマンスには影響しません。

-   入力方向のデータ セグメント (**SEG します。ACK** == **H.ACK**)、受信ピギーバック ACK または (**SEG します。ACK** &gt; **H.ACK**) の両方の次の条件が満たされた場合に、現在追跡されている SCU に結合された可能性があります。

    -   セグメントは、シーケンスの領域で SCU に連続したです。 つまり、 **SEG します。SEQ** == **H.NXT**します。
    -   追跡されている結合されたセグメント内の重複 ACK カウントには 0 です。 つまり、 **H.DupAckCount** 0 を = =。

## <a name="additional-notes-on-duplicate-ack-coalescing"></a>重複する ACK の結合についての注意事項


### <a name="duplicate-ack-behavior"></a>ACK の動作が重複しています

ミニポート ドライバーは、純粋な ACK に相当重複 ACK セグメントを扱う必要があり、合体しません。 この場合は、現在 SCU (あれば) の表示を完了し、個々 のセグメントとして重複 ACK セグメントを示しますにする必要があります。 Windows クライアントでは、既定で選択的受信確認 (SACK) を使用するため、重複した ACK セグメントは例外を生成可能性があります。 参照してください[例の受信 Segment Coalescing](examples-of-receive-segment-coalescing.md)例についてはします。 セグメントと場合、 **DupAckCount** &gt; 0 が示される、NDIS インターフェイスで、RSC が無効になります。

### <a name="handling-duplicate-ack-when-tracking-a-scu-consisting-of-data-segments"></a>データ セグメントから成る SCU を追跡する場合は、重複の確認を処理

SCU を追跡する場合は**H.LEN** &gt; 0 (つまり、まとめられたセグメント データを含む)、次に、その追跡 SCU は次のように終了する必要があります、重複の確認が到着した場合。

1.  重複の確認以降に、新しい SCU を追跡する必要があります。

2.  **DupAckCount**新しい SCU は、0 に設定する必要があります。

3.  **DupAckCount**重複する追加の Ack を受信した場合にインクリメントする必要があります。

この場合、 **DupAckCount** 1 未満の重複する Ack の数になります。 ホストのスタックでは、正しくカウントを処理します。

### <a name="handling-duplicate-ack-when-tracking-a-scu-consisting-of-a-pure-cumulative-ack"></a>純粋な累積的な確認から成る SCU を追跡する場合は、重複の確認を処理

1 つの純粋な累積的な確認 (純粋な確認を複数の結合を禁止する規則) で構成される、SCU を追跡する場合は次に、重複の確認が到着する場合は、 **DupAckCount**追跡 SCU をインクリメントする必要があります。 また重複する追加の Ack を受信した場合もインクリメントする必要があります。 この場合、 **DupAckCount**をひとまとめに重複する Ack の数と等しくなります。

### <a name="when-the-first-segment-that-is-received-in-a-dpc-is-a-duplicate-ack"></a>DPC で受信する最初のセグメントが重複する ACK の場合

ここでは、NIC ことはできませんかを判断、受信したセグメント、ACK が重複しているため、いずれかの状態は保持されません。 セグメントとして扱う純粋 ACK 代わりに次のようにします。

1.  このセグメントで始まる新しい SCU を追跡する必要があります。

2.  **DupAckCount**新しい SCU は、0 に設定する必要があります。

3.  **DupAckCount**を受信した各追加重複の確認を 1 増加する必要があります。

この場合、 **DupAckCount**は重複する Ack の実際の数よりも小さい 1 と等しくなります。 ホストのスタックでは、正しくカウントを処理します。

### <a name="duplicate-ack-exemption"></a>ACK の除外対象が重複しています

ミニポート ドライバーは、純粋な ACK に相当重複 ACK セグメントを扱うし、合体しません可能性があります。 この場合は、現在 SCU (あれば) の表示を完了し、個々 のセグメントとして重複 ACK セグメントを示しますにする必要があります。 Windows クライアントは、既定では、SACK を使用するため、重複した ACK セグメントは例外を生成可能性があります。 例については、次を参照してください。[例の受信 Segment Coalescing](examples-of-receive-segment-coalescing.md)します。 この除外は、ウィンドウの更新プログラムのセグメントには適用されません。

## <a name="coalescing-segments-with-the-timestamp-option"></a>タイムスタンプ オプションを使用してセグメントを結合


TCP タイムスタンプ オプションは、合法的に結合された唯一のオプションです。 このセグメントを結合オプションは、実装に固有の決定事項として残しておきます。 ミニポート ドライバーでは、タイムスタンプのオプションを使用してセグメントを連結は次のフローチャートで説明する規則を従う必要があります。

![tcp タイムスタンプ オプションを使用して結合のセグメントの規則を記述するフローチャート](images/rsc-rules3.png)

**注**  チェック**SEG します。TSval** &gt; =  **H.TSval** TCP シーケンス番号に使用するときと同様の 232 剰余算術演算子を使用して実行する必要があります。 参照してください[RFC 793](http://www.ietf.org/rfc/rfc793.txt)、セクション 3.3 です。

 

設定して、次の帯域外の情報を次のように表示する必要がまとめられたセグメントを指定する際に、 **NetBufferListInfo**のメンバー、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)まとめられたセグメントを記述する構造体。

-   結合されたセグメントの数を格納する必要があります、 **NetBufferListInfo**\[**TcpRecvSegCoalesceInfo**\].**CoalescedSegCount**メンバー。 この数には、結合されたデータのセグメントのみを表します。 ACK の純粋な結合が禁止されているし、ウィンドウの更新プログラムのセグメントは、このフィールドの一部としてカウントされない必要があります。

-   重複の確認数を格納する必要があります、 **NetBufferListInfo**\[**TcpRecvSegCoalesceInfo**\].**DupAckCount**メンバー。 上記の最初のフローチャートは、この値を計算する方法について説明します。

-   タイムスタンプの TCP オプションを持つセグメントが 1 つにまとめ、ときに**NetBufferListInfo**\[**RscTcpTimestampDelta** \]早い絶対デルタが入力される必要がありますまとめられたセグメントのシーケンスに表示される最新の TCP タイムスタンプ値が、SCU を構成します。 SCU 自体には、まとめられたセグメントのシーケンスに表示される最新の TCP タイムスタンプ値を含める必要があります。

**DupAckCount**と**RscTcpTimestampDelta**メンバーは、解釈された場合、および場合にのみ、 **CoalescedSegCount**メンバーが 0 より大きい。 場合、 **CoalescedSegCount** 0 の場合は、セグメントは、非結合以外の RSC セグメントとして扱われます。

内容については、 **NetBufferListInfo** 、メンバーを参照してください[ **NDIS\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff566569)と[ **NDIS\_RSC\_NBL\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451655)します。

PSH ビットまとめられたすべてのセグメントの or 演算があります。 つまり、個々 のセグメントのいずれかで PSH ビットが設定されている場合、ミニポート ドライバーが PSH ビットを SCU でに設定する必要があります。

SCU の最終処理が含まれます。

-   TCP を再計算し、該当する場合、IPv4 のチェックサム。

-   IP ヘッダーの更新」の説明に従って[セグメントの結合の IP ヘッダーを更新](updating-the-ip-headers-for-coalesced-segments.md)します。

-   個々 のセグメントで設定された値と同じにし、TCP IP ヘッダーで ECN bits および ECN フィールドを設定します。

## <a name="handling-tcpip-ipsec-segments"></a>TCP/IP の IPsec のセグメントの処理


ネットワーク カードによって、RSC と IPsec タスク オフロード機能を報告する必要があります。 (を参照してください[、RSC、ネットワーク アダプターの機能を決定する](determining-the-rsc-capabilities-of-a-network-adapter.md))。ただし、IPsec タスク オフロードをサポートしている場合は、IPsec によって保護されているセグメントの結合が試行する必要がありますされません。

 

 





