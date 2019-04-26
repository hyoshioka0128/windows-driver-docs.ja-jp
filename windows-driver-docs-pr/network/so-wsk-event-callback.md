---
title: SO_WSK_EVENT_CALLBACK
description: SO_WSK_EVENT_CALLBACK
ms.assetid: cb697103-20ef-4667-8823-060a68d904c8
ms.date: 07/18/2017
keywords:
- SO_WSK_EVENT_CALLBACK ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: cb01680ab134812a027a8b3ddd0a01bd3c4ce4b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349342"
---
# <a name="sowskeventcallback"></a>したがって\_WSK\_イベント\_コールバック


SO\_WSK\_イベント\_コールバック ソケット オプションにより、WSK アプリケーションを有効にし、ソケットのイベントのコールバック関数を無効にします。 このソケット オプションは、リッスン ソケット、データグラム ソケット、接続指向のソケット、および少なくとも 1 つのイベントのコールバック関数が定義されている拡張機能インターフェイスに登録されている基本的なソケットにのみ適用されます。

WSK アプリケーションでは、待機中のソケットまたはデータグラム ソケットでのイベントのコールバック関数を有効またはこのソケット オプションを使用している場合、ソケットがローカル トランスポート アドレスにバインドされた後は、する必要があります。

WSK アプリケーションでは、接続指向のソケットでのイベントのコールバック関数を有効またはこのソケット オプションを使用している場合、ソケットがリモートのトランスポート アドレスに接続された後は、する必要があります。

WSK アプリケーションの呼び出しを有効にまたはソケットでのイベントのコールバック関数を無効にする、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)関数は次のパラメーター。

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
<td><p>取得</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(WSK_EVENT_CALLBACK_CONTROL)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>ポインターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff571166" data-raw-source="[&lt;strong&gt;WSK_EVENT_CALLBACK_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571166)"> <strong>WSK_EVENT_CALLBACK_CONTROL</strong> </a>構造体</p></td>
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


呼び出すときに、WSK アプリケーションが IRP へのポインターを指定しない、 **WskControlSocket**ソケットでのイベントのコールバック関数を有効にする関数。

WSK アプリケーションを必要に応じて指定できます IRP へのポインターを呼び出すときに、 **WskControlSocket**ソケットでのイベントのコールバック関数を無効にする関数。

WSK アプリケーションを呼び出すと**WskControlSocket** WSK サブシステムを次のように動作をコールバック関数がイベントを無効にします。

-   WSK アプリケーション呼び出すときに無効化されるイベントのコールバック関数の実行中の呼び出しがないかどうか、 **WskControlSocket**関数、イベントのコールバック関数が無効になっていると、 **WskControlSocket**ステータスを返します\_成功します。 WSK アプリケーションでは、IRP を指定する場合は、成功の状態で IRP が完了しました。

-   進行中、WSK アプリケーションが無効化されるイベントのコールバック関数への呼び出しがあるかどうか、 **WskControlSocket**関数と WSK アプリケーションは、IRP を指定、 **WskControlSocket**ステータスを返します\_保留します。 WSK サブシステムは、イベントのコールバック関数を無効にし、イベントのコールバック関数へのすべての実行中の呼び出しが返された後、IRP を完了します。

-   進行中、WSK アプリケーションが無効化されるイベントのコールバック関数への呼び出しがあるかどうか、 **WskControlSocket**関数と WSK アプリケーション、IRP を指定しなかった、 **WskControlSocket**ステータスを返します\_イベント\_保留します。 WSK サブシステムには、イベントのコールバック関数へのすべての実行中の呼び出しが返された後のイベントのコールバック関数が無効にします。

