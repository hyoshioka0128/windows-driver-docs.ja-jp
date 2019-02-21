---
title: 一般的な統計の Oid
description: 一般的な統計の Oid
ms.assetid: ebdd5723-d913-4c1a-8b1f-f70e4b0080ad
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35fd0aea63406a37355fd12967cbdc510640104e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528324"
---
# <a name="general-statistic-oids"></a>一般的な統計の Oid





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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569656" data-raw-source="[OID_GEN_XMIT_OK](https://msdn.microsoft.com/library/windows/hardware/ff569656)">OID_GEN_XMIT_OK</a></p></td>
<td align="left"><p>エラーなしで送信されたフレーム</p></td>
</tr>
<tr class="even">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569632" data-raw-source="[OID_GEN_RCV_OK](https://msdn.microsoft.com/library/windows/hardware/ff569632)">OID_GEN_RCV_OK</a></p></td>
<td align="left"><p>エラーなしで受信したフレーム</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569654" data-raw-source="[OID_GEN_XMIT_ERROR](https://msdn.microsoft.com/library/windows/hardware/ff569654)">OID_GEN_XMIT_ERROR</a></p></td>
<td align="left"><p>エラーの転送されたフレーム</p></td>
</tr>
<tr class="even">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569629" data-raw-source="[OID_GEN_RCV_ERROR](https://msdn.microsoft.com/library/windows/hardware/ff569629)">OID_GEN_RCV_ERROR</a></p></td>
<td align="left"><p>エラーを受信したフレーム</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569631" data-raw-source="[OID_GEN_RCV_NO_BUFFER](https://msdn.microsoft.com/library/windows/hardware/ff569631)">OID_GEN_RCV_NO_BUFFER</a></p></td>
<td align="left"><p>フレームがなく、バッファーがありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569578" data-raw-source="[OID_GEN_DIRECTED_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569578)">OID_GEN_DIRECTED_BYTES_XMIT</a></p></td>
<td align="left"><p>有向のエラーのない転送バイト数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569580" data-raw-source="[OID_GEN_DIRECTED_FRAMES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569580)">OID_GEN_DIRECTED_FRAMES_XMIT</a></p></td>
<td align="left"><p>エラーなしで送信されたフレームを送信</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569612" data-raw-source="[OID_GEN_MULTICAST_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569612)">OID_GEN_MULTICAST_BYTES_XMIT</a></p></td>
<td align="left"><p>エラーなしで送信されたマルチキャスト バイト数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569614" data-raw-source="[OID_GEN_MULTICAST_FRAMES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569614)">OID_GEN_MULTICAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>エラーなしで送信されたマルチキャスト フレーム</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569440" data-raw-source="[OID_GEN_BROADCAST_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569440)">OID_GEN_BROADCAST_BYTES_XMIT</a></p></td>
<td align="left"><p>エラーなしで送信されたバイトをブロードキャストします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569442" data-raw-source="[OID_GEN_BROADCAST_FRAMES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569442)">OID_GEN_BROADCAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>エラーなしで送信されたフレームをブロードキャストします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569577" data-raw-source="[OID_GEN_DIRECTED_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569577)">OID_GEN_DIRECTED_BYTES_RCV</a></p></td>
<td align="left"><p>エラーなしで受信したバイトを送信</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569579" data-raw-source="[OID_GEN_DIRECTED_FRAMES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569579)">OID_GEN_DIRECTED_FRAMES_RCV</a></p></td>
<td align="left"><p>エラーなしで受信したフレームを送信</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569611" data-raw-source="[OID_GEN_MULTICAST_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569611)">OID_GEN_MULTICAST_BYTES_RCV</a></p></td>
<td align="left"><p>エラーなしで受信したマルチキャスト バイト数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569613" data-raw-source="[OID_GEN_MULTICAST_FRAMES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569613)">OID_GEN_MULTICAST_FRAMES_RCV</a></p></td>
<td align="left"><p>エラーなしで受信したマルチキャスト フレーム</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569439" data-raw-source="[OID_GEN_BROADCAST_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569439)">OID_GEN_BROADCAST_BYTES_RCV</a></p></td>
<td align="left"><p>エラーのない受信バイト数をブロードキャストします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569441" data-raw-source="[OID_GEN_BROADCAST_FRAMES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569441)">OID_GEN_BROADCAST_FRAMES_RCV</a></p></td>
<td align="left"><p>エラーなしで受信したフレームをブロードキャストします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569627" data-raw-source="[OID_GEN_RCV_CRC_ERROR](https://msdn.microsoft.com/library/windows/hardware/ff569627)">OID_GEN_RCV_CRC_ERROR</a></p></td>
<td align="left"><p>循環冗長検査 (CRC) またはフレームを持つ受信フレーム チェック シーケンス (FCS) エラー</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569646" data-raw-source="[OID_GEN_TRANSMIT_QUEUE_LENGTH](https://msdn.microsoft.com/library/windows/hardware/ff569646)">OID_GEN_TRANSMIT_QUEUE_LENGTH</a></p></td>
<td align="left"><p>送信キューの長さ</p></td>
</tr>
</tbody>
</table>

 

 

 





