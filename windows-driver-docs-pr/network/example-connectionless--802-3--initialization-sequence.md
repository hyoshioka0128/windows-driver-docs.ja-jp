---
title: コネクションレス (802.3) 初期化シーケンスの例
description: コネクションレス (802.3) 初期化シーケンスの例
ms.assetid: 9625f717-81c3-460b-83e8-c7a86aa85f36
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e0320207ba01037fbb37a84a51f7e99c86c348d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391665"
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570624" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_INITIALIZE_MSG&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570624)"><strong>REMOTE_NDIS_INITIALIZE_MSG</strong></a></p></td>
<td align="left"></td>
<td align="left"><p>ホストは、デバイスにリモートで NDIS 初期化メッセージを送信します。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570621" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_INITIALIZE_CMPLT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570621)"><strong>REMOTE_NDIS_INITIALIZE_CMPLT</strong></a></p></td>
<td align="left"><p>初期化の完全なメッセージをデバイスの応答。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>受信します。 正常な初期化</p></td>
<td align="left"></td>
<td align="left"><p>ホストは、受信データ チャネル上のデータの受け入れを開始します。 (例: USB 上の起動にパイプで読み取りを行っている)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570641" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_QUERY_MSG&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570641)"><strong>REMOTE_NDIS_QUERY_MSG</strong></a></p>
<p>および</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570654" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_SET_MSG&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570654)"><strong>REMOTE_NDIS_SET_MSG</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570638" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_QUERY_CMPLT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570638)"><strong>REMOTE_NDIS_QUERY_CMPLT</strong></a></p>
<p>または</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570651" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_SET_CMPLT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570651)"><strong>REMOTE_NDIS_SET_CMPLT</strong></a></p></td>
<td align="left"><p>ホストは、一連の設定とデバイスの状態を確認し、初期パラメーターを設定するクエリを開始します。 デバイス応答適切に、適切な完了メッセージ。 次の NDIS Oid を照会することがあります。<a href="https://msdn.microsoft.com/library/windows/hardware/ff569069" data-raw-source="[OID_802_3_CURRENT_ADDRESS](https://msdn.microsoft.com/library/windows/hardware/ff569069)">OID_802_3_CURRENT_ADDRESS</a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff569072" data-raw-source="[OID_802_3_MAXIMUM_LIST_SIZE](https://msdn.microsoft.com/library/windows/hardware/ff569072)">OID_802_3_MAXIMUM_LIST_SIZE</a>など。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570654" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_SET_MSG&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570654)"><strong>REMOTE_NDIS_SET_MSG</strong></a></p></td>
<td align="left"></td>
<td align="left"><p>送信ホスト、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff569575" data-raw-source="[OID_GEN_CURRENT_PACKET_FILTER](https://msdn.microsoft.com/library/windows/hardware/ff569575)">OID_GEN_CURRENT_PACKET_FILTER</a> 0 以外のフィルターの値に、デバイスの OID。 この時点でデバイスが受信データ チャネルでのデータ パケットの送信を開始する必要があります。 ホストは、送信データ チャネルでデータ パケットの送信も開始されます。</p></td>
</tr>
</tbody>
</table>

 

 

 





