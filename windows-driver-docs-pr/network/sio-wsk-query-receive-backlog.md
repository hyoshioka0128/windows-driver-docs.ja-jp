---
title: SIO_WSK_QUERY_RECEIVE_BACKLOG
description: SIO_WSK_QUERY_RECEIVE_BACKLOG
ms.assetid: 5924c6ae-fa9d-4a8c-acbe-65ca0664ad74
ms.date: 07/18/2017
keywords:
- SIO_WSK_QUERY_RECEIVE_BACKLOG ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 07896d59c9c2255d2e09bbc325bf5a04dde67f6b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841900"
---
# <a name="sio_wsk_query_receive_backlog"></a>SIO\_WSK\_クエリ\_\_バックログを受信する


SIO\_WSK\_QUERY\_\_バックログソケット i/o 制御操作を使用すると、WSK アプリケーションは、接続指向のソケットに対して受信したデータの現在のバックログを照会できます。 このソケット i/o 制御操作は、接続指向のソケットにのみ適用されます。

WSK アプリケーションがこのソケット i/o 制御操作を使用して受信バックログを照会する場合は、接続指向のソケットがリモートトランスポートアドレスに接続された後で、この処理を実行する必要があります。

接続指向ソケットの受信データの現在のバックログを照会するには、WSK アプリケーションは次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

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
<td><p>SIO_WSK_QUERY_RECEIVE_BACKLOG</p></td>
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
<td><p>受信したデータの現在のバックログを受け取る SIZE_T 型の変数へのポインター</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

WSK アプリケーションは、 **Wskcontrolsocket**関数を呼び出して、接続指向のソケットの受信データの現在のバックログを照会するときに、IRP へのポインターを指定する必要があります。

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

 

 




