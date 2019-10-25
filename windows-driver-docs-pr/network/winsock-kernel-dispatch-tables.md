---
title: Winsock カーネル ディスパッチ テーブル
description: Winsock カーネル ディスパッチ テーブル
ms.assetid: 391c6868-fb85-41ea-ada5-6ba90750300c
keywords:
- Winsock カーネル WDK ネットワーク、ディスパッチテーブル
- WSK WDK ネットワーク、ディスパッチテーブル
- ディスパッチテーブル WDK Winsock カーネル
- functions WDK Winsock カーネル
- basic sockets WDK Winsock カーネル
- リスニングソケット WDK Winsock カーネル
- データグラムソケット WDK Winsock カーネル
- 接続指向ソケット WDK Winsock カーネル
- イベントコールバック関数 WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 990a06efc3982fbd16ae88c4d1aab850bf53f134
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844377"
---
# <a name="winsock-kernel-dispatch-tables"></a>Winsock カーネル ディスパッチ テーブル


Winsock カーネル (WSK) ソケットの[ソケットオブジェクト](winsock-kernel-objects.md)には、ソケットによってサポートされるソケット関数への関数ポインターを含むプロバイダーディスパッチテーブル構造へのポインターが含まれています。 WSK アプリケーションは、プロバイダーディスパッチテーブル構造内の関数を呼び出して、ソケットでネットワーク i/o 操作を実行します。 各 WSK[ソケットカテゴリ](winsock-kernel-socket-categories.md)は異なるソケット関数のセットをサポートしているため、Wsk[ネットワークプログラミングインターフェイス (NPI)](network-programming-interface.md)は wsk ソケットの各カテゴリに対して異なるプロバイダーディスパッチテーブル構造を定義します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ソケットカテゴリ</th>
<th align="left">ディスパッチテーブルの構造</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>基本ソケット</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_basic_dispatch" data-raw-source="[&lt;strong&gt;WSK_PROVIDER_BASIC_DISPATCH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_basic_dispatch)"><strong>WSK_PROVIDER_BASIC_DISPATCH</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>リッスンしているソケット</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_listen_dispatch" data-raw-source="[&lt;strong&gt;WSK_PROVIDER_LISTEN_DISPATCH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_listen_dispatch)"><strong>WSK_PROVIDER_LISTEN_DISPATCH</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>データグラムソケット</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_datagram_dispatch" data-raw-source="[&lt;strong&gt;WSK_PROVIDER_DATAGRAM_DISPATCH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_datagram_dispatch)"><strong>WSK_PROVIDER_DATAGRAM_DISPATCH</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>接続指向のソケット</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_connection_dispatch" data-raw-source="[&lt;strong&gt;WSK_PROVIDER_CONNECTION_DISPATCH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_connection_dispatch)"><strong>WSK_PROVIDER_CONNECTION_DISPATCH</strong></a></p></td>
</tr>
</tbody>
</table>

 

WSK アプリケーションで、作成するソケットに対してイベントコールバック関数を使用する場合、新しいソケットを作成するたびに、ソケットのイベントコールバック関数への関数ポインターを含むクライアントディスパッチテーブル構造を提供する必要があります。 各 WSK ソケットカテゴリは異なるイベントコールバック関数のセットをサポートしているため、WSK NPI は WSK ソケットの各カテゴリに対して異なるクライアントディスパッチテーブル構造を定義します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ソケットカテゴリ</th>
<th align="left">ディスパッチテーブルの構造</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>リッスンしているソケット</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_listen_dispatch" data-raw-source="[&lt;strong&gt;WSK_CLIENT_LISTEN_DISPATCH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_listen_dispatch)"><strong>WSK_CLIENT_LISTEN_DISPATCH</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>データグラムソケット</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_datagram_dispatch" data-raw-source="[&lt;strong&gt;WSK_CLIENT_DATAGRAM_DISPATCH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_datagram_dispatch)"><strong>WSK_CLIENT_DATAGRAM_DISPATCH</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>接続指向のソケット</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_connection_dispatch" data-raw-source="[&lt;strong&gt;WSK_CLIENT_CONNECTION_DISPATCH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_connection_dispatch)"><strong>WSK_CLIENT_CONNECTION_DISPATCH</strong></a></p></td>
</tr>
</tbody>
</table>

 

**注**  基本ソケットは、イベントコールバック関数をサポートしていません。 そのため、基本ソケットに対してクライアントディスパッチテーブル構造は定義されていません。

 

 

 





