---
title: SO_RCVBUF
description: SO_RCVBUF
ms.assetid: 218b52ac-95ee-4047-ad75-76d6ae6ab14e
ms.date: 08/08/2017
keywords: -SO_RCVBUF ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ee27d5493475bf6a8cbabd46a3bca144bac299fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373772"
---
# <a name="sorcvbuf"></a>したがって\_RCVBUF


SO\_RCVBUF ソケット オプションは、ソケットのサイズには、基になるトランスポートによって使用されるバッファーの受信を決定します。 このソケット オプションは、リッスンしているソケット、データグラム ソケットでは、接続指向のソケットにのみ適用されます。

このソケット オプションの値を設定する WSK アプリケーションを呼び出す、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)関数は次のパラメーター。

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
<td><p><em>Level</em></p></td>
<td><p>取得</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(ULONG)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>受信バッファーのソケットの新しいサイズを含む ULONG に型指定された変数へのポインター</p></td>
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

SO の値を取得する\_RCVBUF ソケット オプション、WSK アプリケーションを呼び出す、 **WskControlSocket**関数は次のパラメーター。

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
<td><p>受信バッファーのソケットの現在のサイズを受け取る ULONG に型指定された変数へのポインター</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>


呼び出すときに、WSK アプリケーションは IRP へのポインターを指定する必要があります、 **WskControlSocket**などの値を取得または設定する関数\_RCVBUF ソケット オプション。

ソケットの既定のサイズの受信バッファーがトランスポートに固有です。 一部のトランスポートが、このソケット オプションをサポートしていません。

このソケット オプションがリスニング ソケットに設定されている場合、受信バッファーがリスニング ソケットに対して指定されているのと同じサイズに設定があるすべての着信接続をリッスンしているソケットの受け入れられる。 WSK アプリケーションが呼び出すことができます、 **WskControlSocket**で受け入れられたソケット、リッスン ソケットから継承された受信バッファーのサイズをオーバーライドする関数。

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
<td>Ws2def.h (Wsk.h を含む)</td>
</tr>
</tbody>
</table>

 

 




