---
title: REMOTE_NDIS_INITIALIZE_MSG
Description: This message is sent by the host to a Remote NDIS device to initialize the network connection.
ms.assetid: 08735ee8-7a4c-4a3d-9082-27c61cfd15e8
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74da17faed5fa28822ff5098414175bb27f1990c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552378"
---
# <a name="remotendisinitializemsg"></a>リモート\_NDIS\_初期化\_メッセージ


このメッセージは、NDIS リモート デバイスへのホストでネットワーク接続を初期化するために送信されます。 デバイスでリモートの NDIS によって初期化された状態でない場合にのみ、コントロール チャネルを介して送信されます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Offset</th>
<th>サイズ</th>
<th>フィールド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>4</p></td>
<td><p>メッセージの種類</p></td>
<td><p>送信されるメッセージの種類を指定します。 0x00000002 に設定します。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>MessageLength</p></td>
<td><p>メッセージの先頭からこのメッセージの合計の長さ (バイト単位) を指定します。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>RequestId</p></td>
<td><p>リモートの NDIS メッセージの ID 値を指定します。 この値は、デバイスの応答を持つホストによって送信されたメッセージに一致するように使用されます。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>MajorVersion</p></td>
<td><p>ホストによって実装されるリモート NDIS プロトコルのバージョンを指定します。 現在の仕様は RNDIS_MAJOR_VERSION = 1。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>MinorVersion</p></td>
<td><p>ホストによって実装されるリモート NDIS プロトコルのバージョンを指定します。 現在の仕様は RNDIS_MINOR_VERSION = 0。</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>4</p></td>
<td><p>MaxTransferSize</p></td>
<td><p>ホストがデバイスから受信する 1 つのバス データ転送はすべてのバイト単位の最大サイズを指定します。 通常、各 bus データ転送には、1 つのリモートの NDIS メッセージが対応しています。 ただし、デバイスがデータ パケットを 1 つの転送に含めることがいくつかのリモートの NDIS メッセージをバンドル可能性があります (を参照してください<a href="remote-ndis-packet-msg.md" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_PACKET_MSG&lt;/strong&gt;](remote-ndis-packet-msg.md)"> <strong>REMOTE_NDIS_PACKET_MSG</strong></a>)。</p></td>
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
<td><p>バージョン</p></td>
<td><p>Microsoft Windows XP および Windows オペレーティング システムの以降のバージョンで使用できます。 としても使用可能では、Windows 2000 バイナリの再頒布可能パッケージ。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Rndis.h (Rndis.h を含む)</td>
</tr>
</tbody>
</table>

 

 




