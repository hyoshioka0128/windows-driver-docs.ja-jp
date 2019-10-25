---
title: SO_KEEPALIVE
description: SO_KEEPALIVE
ms.assetid: 47b29218-f227-4d36-b206-d8bf009252c0
ms.date: 08/08/2017
keywords: -Windows Vista 以降の SO_KEEPALIVE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 756fea0495579d7ddc7308992db2f0ed77a44206
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841883"
---
# <a name="so_keepalive"></a>\_KEEPALIVE


SO\_KEEPALIVE socket オプションの状態によって、キープアライブパケットが接続指向のソケットで送信されるかどうかが決まります。 このソケットオプションは、リッスンしているソケットと接続指向のソケットにのみ適用されます。

このソケットオプションの状態を設定するために、WSK アプリケーションは次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

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
<td><p>SO_KEEPALIVE</p></td>
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
<td><p>Socket オプションの新しい状態の値を格納する、ULONG 型の変数へのポインター。</p>
<ul>
<li><p>0: キープアライブパケットの送信を無効にします。</p></li>
<li><p>1: キープアライブパケットの送信を有効にします。</p></li>
</ul></td>
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



WSK アプリケーションは、このソケットオプションの状態を取得するために、次のパラメーターを使用して**Wskcontrolsocket**関数を呼び出します。

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
<td><p>SO_KEEPALIVE</p></td>
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
<td><p>ソケットオプションの状態の値を受け取る、ULONG 型の変数へのポインター。</p>
<ul>
<li><p>0: キープアライブパケットの送信が無効になっています</p></li>
<li><p>1: キープアライブパケットの送信が有効になっています</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>


WSK アプリケーションは、 **Wskcontrolsocket**関数を呼び出して、SO\_KEEPALIVE socket オプションの状態を設定または取得するときに、IRP へのポインターを指定する必要があります。

このソケットオプションの既定の状態は、keep-alive パケットの送信が無効になっていることを示します。

このソケットオプションがリッスンソケットで有効になっている場合、そのリッスンソケットで受け入れられるすべての受信接続で、このソケットオプションが既定で有効になります。 WSK アプリケーションは、受け入れられたソケットで**Wskcontrolsocket**関数を呼び出して、リッスンしているソケットから継承されたこのソケットオプションの状態をオーバーライドできます。

Keep-alive パケットは、基になるネットワークトランスポートによって送信されます。 すべてのネットワークトランスポートがキープアライブパケットの送信をサポートしているわけではありません。

Keep-alive パケットの使用方法の詳細については、 *RFC 1122*のセクション4.2.3.6 「」を参照してください。

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

 

 




