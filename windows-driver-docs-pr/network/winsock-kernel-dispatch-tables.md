---
title: Winsock Kernel ディスパッチ テーブル
description: Winsock Kernel ディスパッチ テーブル
ms.assetid: 391c6868-fb85-41ea-ada5-6ba90750300c
keywords:
- Winsock カーネル WDK がネットワーク接続、ディスパッチ テーブル
- ネットワーク、WSK WDK ディスパッチ テーブル
- ディスパッチ テーブル WDK Winsock カーネル
- WDK Winsock Kernel 関数
- 基本的なソケット WDK Winsock カーネル
- リッスンしているソケット WDK Winsock カーネル
- データグラム ソケット WDK Winsock カーネル
- 接続指向のソケット WDK Winsock カーネル
- WDK Winsock Kernel のイベントのコールバック関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c62de8e85bfd1ca9251bf5ae7a6c19e0d9eb8d41
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558650"
---
# <a name="winsock-kernel-dispatch-tables"></a>Winsock Kernel ディスパッチ テーブル


[ソケット オブジェクト](winsock-kernel-objects.md)Winsock カーネル (WSK) のソケットがソケットでサポートされているソケット関数への関数ポインターを含むプロバイダー ディスパッチ テーブルの構造体へのポインターを格納します。 WSK アプリケーションでは、ソケットでのネットワーク I/O 操作を実行するには、プロバイダー ディスパッチ テーブル構造で、関数を呼び出します。 ため、各 WSK[ソケット カテゴリ](winsock-kernel-socket-categories.md)、WSK、ソケット関数のさまざまなセットがサポートする[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)のカテゴリごとに別のプロバイダーのディスパッチ テーブル構造を定義します。WSK ソケット。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ソケットのカテゴリ</th>
<th align="left">ディスパッチ テーブルの構造</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>基本的なソケット</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571171" data-raw-source="[&lt;strong&gt;WSK_PROVIDER_BASIC_DISPATCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571171)"><strong>WSK_PROVIDER_BASIC_DISPATCH</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>待機中のソケット</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571176" data-raw-source="[&lt;strong&gt;WSK_PROVIDER_LISTEN_DISPATCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571176)"><strong>WSK_PROVIDER_LISTEN_DISPATCH</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>データグラム ソケット</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571174" data-raw-source="[&lt;strong&gt;WSK_PROVIDER_DATAGRAM_DISPATCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571174)"><strong>WSK_PROVIDER_DATAGRAM_DISPATCH</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>接続志向ソケット</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571173" data-raw-source="[&lt;strong&gt;WSK_PROVIDER_CONNECTION_DISPATCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571173)"><strong>WSK_PROVIDER_CONNECTION_DISPATCH</strong></a></p></td>
</tr>
</tbody>
</table>

 

WSK アプリケーションでは、作成したソケットの場合、イベントのコールバック関数を使用している場合は、新しいソケットが作成されるたびに、ソケットのイベントのコールバック関数への関数ポインターを含むディスパッチ テーブル構造をクライアントに提供する必要があります。 WSK ソケットのカテゴリごとに異なる一連のイベント コールバック関数がサポートされているために、WSK NPI は WSK ソケットのカテゴリごとに異なるクライアント ディスパッチ テーブル構造を定義します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ソケットのカテゴリ</th>
<th align="left">ディスパッチ テーブルの構造</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>待機中のソケット</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571162" data-raw-source="[&lt;strong&gt;WSK_CLIENT_LISTEN_DISPATCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571162)"><strong>WSK_CLIENT_LISTEN_DISPATCH</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>データグラム ソケット</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571158" data-raw-source="[&lt;strong&gt;WSK_CLIENT_DATAGRAM_DISPATCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571158)"><strong>WSK_CLIENT_DATAGRAM_DISPATCH</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>接続志向ソケット</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571156" data-raw-source="[&lt;strong&gt;WSK_CLIENT_CONNECTION_DISPATCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571156)"><strong>WSK_CLIENT_CONNECTION_DISPATCH</strong></a></p></td>
</tr>
</tbody>
</table>

 

**注**  基本的なソケットはイベントのコールバック関数をサポートしていません。 そのため、クライアント ディスパッチ テーブル構造が定義されていないソケットの基本的です。

 

 

 





