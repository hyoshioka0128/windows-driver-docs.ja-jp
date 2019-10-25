---
title: SO_RCVBUF
description: SO_RCVBUF
ms.assetid: 218b52ac-95ee-4047-ad75-76d6ae6ab14e
ms.date: 08/08/2017
keywords: -Windows Vista 以降の SO_RCVBUF ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: f5d3f0aa519cabf2ca6abea464894258c8b1de66
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841884"
---
# <a name="so_rcvbuf"></a>RCVBUF\_


SO\_RCVBUF socket オプションは、基になるトランスポートが使用するソケットの受信バッファーのサイズを決定します。 このソケットオプションは、リッスンしているソケット、データグラムソケット、および接続指向のソケットにのみ適用されます。

このソケットオプションの値を設定するために、WSK アプリケーションは次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

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
<td><p><strong>WskSetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_RCVBUF</p></td>
</tr>
<tr class="odd">
<td><p><em>平準</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (ULONG)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>ソケットの受信バッファーの新しいサイズを格納する、ULONG 型の変数へのポインター。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

RCVBUF socket オプション\_の値を取得するために、WSK アプリケーションは次のパラメーターを使用して**Wskcontrolsocket**関数を呼び出します。

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
<td><p><strong>WskGetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_RCVBUF</p></td>
</tr>
<tr class="odd">
<td><p><em>平準</em></p></td>
<td><p>SOL_SOCKET</p></td>
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
<td><p>sizeof (ULONG)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>ソケットの受信バッファーの現在のサイズを受け取る、ULONG 型の変数へのポインター</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>


WSK アプリケーションは、 **Wskcontrolsocket**関数を呼び出して、SO\_RCVBUF socket オプションの値を設定または取得するときに、IRP へのポインターを指定する必要があります。

ソケットの受信バッファーの既定のサイズは、トランスポートに固有です。 一部のトランスポートでは、このソケットオプションがサポートされていない可能性があります。

このソケットオプションがリッスンソケットに設定されている場合、そのリッスンソケットで受け入れられるすべての受信接続には、リッスンしているソケットに対して指定されたのと同じサイズの受信バッファーが設定されます。 WSK アプリケーションは、受け入れられたソケットで**Wskcontrolsocket**関数を呼び出して、リッスンしているソケットから継承された受信バッファーのサイズをオーバーライドできます。

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
<td>Ws2def (Wsk .h を含む)</td>
</tr>
</tbody>
</table>

 

 




