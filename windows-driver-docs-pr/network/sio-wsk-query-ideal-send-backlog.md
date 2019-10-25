---
title: SIO_WSK_QUERY_IDEAL_SEND_BACKLOG
description: SIO_WSK_QUERY_IDEAL_SEND_BACKLOG
ms.assetid: 8d05b1dc-9dbf-4726-9eaf-721d1fb8282e
ms.date: 07/18/2017
keywords:
- SIO_WSK_QUERY_IDEAL_SEND_BACKLOG ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: e2a50bdcacf4a5f44bd54c97e8f4e9f4703a7606
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841910"
---
# <a name="sio_wsk_query_ideal_send_backlog"></a>SIO\_WSK\_クエリ\_最適\_\_バックログを送信する


SIO\_WSK\_クエリ\_理想的\_送信\_バックログソケット i/o 制御操作により、WSK アプリケーションは、接続指向のソケットの理想的な送信バックログサイズを照会できます。 このソケット i/o 制御操作は、接続指向のソケットにのみ適用されます。

接続指向ソケットの理想的な送信バックログサイズは、未処理のままにしておく必要がある (つまり、WSK サブシステムに渡され、まだ完了していない) 送信データの最適な量で、ソケットのデータストリームが常にいっぱいになるようにします。 WSK アプリケーションでは、このサイズを使用して、基になる接続のフロー制御の状態に基づいて、送信されるデータのバッファーを段階的にプローブおよびロックできます。

WSK アプリケーションがこのソケット i/o 制御操作を使用して理想的な送信バックログサイズを照会する場合は、接続指向のソケットがリモートトランスポートアドレスに接続された後で、この処理を行う必要があります。

接続指向ソケットの理想的な送信バックログサイズを照会するために、WSK アプリケーションは次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

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
<td><p><em>平準</em></p></td>
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
<td><p>sizeof (SIZE_T)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>現在の理想的な送信バックログサイズを受け取る SIZE_T 型の変数へのポインター</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

WSK アプリケーションは、 **Wskcontrolsocket**関数を呼び出して接続指向のソケットの理想的な送信バックログサイズを照会するときに、IRP へのポインターを指定する必要があります。

接続指向のソケットは、 [*WskSendBacklogEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send_backlog_event)イベントコールバック関数を有効にすることで、最適な送信バックログサイズに対する変更を通知できます。

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
<td><p>Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk .h (Wsk .h を含む)</td>
</tr>
</tbody>
</table>

 

 




