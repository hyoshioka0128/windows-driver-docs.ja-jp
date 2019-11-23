---
title: SO_WSK_EVENT_CALLBACK
description: SO_WSK_EVENT_CALLBACK
ms.assetid: cb697103-20ef-4667-8823-060a68d904c8
ms.date: 07/18/2017
keywords:
- Windows Vista 以降のネットワークドライバーの SO_WSK_EVENT_CALLBACK
ms.localizationpriority: medium
ms.openlocfilehash: 8630f6f4c041dadae0874f22a2f81f54246bc2b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841878"
---
# <a name="so_wsk_event_callback"></a>\_WSK\_イベント\_コールバック


\_WSK\_EVENT\_CALLBACK socket オプションを使用すると、WSK アプリケーションでソケットのイベントコールバック関数を有効または無効にすることができます。 このソケットオプションは、少なくとも1つのイベントコールバック関数が定義されている拡張インターフェイスを登録した、リッスンしているソケット、データグラムソケット、接続指向ソケット、および基本ソケットにのみ適用されます。

WSK アプリケーションがこのソケットオプションを使用して、リッスンしているソケットまたはデータグラムソケットのイベントコールバック関数を有効または無効にする場合は、ソケットがローカルトランスポートアドレスにバインドされた後で、その処理を行う必要があります。

WSK アプリケーションがこのソケットオプションを使用して、接続指向のソケットでイベントコールバック関数を有効または無効にする場合は、ソケットがリモートトランスポートアドレスに接続された後で、その処理を行う必要があります。

ソケットでイベントコールバック関数を有効または無効にするには、WSK アプリケーションが次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

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
<td><p>SO_WSK_EVENT_CALLBACK</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (WSK_EVENT_CALLBACK_CONTROL)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_event_callback_control" data-raw-source="[&lt;strong&gt;WSK_EVENT_CALLBACK_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_event_callback_control)"><strong>WSK_EVENT_CALLBACK_CONTROL</strong></a>構造体へのポインター</p></td>
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


WSK アプリケーションは、 **Wskcontrolsocket**関数を呼び出して、ソケットでイベントコールバック関数を有効にするときに、IRP へのポインターを指定しません。

WSK アプリケーションでは、必要に応じて、 **Wskcontrolsocket**関数を呼び出して、ソケットでイベントのコールバック関数を無効にするときに、IRP へのポインターを指定できます。

WSK アプリケーションが**Wskcontrolsocket**を呼び出してイベントコールバック関数を無効にすると、wsk サブシステムは次のように動作します。

-   WSK アプリケーションが**Wskcontrolsocket**関数を呼び出したときに無効になっているイベントコールバック関数への呼び出しが実行されていない場合、イベントコールバック関数は無効になり、 **WSKCONTROLSOCKET**関数は状態を返し @no成功します。\_ WSK アプリケーションで IRP が指定されている場合、IRP は成功の状態で完了します。

-   WSK アプリケーションが**Wskcontrolsocket**関数を呼び出し、wsk アプリケーションで IRP が指定されているときに、無効になっているイベントコールバック関数への呼び出しが進行中の場合、 **WSKCONTROLSOCKET**関数は状態\_PENDING を返します。 WSK サブシステムは、イベントコールバック関数を無効にし、イベントコールバック関数に対するすべての実行中の呼び出しが返された後に、IRP を完了します。

-   WSK アプリケーションが**Wskcontrolsocket**関数を呼び出し、wsk アプリケーションで IRP が指定されていない場合に、無効になっているイベントコールバック関数への呼び出しが進行中の場合、 **WSKCONTROLSOCKET**関数は状態を返し\_イベント\_保留中です。 WSK サブシステムは、イベントコールバック関数に対するすべての実行中の呼び出しが返された後に、イベントコールバック関数を無効にします。

