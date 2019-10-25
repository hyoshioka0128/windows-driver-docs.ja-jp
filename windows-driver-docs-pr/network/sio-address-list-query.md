---
title: SIO_ADDRESS_LIST_QUERY
description: SIO_ADDRESS_LIST_QUERY
ms.assetid: c50520a3-6ba3-448e-bbb4-bf3425dcbc41
ms.date: 08/08/2017
keywords: -Windows Vista 以降の SIO_ADDRESS_LIST_QUERY ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: c34a4c04696aed1868b5f61686782339b9ed4314
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841915"
---
# <a name="sio_address_list_query"></a>SIO\_ADDRESS\_LIST\_クエリ


SIO\_ADDRESS\_LIST\_QUERY socket i/o control 操作を使用すると、WSK アプリケーションで、ソケットのアドレスファミリのローカルトランスポートアドレスの現在の一覧を照会できます。 このソケット i/o 制御操作は、すべてのソケットの種類に適用されます。

ソケットのアドレスファミリのローカルトランスポートアドレスの現在の一覧を照会するには、WSK アプリケーションが次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

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
<td><p>SIO_ADDRESS_LIST_QUERY</p></td>
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
<td><p><em>Outputbuffer</em>パラメーターによって示されるバッファーのサイズ (バイト単位)。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>ローカルトランスポートアドレスの現在のリストを受け取るバッファーへのポインター。 バッファーのサイズは、 <em>Outputsize</em>パラメーターで指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p><em>Outputbuffer</em>パラメーターによって示されるバッファーにコピーされるデータのバイト数を受け取る、ULONG 型の変数へのポインター。</p></td>
</tr>
</tbody>
</table>

 

WSK アプリケーションは、 **Wskcontrolsocket**関数を呼び出して、ソケットのアドレスファミリのローカルトランスポートアドレスの現在の一覧を照会するときに、IRP へのポインターを指定しません。

**Wskcontrolsocket**関数の呼び出しが成功した場合、出力バッファーにはソケットの[ **\_アドレス\_リスト**](https://docs.microsoft.com/windows/desktop/api/ws2def/ns-ws2def-_socket_address_list)構造が含まれ、その後にソケットのアドレスの各ローカルトランスポートアドレスの SOCKADDR 構造が格納されます。グループ.

**Wskcontrolsocket**関数から STATUS\_BUFFER\_OVERFLOW が返された場合、 *Outputsizereturned*パラメーターによって示される変数には、完全なリストを格納するために必要な出力バッファーサイズ (バイト単位) が含まれます。ソケットのアドレスファミリのローカルトランスポートアドレス。

ソケットのアドレスファミリのローカルトランスポートアドレスの一覧が変更されたときに WSK アプリケーションに通知されるようにするには、 [**SIO\_ADDRESS\_LIST\_CHANGE**](sio-address-list-change.md) socket i/o control 操作を使用します。

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

 

 




