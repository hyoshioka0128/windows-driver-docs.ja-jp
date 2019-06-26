---
title: SIO_WSK_SET_REMOTE_ADDRESS
description: SIO_WSK_SET_REMOTE_ADDRESS
ms.assetid: 1db11c7a-c9ce-428e-b4da-4a49904a9e4c
ms.date: 07/18/2017
keywords:
- SIO_WSK_SET_REMOTE_ADDRESS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b8fac4433823c57ee465dbbff013e6d739c54bdf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379128"
---
# <a name="siowsksetremoteaddress"></a>SIO\_WSK\_設定\_リモート\_アドレス


SIO\_WSK\_設定\_リモート\_アドレス ソケット I/O 制御操作により、WSK アプリケーションは、データグラム ソケットに対して固定のリモート トランスポート アドレスを指定します。 このソケット I/O 制御操作は、データグラム ソケットだけに適用されます。

WSK アプリケーションでは、データグラム ソケットに対して固定のリモート トランスポート アドレスを設定、ソケット経由で送信されるすべてのデータグラムは、リモートの固定のトランスポート アドレスに送信し、固定リモート トランスポート アドレスから受信したデータグラムのみが受け入れられます。

WSK アプリケーションでは、代替リモート トランスポート アドレスを指定することによって、ソケットを使ってデータグラムを送信するときに、リモートの固定のトランスポート アドレスをオーバーライドする、 *RemoteAddress*パラメーターを呼び出すときに、 [ **WskSendTo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_send_to)関数。 このような状況では、データグラムがリモートの固定のトランスポート アドレスの代わりに代替リモート トランスポート アドレスに送信されます。 ただし、他のリモート転送アドレスから送信されるすべての応答は許容されません。

WSK アプリケーションでは、リモートの固定のトランスポート アドレスを指定するこのソケット I/O 制御操作を使用している場合、データグラム ソケットがローカル トランスポート アドレスにバインドされた後は、する必要があります。

WSK アプリケーションを呼び出して、データグラム ソケットに対して固定のリモート トランスポート アドレスを設定する、 [ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)関数は次のパラメーター。

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
<td><p>SIO_WSK_SET_REMOTE_ADDRESS</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>によって示される SOCKADDR 構造体のサイズ、 <em>InputBuffer</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>データグラム ソケットに対して固定のリモート トランスポート アドレスを指定する構造体へのポインター。 ポインターは、データグラム ソケットが作成されたとき、WSK アプリケーションが指定されているアドレス ファミリに対応する特定の SOCKADDR 構造体の型へのポインターである必要があります。</p></td>
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


データグラム ソケットに対して固定のリモート トランスポート アドレスをクリアする WSK アプリケーションが呼び出す、 **WskControlSocket**関数は次のパラメーター。

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
<td><p>SIO_WSK_SET_REMOTE_ADDRESS</p></td>
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


呼び出すときに、WSK アプリケーションは IRP へのポインターを指定する必要があります、 **WskControlSocket**関数を設定または、データグラム ソケットに対して固定のリモート トランスポート アドレスをクリアします。

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
<td>Wsk.h (Wsk.h を含む)</td>
</tr>
</tbody>
</table>
