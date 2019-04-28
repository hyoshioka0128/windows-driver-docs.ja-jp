---
title: SO_KEEPALIVE
description: SO_KEEPALIVE
ms.assetid: 47b29218-f227-4d36-b206-d8bf009252c0
ms.date: 08/08/2017
keywords: -接続ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ea6dc1c84d48b2c0daae9e315c8703ed45cbcffb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373776"
---
# <a name="sokeepalive"></a>したがって\_KEEPALIVE


SO の状態\_KEEPALIVE ソケット オプションは、接続指向のソケットで、キープ アライブ パケットが送信されるかどうかを決定します。 このソケット オプションは、リッスン ソケットとの接続指向のソケットにのみ適用されます。

WSK アプリケーションを呼び出すこのソケット オプションの状態を設定する、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)関数は次のパラメーター。

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
<td><p><em>Level</em></p></td>
<td><p>取得</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(ULONG)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>新しいソケット オプションの状態の値を含む ULONG に型指定された変数へのポインター。</p>
<ul>
<li><p>0:キープ アライブ パケットの送信を無効にします。</p></li>
<li><p>1:キープ アライブ パケットの送信を有効にします。</p></li>
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



このソケット オプションの状態を取得するには、WSK アプリケーションが呼び出す、 **WskControlSocket**関数は次のパラメーター。

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
<td><p><em>Level</em></p></td>
<td><p>取得</p></td>
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
<td><p>sizeof(ULONG)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>ソケット オプションの状態の値を受信する ULONG に型指定された変数へのポインター。</p>
<ul>
<li><p>0:キープ アライブ パケットの送信が無効になっています</p></li>
<li><p>1:キープ アライブ パケットの送信が有効になっています。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>


呼び出すときに、WSK アプリケーションは IRP へのポインターを指定する必要があります、 **WskControlSocket**などの状態を取得または設定する関数\_KEEPALIVE ソケット オプション。

このソケット オプションの既定の状態は、キープ アライブ パケットの送信が無効になっていることです。

このソケット オプションは、リスナ ソケットで有効になっている、そのリッスン ソケットの受け入れられるすべての着信接続はこのソケット オプションは既定で有効になっているをあります。 WSK アプリケーションが呼び出すことができます、 **WskControlSocket**で受け入れられたソケット、リッスン ソケットから継承されたこのソケット オプションの状態をオーバーライドする関数。

基になるネットワーク トランスポートがキープ アライブ パケットが送信されます。 すべてのネットワーク トランスポートでは、キープ アライブ パケットの送信をサポートします。

詳細については、キープ アライブ パケットを使用して、次を参照してください。 *RFC 1122*、セクション 4.2.3.6、"TCP Keep-alive"。

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
<td><p>Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ws2def.h (Wsk.h を含む)</td>
</tr>
</tbody>
</table>

 

 




