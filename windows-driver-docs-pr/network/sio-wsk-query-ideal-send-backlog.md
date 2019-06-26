---
title: SIO_WSK_QUERY_IDEAL_SEND_BACKLOG
description: SIO_WSK_QUERY_IDEAL_SEND_BACKLOG
ms.assetid: 8d05b1dc-9dbf-4726-9eaf-721d1fb8282e
ms.date: 07/18/2017
keywords:
- SIO_WSK_QUERY_IDEAL_SEND_BACKLOG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c10aabe83f0f2abf9ec71847d72a1b222fd62d0c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379166"
---
# <a name="siowskqueryidealsendbacklog"></a>SIO\_WSK\_クエリ\_理想的な\_送信\_バックログ


SIO\_WSK\_クエリ\_理想的な\_送信\_バックログ ソケット I/O 制御操作により、接続指向のソケットの理想的な送信バックログのサイズを照会する WSK アプリケーション。 このソケット I/O 制御操作は、接続指向のソケットだけに適用されます。

接続指向のソケットの理想的な送信バックログのサイズは (つまり、WSK サブシステムに渡されるがまだ完了していない)、保留状態を維持する必要がある送信データの最適な量を常にすべての完全なソケットのデータのストリームを保持します。 WSK アプリケーションでは、プローブし、基になる接続のフロー制御の状態に基づいて送信されるデータのバッファーをロックを段階的に、このサイズを使用できます。

WSK アプリケーションでは、このソケット I/O 制御操作を使用して、最適な送信バックログのサイズを照会する場合、接続指向のソケットがリモートのトランスポート アドレスに接続された後に実行する必要があります。

WSK アプリケーションを呼び出す接続指向のソケットの理想的な送信バックログのサイズを照会、 [ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)関数は次のパラメーター。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskIoctl</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SIO_WSK_QUERY_IDEAL_SEND_BACKLOG</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof(SIZE_T)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>現在の最適な送信バックログのサイズを受け取る SIZE_T に型指定された変数へのポインター</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

呼び出すときに、WSK アプリケーションは IRP へのポインターを指定する必要があります、 **WskControlSocket**接続指向のソケットの理想的な送信バックログのサイズを照会する関数。

接続指向のソケットは、有効にすると、最適な送信バックログのサイズに対する変更の通知ことができます、 [ *WskSendBacklogEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_send_backlog_event)イベント コールバック関数。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk.h (Wsk.h を含む)</td>
</tr>
</tbody>
</table>

 

 