任意の標準 WSK イベントコールバック関数を有効または無効にすると、wsk アプリケーションは wsk [ **\_イベント\_コール\_バック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_event_callback_control)の**NpiId**メンバーを wsk ネットワークプログラミングへのポインターに設定します。 [Interface (NPI)](https://docs.microsoft.com/windows-hardware/drivers/network/network-programming-interface) identifier、NPI\_WSK\_インターフェイス\_ID。

拡張インターフェイスのコールバック関数を有効または無効にすると、WSK アプリケーションは WSK\_イベント\_コール\_バックの**NpiId**メンバーを、その拡張機能の NPI 識別子へのポインターに設定します。efi.

イベントコールバック関数を有効にすると、wsk アプリケーションは、WSK ソケットの特定の[カテゴリ](https://docs.microsoft.com/windows-hardware/drivers/network/winsock-kernel-socket-categories)に対して有効なイベントコールバック関数の任意の組み合わせを同時に有効にすることができます。 WSK アプリケーションでは、WSK\_イベント\_コールバック\_制御構造の**Eventmask**メンバーを、次に示すすべてのイベントコールバック関数のイベントフラグのビットごとの or に設定することによって、これらの組み合わせを同時に有効にすることができます。有効になっています。

イベントコールバック関数を無効にする場合、WSK アプリケーションは各イベントコールバック関数を個別に無効にする必要があります。 WSK アプリケーションは、WSK\_イベント\_コールバック\_コントロール構造体の**Eventmask**メンバーを、イベントコールバック関数のイベントフラグのビットごとの or に設定することによって、イベントコールバック関数を無効にします。disabled と WSK\_イベント\_無効にするフラグ。

次の表は、リッスンしているソケットの有効なイベントフラグを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>イベントフラグ</th>
<th>イベントコールバック関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WSK_EVENT_ACCEPT</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event" data-raw-source="[&lt;em&gt;WskAcceptEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event)"><em>WskAcceptEvent</em></a></p></td>
</tr>
</tbody>
</table>


次の表は、データグラムソケットの有効なイベントフラグを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>イベントフラグ</th>
<th>イベントコールバック関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WSK_EVENT_RECEIVE_FROM</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_from_event" data-raw-source="[&lt;em&gt;WskReceiveFromEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_from_event)"><em>WskReceiveFromEvent</em></a></p></td>
</tr>
</tbody>
</table>



次の表は、接続指向のソケットの有効なイベントフラグを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>イベントフラグ</th>
<th>イベントコールバック関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WSK_EVENT_DISCONNECT</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_disconnect_event" data-raw-source="[&lt;em&gt;WskDisconnectEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_disconnect_event)"><em>Wsk切断イベント</em></a></p></td>
</tr>
<tr class="even">
<td><p>WSK_EVENT_RECEIVE</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event" data-raw-source="[&lt;em&gt;WskReceiveEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event)"><em>WskReceiveEvent</em></a></p></td>
</tr>
<tr class="odd">
<td><p>WSK_EVENT_SEND_BACKLOG</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send_backlog_event" data-raw-source="[&lt;em&gt;WskSendBacklogEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send_backlog_event)"><em>WskSendBacklogEvent</em></a></p></td>
</tr>
</tbody>
</table>


リッスンソケットは、リッスンしているソケットによって受け入れられる接続指向のソケットに対して、イベントコールバック関数を自動的に有効にすることができます。 WSK アプリケーションは、リッスンしているソケットで接続指向のソケットイベントコールバック関数を有効にすることで、これらのコールバック関数を自動的に有効にします。 イベントコールバック関数は、ソケットがリッスンソケットの[*Wskacceptevent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event)イベントコールバック関数によって受け入れられる場合にのみ、受け入れられた接続指向ソケットで自動的に有効になります。 接続指向ソケットがリッスンソケットの[**Wskaccept**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept)関数によって受け入れられる場合、受け入れられるソケットのイベントコールバック関数は自動的に有効になりません。

接続指向のイベントコールバック関数がリッスンソケットで有効になった後は、リッスンしているソケットで無効にすることはできません。 *Wskacceptevent*イベントのコールバック関数が無効になっていて、リッスンしているソケットで再度有効になった場合、そのリスニングソケットで最初に有効にされた接続指向のイベントコールバック関数はすべて、引き続き適用されます。*Wskacceptevent*イベントコールバック関数によって受け入れられる接続指向ソケット。

ソケットのイベントコールバック関数の有効化と無効化の詳細については、「[イベントコールバック関数の有効化と無効化](https://docs.microsoft.com/windows-hardware/drivers/network/enabling-and-disabling-event-callback-functions)」を参照してください。

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

 

 




