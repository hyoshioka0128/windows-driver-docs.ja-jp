---
title: SIO_WSK_QUERY_INSPECT_ID
description: SIO_WSK_QUERY_INSPECT_ID
ms.assetid: 6fc3e5ea-61df-47fc-8f79-f9ae272b3544
ms.date: 07/18/2017
keywords:
- SIO_WSK_QUERY_INSPECT_ID ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: d68c55d59af6b4e7a021218042df701a6f0d08b3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841902"
---
# <a name="sio_wsk_query_inspect_id"></a>SIO\_WSK\_クエリ\_\_ID を検査します。


SIO\_WSK\_クエリ\_\_ID ソケット i/o 制御操作を使用すると、WSK アプリケーションは、リッスンしているソケットで正常に受け入れられた接続指向のソケットの検査識別データを照会できます。条件付き受け入れモードが有効になっています。 このソケット i/o 制御操作は、条件付き受け入れモードが有効になっているリスニングソケットで受け入れられた接続指向のソケットにのみ適用されます。

接続指向のソケットの検査識別データを照会するために、WSK アプリケーションは次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

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
<td><p>SIO_WSK_QUERY_INSPECT_ID</p></td>
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
<td><p>sizeof (WSK_INSPECT_ID)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>検査識別データを受け取る WSK_INSPECT_ID 構造体へのポインター</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p><em>Outputbuffer</em>パラメーターによって示されるバッファーにコピーされるデータのバイト数を受け取る、ULONG 型の変数へのポインター。</p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

WSK アプリケーションが**Wskcontrolsocket**関数を呼び出して、条件付き受け入れモードが有効になっているリスニングソケットで受け入れられた接続指向ソケット以外のソケットの検査識別データを照会する場合は、 **WskControlSocket**関数は、デバイス\_要求\_無効\_状態を返します。

条件付きで接続を許可する方法の詳細については、「[受信接続のリッスンと受け入れ](https://docs.microsoft.com/windows-hardware/drivers/network/listening-for-and-accepting-incoming-connections)」を参照してください。

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
<td>Wsk .h (Wsk .h を含む)</td>
</tr>
</tbody>
</table>

 

 




