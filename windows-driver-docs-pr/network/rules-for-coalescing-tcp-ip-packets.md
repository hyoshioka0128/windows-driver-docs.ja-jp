---
title: TCP/IP セグメントを結合するための規則
description: このセクションでは、ミニポートドライバーで TCP/IP セグメントを結合するための規則を定義します。
ms.assetid: EC3C72EB-20A6-4D48-8E8C-F70EE4483193
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6085d3be7961565fb41a8af13bc2cd11181e6d78
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842001"
---
# <a name="rules-for-coalescing-tcpip-segments"></a>TCP/IP セグメントの結合の規則


このセクションでは、受信セグメント合体 (RSC) 対応ミニポートドライバーが特定の TCP 接続のセグメントを結合する必要がある場合に指定するルールを定義します。 いずれかの規則に違反すると、例外が生成され、ミニポートドライバーはセグメントの合体を中止する必要があります。

ミニポートドライバーは、1つの結合されたユニット (SCU) の IP ヘッダーと TCP ヘッダーを更新する必要があります。 ミニポートドライバーは、SCU 経由で TCP および IPv4 チェックサムを再計算し、TCP ペイロードをチェーンする必要があります。

次の2つのフローチャートの最初の例では、セグメントを結合し、TCP ヘッダーを更新するための規則について説明します。 このフローチャートは、有効な重複する Ack とウィンドウの更新を区別するためのメカニズムを示しています。 2番目のフローチャートは、これらのメカニズムについて説明します。

これらのフローチャートは、RSC ルールを理解するための参考資料として提供されています。 ハードウェアの実装では、正確さが維持されている限り、フローチャートを最適化できます。

フローチャートでは、次の用語が使用されます。

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
<td align="left"><p><strong>セグメント.SEQ</strong></p></td>
<td align="left"><p>受信セグメントのシーケンス番号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.H. SEQ</strong></p></td>
<td align="left"><p>現在追跡されている SCU のシーケンス番号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>セグメント.ファクタ</strong></p></td>
<td align="left"><p>受信セグメントの受信確認番号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.H</strong></p></td>
<td align="left"><p>現在追跡されている SCU の受信確認番号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>セグメント.WND</strong></p></td>
<td align="left"><p>受信セグメントによって提供されるウィンドウ。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>WND</strong></p></td>
<td align="left"><p>現在追跡されている SCU によって提供されるウィンドウ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>セグメント.LEN</strong></p></td>
<td align="left"><p>受信セグメントの TCP ペイロードの長さ。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.H</strong></p></td>
<td align="left"><p>現在追跡されている SCU の TCP ペイロードの長さ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>セグメント.NXT</strong></p></td>
<td align="left"><p>SEG の合計<strong>。SEQ</strong>と<strong>SEG。LEN</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.H. NXT</strong></p></td>
<td align="left"><p><strong>SEQ</strong>と<strong>.h</strong>の合計です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-DupAckCount</strong></p></td>
<td align="left"><p>SCU に結合された重複する Ack の数。 この数値は0にする必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>セグメント.Tsval</strong></p></td>
<td align="left"><p>現在受信されているセグメントの<strong>タイムスタンプ</strong>値。 この値の形式は、 <a href="http://www.ietf.org/rfc/rfc1323.txt" data-raw-source="[RFC 1323](http://www.ietf.org/rfc/rfc1323.txt)">RFC 1323</a>で定義されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>.H. Tsval</strong></p></td>
<td align="left"><p>現在追跡されている SCU の<strong>タイムスタンプ</strong>値。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>セグメント.TSecr</strong></p></td>
<td align="left"><p>現在受信されているセグメントの<strong>タイムスタンプエコー応答</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>.H. TSecr</strong></p></td>
<td align="left"><p>現在追跡されている SCU の<strong>タイムスタンプエコー応答</strong>。</p></td>
</tr>
</tbody>
</table>

 

![セグメントを結合し、tcp ヘッダーを更新するための規則を記述するフローチャート](images/rsc-rules1.png)

![有効な重複する ack とウィンドウの更新を区別するためのメカニズムを示すフローチャート](images/rsc-rules2.png)

フローチャートは、ミニポートドライバーが異なる確認番号を持つセグメントを合体する可能性があることを示しています。 ただし、上記の最初のフローチャートに示すように、ミニポートドライバーは、ACK 番号に関する次の規則に従う必要があります。

