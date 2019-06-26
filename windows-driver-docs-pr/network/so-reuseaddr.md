---
title: SO_REUSEADDR
description: SO_REUSEADDR
ms.assetid: 9436492b-0bfb-4234-bcf3-c44657a846d7
ms.date: 08/08/2017
keywords: ・ SO_REUSEADDR ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: db3903e1df36a9896819a4104d358bcfc48258ba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374735"
---
# <a name="soreuseaddr"></a>したがって\_REUSEADDR


SO の状態\_REUSEADDR ソケット オプションは、ソケットをバインドするローカル トランスポート アドレスは常に他のソケットと共有するかどうかを決定します。 このソケット オプションは、リッスンしているソケット、データグラム ソケットでは、接続指向のソケットにのみ適用されます。

WSK アプリケーションでは、このソケット オプションを設定する場合、ローカル トランスポート アドレスにソケットをバインドする前に、実行する必要があります。

WSK アプリケーションを呼び出すこのソケット オプションの状態を設定する、 [ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)関数は次のパラメーター。

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
<td><p>SO_REUSEADDR</p></td>
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
<li><p>0:ローカル トランスポート アドレスを常に共有を無効にします。</p></li>
<li><p>1:ローカル トランスポート アドレスを常に共有を有効にします。</p></li>
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
<td><p>SO_REUSEADDR</p></td>
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
<li><p>0:ローカル トランスポート アドレスを常に共有が無効になっています</p></li>
<li><p>1:ローカル トランスポート アドレスを常に共有が有効になっています。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

呼び出すときに、WSK アプリケーションは IRP へのポインターを指定する必要があります、 **WskControlSocket**などの状態を取得または設定する関数\_REUSEADDR ソケット オプション。

このソケット オプションの既定の状態は、常にローカル トランスポート アドレスを共有が無効になっていることです。

SO を使用しての詳細については\_REUSEADDR ソケット オプションと、ソケットとの間ローカル トランスポート アドレスの共有への影響を参照してください。[トランスポート アドレスを共有](https://docs.microsoft.com/windows-hardware/drivers/network/sharing-transport-addresses)します。

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

 

 




