---
title: コネクションレス (802.3) 初期化シーケンスの例
description: コネクションレス (802.3) 初期化シーケンスの例
ms.assetid: 9625f717-81c3-460b-83e8-c7a86aa85f36
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 382dbcfa2be4ed91db2b0e4da29f98f4dbb67daf
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393774"
---
# <a name="example-connectionless-8023-initialization-sequence"></a>コネクションレス (802.3) 初期化シーケンスの例





このセクションでは、デバイスがリモートの NDIS コネクションレス デバイスとしての起動時に期待できるイベントの一般的な順序について説明します。 リモートの NDIS の基本的な操作が基になるバスに関係なく同じであるために、require bus 列挙し、起動プロセスを例から除外されています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Host</th>
<th align="left">デバイス</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff570624(v=vs.85)" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_INITIALIZE_MSG&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff570624(v=vs.85))"><strong>REMOTE_NDIS_INITIALIZE_MSG</strong></a></p></td>
<td align="left"></td>
<td align="left"><p>ホストは、デバイスにリモートで NDIS 初期化メッセージを送信します。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff570621(v=vs.85)" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_INITIALIZE_CMPLT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff570621(v=vs.85))"><strong>REMOTE_NDIS_INITIALIZE_CMPLT</strong></a></p></td>
<td align="left"><p>初期化の完全なメッセージをデバイスの応答。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>受信します。 正常な初期化</p></td>
<td align="left"></td>
<td align="left"><p>ホストは、受信データ チャネル上のデータの受け入れを開始します。 (例: USB 上の起動にパイプで読み取りを行っている)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff570641(v=vs.85)" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_QUERY_MSG&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff570641(v=vs.85))"><strong>REMOTE_NDIS_QUERY_MSG</strong></a></p>
<p>および</p>
<p><a href="https://docs.microsoft.com/previous-versions/ff570654(v=vs.85)" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_SET_MSG&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff570654(v=vs.85))"><strong>REMOTE_NDIS_SET_MSG</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff570638(v=vs.85)" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_QUERY_CMPLT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff570638(v=vs.85))"><strong>REMOTE_NDIS_QUERY_CMPLT</strong></a></p>
<p>または</p>
<p><a href="https://docs.microsoft.com/previous-versions/ff570651(v=vs.85)" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_SET_CMPLT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff570651(v=vs.85))"><strong>REMOTE_NDIS_SET_CMPLT</strong></a></p></td>
<td align="left"><p>ホストは、一連の設定とデバイスの状態を確認し、初期パラメーターを設定するクエリを開始します。 デバイス応答適切に、適切な完了メッセージ。 次の NDIS Oid を照会することがあります。<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-current-address" data-raw-source="[OID_802_3_CURRENT_ADDRESS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-current-address)">OID_802_3_CURRENT_ADDRESS</a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-maximum-list-size" data-raw-source="[OID_802_3_MAXIMUM_LIST_SIZE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-maximum-list-size)">OID_802_3_MAXIMUM_LIST_SIZE</a>など。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff570654(v=vs.85)" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_SET_MSG&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff570654(v=vs.85))"><strong>REMOTE_NDIS_SET_MSG</strong></a></p></td>
<td align="left"></td>
<td align="left"><p>送信ホスト、 <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter" data-raw-source="[OID_GEN_CURRENT_PACKET_FILTER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)">OID_GEN_CURRENT_PACKET_FILTER</a> 0 以外のフィルターの値に、デバイスの OID。 この時点でデバイスが受信データ チャネルでのデータ パケットの送信を開始する必要があります。 ホストは、送信データ チャネルでデータ パケットの送信も開始されます。</p></td>
</tr>
</tbody>
</table>

 

 

 





