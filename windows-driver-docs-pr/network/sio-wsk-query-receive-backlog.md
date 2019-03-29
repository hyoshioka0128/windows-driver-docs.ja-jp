---
title: SIO_WSK_QUERY_RECEIVE_BACKLOG
description: SIO_WSK_QUERY_RECEIVE_BACKLOG
ms.assetid: 5924c6ae-fa9d-4a8c-acbe-65ca0664ad74
ms.date: 07/18/2017
keywords:
- SIO_WSK_QUERY_RECEIVE_BACKLOG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ed4d02617201f39c6ebeb9f98d02ed52069d4edc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579738"
---
# <a name="siowskqueryreceivebacklog"></a>SIO\_WSK\_クエリ\_受信\_バックログ


SIO\_WSK\_クエリ\_受信\_バックログ ソケット I/O 制御操作により、接続指向のソケットの受信データの現在のバックログを照会する WSK アプリケーション。 このソケット I/O 制御操作は、接続指向のソケットだけに適用されます。

WSK アプリケーションがこのソケット I/O 制御操作を使用して、受信バックログ クエリを場合接続指向のソケットがリモートのトランスポート アドレスに接続された後に実行する必要があります。

WSK アプリケーションを呼び出す接続指向のソケットの受信データの現在のバックログを照会、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)関数は次のパラメーター。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>値</th>
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
<td><p><em>レベル</em></p></td>
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
<td><p>受信したデータの現在のバックログを受け取る SIZE_T に型指定された変数へのポインター</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

呼び出すときに、WSK アプリケーションは IRP へのポインターを指定する必要があります、 **WskControlSocket**接続指向のソケットの受信データの現在のバックログ クエリを実行する関数。

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

 

 




