---
title: SO_EXCLUSIVEADDRUSE
description: SO_EXCLUSIVEADDRUSE
ms.assetid: d281086f-4d8b-4e1e-b2bd-7b0a20338222
ms.date: 08/08/2017
keywords: -SO_EXCLUSIVEADDRUSE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 487a9c2557341cfb7eba1b6fddc414ccf3b0677c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376412"
---
# <a name="soexclusiveaddruse"></a>したがって\_EXCLUSIVEADDRUSE


SO の状態\_EXCLUSIVEADDRUSE ソケット オプションは、ソケットが使用するソケットをバインドするローカル トランスポート アドレスが予約されている排他的かどうかを判断します。 このソケット オプションは、リッスンしているソケット、データグラム ソケットでは、接続指向のソケットにのみ適用されます。

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
<td><p>SO_EXCLUSIVEADDRUSE</p></td>
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
<p>0:ローカル トランスポート アドレスを排他的に使用を無効にします。</p>
<p>1:ローカル トランスポート アドレスを排他的に使用を有効にします。</p></td>
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
<td><p>SO_EXCLUSIVEADDRUSE</p></td>
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
<p>0:ローカル トランスポート アドレスを排他的に使用が無効になっています</p>
<p>1:ローカル トランスポート アドレスを排他的に使用が有効になっています。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>


呼び出すときに、WSK アプリケーションは IRP へのポインターを指定する必要があります、 **WskControlSocket**などの状態を取得または設定する関数\_EXCLUSIVEADDRUSE ソケット オプション。

このソケット オプションの既定の状態は、排他的に使用してローカル トランスポート アドレスが無効になっていることです。

SO を使用しての詳細については\_EXCLUSIVEADDRUSE ソケット オプションと、ソケットとの間ローカル トランスポート アドレスの共有への影響を参照してください。[トランスポート アドレスを共有](https://docs.microsoft.com/windows-hardware/drivers/network/sharing-transport-addresses)します。

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

 

 