-   シーケンス番号の確認を実行した後、受信した純粋 ACK が、次のいずれかまたは両方の条件を満たしている場合、現在追跡されている SCU に結合される可能性があります。

    -   ** == ** **SEG。** 確認。
    -   追跡されている結合されたセグメントの重複確認カウントが0です。 言い換えると、「1. **DupAckCount** = = 0」のようになります。

    つまり、重複する ACK またはウィンドウの更新ではない純粋な ACK は、例外をトリガーするため、結合することはできません。 このようなすべての純粋な Ack は、個別のセグメントとして示す必要があります。 この規則により、RSC は Windows TCP 輻輳制御アルゴリズムの動作またはパフォーマンスに影響しません。

-   受信データセグメント (**SEG。ACK** == )、または受信豚によって保証さ**れる Ack (** **SEG。** 次の両方の条件が満たされている場合は、現在追跡されている SCU に ack &gt;) を結合でき**ます。**

    -   セグメントは、シーケンス空間内の SCU に隣接しています。 言い換えると、 **SEG です。SEQ** == . **NXT**。
    -   追跡されている結合されたセグメントの重複確認カウントが0です。 言い換えると、「1. **DupAckCount** = = 0」のようになります。

## <a name="additional-notes-on-duplicate-ack-coalescing"></a>重複する ACK の結合に関する追加の注意事項


### <a name="duplicate-ack-behavior"></a>重複する確認動作

ミニポートドライバーは、純粋な ACK と同等の重複する ACK セグメントを処理し、結合しないようにする必要があります。 この場合は、現在の SCU (存在する場合) を最終処理し、重複する ACK セグメントを個々のセグメントとして示す必要があります。 Windows クライアントでは、既定で選択的受信確認 (SACK) が使用されるため、重複する ACK セグメントでは例外が発生する可能性があります。 例については、「[受信セグメントの結合の例](examples-of-receive-segment-coalescing.md)」を参照してください。 **Dupackcount** &gt; 0 のセグメントが指定されている場合、NDIS はインターフェイスで RSC を無効にします。

### <a name="handling-duplicate-ack-when-tracking-a-scu-consisting-of-data-segments"></a>データセグメントで構成される SCU を追跡するときに重複する ACK を処理する

&gt; 0 (つまり、データを含む結合されたセグメント) を使用して SCU を追跡する場合、重複する ACK が次に到着した場合、追跡 SCU は次の**ように完了**する必要があります。

1.  新しい SCU は、重複する ACK を使用して追跡する必要があります。

2.  新しい SCU の**Dupackcount**は0に設定する必要があります。

3.  追加の重複する Ack を受信した場合は、 **Dupackcount**をインクリメントする必要があります。

この場合、 **Dupackcount**は、重複する ack の数より1小さい値になります。 ホストスタックは、カウントを正しく処理します。

### <a name="handling-duplicate-ack-when-tracking-a-scu-consisting-of-a-pure-cumulative-ack"></a>純粋な累積 ACK で構成される SCU を追跡するときに重複する ACK を処理する

単一の純粋な累積 ACK で構成される SCU を追跡する場合 (複数の純粋な ack の結合を禁止するルール)、重複する ACK が次に到着した場合、追跡 SCU の**Dupackcount**を増やす必要があります。 また、追加の重複する Ack を受信した場合にもインクリメントする必要があります。 この場合、 **Dupackcount**は、結合された重複する ack の数と同じになります。

### <a name="when-the-first-segment-that-is-received-in-a-dpc-is-a-duplicate-ack"></a>DPC で受信した最初のセグメントが、重複する ACK である場合

この場合、NIC は状態を保持していないため、受信したセグメントが重複する ACK であるかどうかを判断できません。 そのため、セグメントは次のように、純粋な ACK として扱う必要があります。

1.  このセグメントから開始して、新しい SCU を追跡する必要があります。

2.  新しい SCU の**Dupackcount**は0に設定する必要があります。

3.  重複する ACK を追加するたびに、 **Dupackcount**を1ずつインクリメントする必要があります。

この場合、 **Dupackcount**は、重複する ack の実際の数より1小さい値になります。 ホストスタックは、カウントを正しく処理します。

### <a name="duplicate-ack-exemption"></a>重複する ACK の除外

