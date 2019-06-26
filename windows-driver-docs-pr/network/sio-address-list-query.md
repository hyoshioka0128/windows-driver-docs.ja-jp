---
title: SIO_ADDRESS_LIST_QUERY
description: SIO_ADDRESS_LIST_QUERY
ms.assetid: c50520a3-6ba3-448e-bbb4-bf3425dcbc41
ms.date: 08/08/2017
keywords: -SIO_ADDRESS_LIST_QUERY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: eb204b36ee0a88e7940b3dfb15df0bcb90e0eb2a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380810"
---
# <a name="sioaddresslistquery"></a>SIO\_アドレス\_一覧\_クエリ


SIO\_アドレス\_一覧\_クエリ ソケット I/O 制御操作により、現在、ソケットのアドレス ファミリ用のローカル トランスポート アドレスの一覧を照会する WSK アプリケーション。 このソケット I/O 制御操作は、すべての種類のソケットに適用されます。

WSK アプリケーションを呼び出して、現在、ソケットのアドレス ファミリ用のローカル トランスポート アドレスの一覧を照会するには[ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)関数は次のパラメーター。

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
<td><p>指すバッファーのバイト単位で、サイズ、 <em>OutputBuffer</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>現在のローカル トランスポート アドレスの一覧を受け取るバッファーへのポインター。 バッファーのサイズがで指定された、 <em>OutputSize</em>パラメーター。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>指すバッファーにコピーされたデータのバイト数を受け取る ULONG に型指定された変数へのポインター、 <em>OutputBuffer</em>パラメーター。</p></td>
</tr>
</tbody>
</table>

 

呼び出すときに、WSK アプリケーションが IRP へのポインターを指定しない、 **WskControlSocket**ソケットのアドレス ファミリ用のローカル トランスポート アドレスの現在の一覧を照会する関数。

場合に呼び出し、 **WskControlSocket**関数が成功すると、出力バッファーが含まれています、 [**ソケット\_アドレス\_一覧**](https://docs.microsoft.com/windows/desktop/api/ws2def/ns-ws2def-_socket_address_list)構造体SOCKADDR 構造体、ソケットのアドレス ファミリ用のローカル トランスポート アドレスごとに続きます。

場合、 **WskControlSocket**ステータスを返します\_バッファー\_オーバーフロー、変数を指していますが、 *OutputSizeReturned*パラメーターには、出力バッファーが含まれています。サイズ (バイト単位)、ソケットのアドレス ファミリ用のローカル トランスポート アドレスの完全な一覧を格納するために必要な。

[ **SIO\_アドレス\_一覧\_変更**](sio-address-list-change.md)ソケット I/O 制御操作により、ローカルの一覧への変更があったときに通知する WSK アプリケーションソケットのアドレス ファミリ用のトランスポート アドレス。

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

 

 




