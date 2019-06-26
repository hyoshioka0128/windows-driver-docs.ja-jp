---
title: 一般的な統計情報 OID
description: 一般的な統計情報 OID
ms.assetid: ebdd5723-d913-4c1a-8b1f-f70e4b0080ad
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ba17db14a0fe6374ebc2291bead3c4c8e2de469
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382761"
---
# <a name="general-statistic-oids"></a>一般的な統計情報 OID





次の表は、リモートの NDIS イーサネット デバイスの一般的な統計の Oid を一覧表示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">サポート</th>
<th align="left">OID</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-ok" data-raw-source="[OID_GEN_XMIT_OK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-ok)">OID_GEN_XMIT_OK</a></p></td>
<td align="left"><p>エラーなしで送信されたフレーム</p></td>
</tr>
<tr class="even">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-ok" data-raw-source="[OID_GEN_RCV_OK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-ok)">OID_GEN_RCV_OK</a></p></td>
<td align="left"><p>エラーなしで受信したフレーム</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-error" data-raw-source="[OID_GEN_XMIT_ERROR](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-error)">OID_GEN_XMIT_ERROR</a></p></td>
<td align="left"><p>エラーの転送されたフレーム</p></td>
</tr>
<tr class="even">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-error" data-raw-source="[OID_GEN_RCV_ERROR](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-error)">OID_GEN_RCV_ERROR</a></p></td>
<td align="left"><p>エラーを受信したフレーム</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-no-buffer" data-raw-source="[OID_GEN_RCV_NO_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-no-buffer)">OID_GEN_RCV_NO_BUFFER</a></p></td>
<td align="left"><p>フレームがなく、バッファーがありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-xmit" data-raw-source="[OID_GEN_DIRECTED_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-xmit)">OID_GEN_DIRECTED_BYTES_XMIT</a></p></td>
<td align="left"><p>有向のエラーのない転送バイト数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-xmit" data-raw-source="[OID_GEN_DIRECTED_FRAMES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-xmit)">OID_GEN_DIRECTED_FRAMES_XMIT</a></p></td>
<td align="left"><p>エラーなしで送信されたフレームを送信</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-xmit" data-raw-source="[OID_GEN_MULTICAST_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-xmit)">OID_GEN_MULTICAST_BYTES_XMIT</a></p></td>
<td align="left"><p>エラーなしで送信されたマルチキャスト バイト数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-xmit" data-raw-source="[OID_GEN_MULTICAST_FRAMES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-xmit)">OID_GEN_MULTICAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>エラーなしで送信されたマルチキャスト フレーム</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-xmit" data-raw-source="[OID_GEN_BROADCAST_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-xmit)">OID_GEN_BROADCAST_BYTES_XMIT</a></p></td>
<td align="left"><p>エラーなしで送信されたバイトをブロードキャストします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-xmit" data-raw-source="[OID_GEN_BROADCAST_FRAMES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-xmit)">OID_GEN_BROADCAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>エラーなしで送信されたフレームをブロードキャストします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-rcv" data-raw-source="[OID_GEN_DIRECTED_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-rcv)">OID_GEN_DIRECTED_BYTES_RCV</a></p></td>
<td align="left"><p>エラーなしで受信したバイトを送信</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-rcv" data-raw-source="[OID_GEN_DIRECTED_FRAMES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-rcv)">OID_GEN_DIRECTED_FRAMES_RCV</a></p></td>
<td align="left"><p>エラーなしで受信したフレームを送信</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-rcv" data-raw-source="[OID_GEN_MULTICAST_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-rcv)">OID_GEN_MULTICAST_BYTES_RCV</a></p></td>
<td align="left"><p>エラーなしで受信したマルチキャスト バイト数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-rcv" data-raw-source="[OID_GEN_MULTICAST_FRAMES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-rcv)">OID_GEN_MULTICAST_FRAMES_RCV</a></p></td>
<td align="left"><p>エラーなしで受信したマルチキャスト フレーム</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-rcv" data-raw-source="[OID_GEN_BROADCAST_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-rcv)">OID_GEN_BROADCAST_BYTES_RCV</a></p></td>
<td align="left"><p>エラーのない受信バイト数をブロードキャストします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-rcv" data-raw-source="[OID_GEN_BROADCAST_FRAMES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-rcv)">OID_GEN_BROADCAST_FRAMES_RCV</a></p></td>
<td align="left"><p>エラーなしで受信したフレームをブロードキャストします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-crc-error" data-raw-source="[OID_GEN_RCV_CRC_ERROR](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-crc-error)">OID_GEN_RCV_CRC_ERROR</a></p></td>
<td align="left"><p>循環冗長検査 (CRC) またはフレームを持つ受信フレーム チェック シーケンス (FCS) エラー</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-transmit-queue-length" data-raw-source="[OID_GEN_TRANSMIT_QUEUE_LENGTH](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-transmit-queue-length)">OID_GEN_TRANSMIT_QUEUE_LENGTH</a></p></td>
<td align="left"><p>送信キューの長さ</p></td>
</tr>
</tbody>
</table>

 

 

 