ミニポートドライバーは、純粋な ACK と同等の重複する ACK セグメントを処理し、結合しないことがあります。 この場合は、現在の SCU (存在する場合) を最終処理し、重複する ACK セグメントを個々のセグメントとして示す必要があります。 Windows クライアントでは既定で SACK が使用されるため、重複する ACK セグメントでは例外が発生する可能性があります。 例については、「[受信セグメントの結合の例](examples-of-receive-segment-coalescing.md)」を参照してください。 この除外は、ウィンドウの更新セグメントには適用されません。

## <a name="coalescing-segments-with-the-timestamp-option"></a>Timestamp オプションを使用した結合セグメント


TCP タイムスタンプオプションは、合法的に結合できる唯一のオプションです。 このオプションを使用した結合セグメントは、実装固有の決定として残されます。 ミニポートドライバーがタイムスタンプオプションを使用してセグメントを結合する場合は、次のフローチャートに記載されている規則に従う必要があります。

![tcp タイムスタンプオプションを使用してセグメントを結合するための規則を説明するフローチャート](images/rsc-rules3.png)

Check SEG  に**注意**して**ください。TSval** &gt;= は、TCP シーケンス番号に使用されるのと同様に、剰余-232 を使用して**実行する必要**があります。 [RFC 793](http://www.ietf.org/rfc/rfc793.txt)のセクション3.3 を参照してください。

 

結合されたセグメントを示す場合、次の帯域外情報は、結合されたセグメントを記述する[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体の**NetBufferListInfo**メンバーを設定することによって次のように指定する必要があります。

-   結合されたセグメントの数は、 **NetBufferListInfo**\[**TcpRecvSegCoalesceInfo**\]に格納されている必要があります。**CoalescedSegCount**メンバー。 この数値は、結合されたデータセグメントのみを表します。 純粋 ACK の合体は禁止されているため、このフィールドの一部として、ウィンドウの更新セグメントをカウントすることはできません。

-   重複する ACK カウントは、 **NetBufferListInfo**\[**TcpRecvSegCoalesceInfo**\]に保存する必要があります。**Dupackcount**メンバー。 上の最初のフローチャートでは、この値がどのように計算されるかを説明します。

-   TCP timestamp オプションを含むセグメントが結合されている場合、 **NetBufferListInfo**\[**Rsctcpタイムスタンプデルタ**\] には、scu で構成される連結されたセグメントのシーケンスで見られる最も古いと最新の TCP タイムスタンプ値の間の絶対差分を格納する必要があります。 SCU 自体には、結合されたセグメントのシーケンスに見られる最新の TCP タイムスタンプ値を含める必要があります。

**CoalescedSegCount**メンバーが0より大きい場合にのみ、 **Dupackcount**メンバーと**rsctcptimestampdelta**メンバーが解釈されます。 **CoalescedSegCount**がゼロの場合、セグメントは非対応の非 RSC セグメントとして扱われます。

**NetBufferListInfo**メンバーの内容の詳細については、「 [**ndis\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ne-ndis-_ndis_net_buffer_list_info) 」と「 [**ndis\_RSC\_NBL\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_rsc_nbl_info)」を参照してください。

すべての結合されたセグメントでは、PSH ビットを連結する必要があります。 つまり、PSH ビットが個々のセグメントのいずれかに設定されている場合、ミニポートドライバーは SCU で PSH ビットを設定する必要があります。

SCU の最終処理には次のものが含まれます。

-   TCP および (該当する場合) IPv4 チェックサムを計算します。

-   「結合された[セグメントの Ip ヘッダーを更新](updating-the-ip-headers-for-coalesced-segments.md)する」の説明に従って ip ヘッダーを更新します。

-   TCP および IP ヘッダーの ECN のビットおよび ECN フィールドに、個々のセグメントで設定されていたのと同じ値を設定します。

## <a name="handling-tcpip-ipsec-segments"></a>TCP/IP IPsec セグメントの処理


ネットワークカードは、RSC と IPsec タスクオフロードの両方の機能を報告する場合があります。 (「[ネットワークアダプターの RSC 機能の決定](determining-the-rsc-capabilities-of-a-network-adapter.md)」を参照してください)。ただし、IPsec タスクオフロードをサポートしている場合は、IPsec によって保護されているセグメントの結合を試行することはできません。

 

 