WSK アプリケーションの設定を有効にするか、標準 WSK イベントのコールバック関数のいずれかを無効にすると、ときに、 **NpiId**のメンバー、 [ **WSK\_イベント\_コールバック\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff571166)構造体、WSK へのポインターを[ネットワーク プログラミング インターフェイス (NPI)](https://msdn.microsoft.com/library/windows/hardware/ff568373)識別子、NPI\_WSK\_インターフェイス\_id。

WSK アプリケーションの設定を有効にするか、拡張機能インターフェイスの任意のコールバック関数を無効にすると、ときに、 **NpiId** 、WSK のメンバー\_イベント\_コールバック\_NPI へのポインターへの制御構造その拡張機能インターフェイスの識別子。

WSK アプリケーションことができます、特定の有効なイベントのコールバック関数の任意の組み合わせを有効に同時にイベントのコールバック関数を有効にすると、[カテゴリ](https://msdn.microsoft.com/library/windows/hardware/ff571093)WSK ソケットの。 WSK アプリケーションは同時に設定してこれらの組み合わせを有効、**使う**、WSK のメンバー\_イベント\_コールバック\_制御構造のすべてのイベント フラグのビットごとの OR を有効になっているされているイベントのコールバック関数。

イベントのコールバック関数を無効にすると、WSK アプリケーションする必要がありますを無効にしない各イベントのコールバック関数個別にします。 WSK アプリケーションを個別に無効にしますしないイベントのコールバック関数を設定して、**使う**、WSK のメンバー\_イベント\_コールバック\_制御構造のイベント フラグのビットごとの OR をイベントのコールバック関数は無効にされていると、WSK\_イベント\_無効にするフラグ。

次の表では、リッスン ソケットの有効なイベント フラグを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>イベント フラグ</th>
<th>イベントのコールバック関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WSK_EVENT_ACCEPT</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571120" data-raw-source="[&lt;em&gt;WskAcceptEvent&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571120)"><em>WskAcceptEvent</em></a></p></td>
</tr>
</tbody>
</table>


次の表では、データグラム ソケットの有効なイベント フラグを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>イベント フラグ</th>
<th>イベントのコールバック関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WSK_EVENT_RECEIVE_FROM</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571142" data-raw-source="[&lt;em&gt;WskReceiveFromEvent&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571142)"><em>WskReceiveFromEvent</em></a></p></td>
</tr>
</tbody>
</table>



次の表では、接続指向のソケットの有効なイベント フラグを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>イベント フラグ</th>
<th>イベントのコールバック関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WSK_EVENT_DISCONNECT</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571130" data-raw-source="[&lt;em&gt;WskDisconnectEvent&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571130)"><em>WskDisconnectEvent</em></a></p></td>
</tr>
<tr class="even">
<td><p>WSK_EVENT_RECEIVE</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571140" data-raw-source="[&lt;em&gt;WskReceiveEvent&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571140)"><em>WskReceiveEvent</em></a></p></td>
</tr>
<tr class="odd">
<td><p>WSK_EVENT_SEND_BACKLOG</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571147" data-raw-source="[&lt;em&gt;WskSendBacklogEvent&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571147)"><em>WskSendBacklogEvent</em></a></p></td>
</tr>
</tbody>
</table>


リッスン ソケットはリッスン ソケットによって受け入れられる接続指向のソケットでのイベントのコールバック関数を自動的に有効にできます。 WSK アプリケーションは、リッスン ソケットの接続指向のソケット イベント コールバック関数を有効にすると、これらのコールバック関数を自動的に有効です。 イベントのコールバック関数が自動的に有効に承認済みの接続指向のソケットでリッスン ソケットのによって、ソケットが受け入れられた場合にのみ[ *WskAcceptEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571120)イベント コールバック関数。 接続志向ソケットはリッスン ソケットのによって受け入れられます[ **WskAccept** ](https://msdn.microsoft.com/library/windows/hardware/ff571109)関数では、受け入れられたソケットのイベントのコールバック関数が自動的に有効でないです。

接続指向のイベントのコールバック関数をリッスン ソケットで有効にした後は、リッスン ソケットで無効にできません。 場合、 *WskAcceptEvent*そのリッスン ソケットで有効にしていた最初の接続指向のイベントのコールバック関数は引き続き、イベントのコールバック関数が無効になり、リッスン ソケットの再有効化によって受け入れられるすべての接続指向のソケットに適用される、 *WskAcceptEvent*イベント コールバック関数。

有効にして、ソケットのイベントのコールバック関数を無効化の詳細については、次を参照してください。[の有効化と無効にするとイベントのコールバック関数](https://msdn.microsoft.com/library/windows/hardware/ff548851)します。

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

 

 




