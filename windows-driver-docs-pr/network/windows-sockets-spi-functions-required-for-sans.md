---
title: SAN に必要な Windows ソケット SPI 関数
description: SAN に必要な Windows ソケット SPI 関数
ms.assetid: b41bd7e0-bb6c-4933-a5d0-18e4d067601b
keywords:
- SAN サービス プロバイダーに必要な関数
- WDK の San の機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b0cc60baa81b749ac1bf977adbb81f83d658d5e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384697"
---
# <a name="windows-sockets-spi-functions-required-for-sans"></a>SAN に必要な Windows ソケット SPI 関数





このセクションでは、SAN サービス プロバイダーの DLL を指定する必要があります Windows Sockets SPI の機能について説明します。 これらの関数が Ws2spi.h で定義され、記載されて、 [Windows Sockets の直接参照](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565857(v=vs.85))セクション。

<a href="" id="wspaccept"></a>[**WSPAccept**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566266(v=vs.85))  
条件付きで指定された条件関数の戻り値に基づいて、接続をリッスンするソケットの接続を受け入れます。

<a href="" id="wspbind"></a>[**WSPBind**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566268(v=vs.85))  
ローカル IP アドレス、またはソケットでのネットワーク インターフェイスの名前を関連付けます。 このネットワーク インターフェイスは、SAN サービス プロバイダーによって処理されます。

<a href="" id="wspcleanup"></a>[**WSPCleanup**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566270(v=vs.85))  
SAN サービス プロバイダーの DLL の使用を終了します。

<a href="" id="wspclosesocket"></a>[**WSPCloseSocket**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566273(v=vs.85))  
ソケットを閉じます。

<a href="" id="wspconnect"></a>[**WSPConnect**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566275(v=vs.85))  
接続を確立ピアへのソケットでの交換が、データを接続し、指定されたフローの仕様に基づいて service (QoS) の必要な品質を指定します。

<a href="" id="wspduplicatesocket"></a>[**WSPDuplicateSocket**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566282(v=vs.85))  
取得、WSAPROTOCOL\_INFOW 構造別のプロセスのコンテキストで共有ソケットの新しいソケット記述子を作成するために使用できます。

<a href="" id="wspenumnetworkevents"></a>[**WSPEnumNetworkEvents**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566284(v=vs.85))  
ソケットでのネットワーク イベントの発生を報告します。

<a href="" id="wspeventselect"></a>[**WSPEventSelect**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566287(v=vs.85))  
ソケットでのイベント オブジェクトを指定します。 このイベント オブジェクトは、指定された一連のネットワーク イベントの発生によって後で設定されます。

<a href="" id="wspgetoverlappedresult"></a>[**WSPGetOverlappedResult**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566288(v=vs.85))  
ソケットで非同期 (重複) 操作の結果を返します。 以前、この操作は、保留中の入力候補が示されます。

<a href="" id="wspgetqosbyname"></a>[**WSPGetQOSByName**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566290(v=vs.85))  
名前付きのテンプレートに基づく QoS 構造体を初期化します。 または、使用可能なテンプレート名の列挙を取得します。

SAN サービス プロバイダーの QoS をサポートする DLL を完全に実装する必要があります**WSPGetQOSByName**します。 SAN サービスは、QoS をサポートしていませんが提供する場合、 **WSPGetQOSByName**関数 WSAEOPNOTSUPP エラーを返すには少なくとも必要があります。

<a href="" id="wspgetsockopt"></a>[**WSPGetSockOpt**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566292(v=vs.85))  
ソケット オプションの現在の値を取得します。

<a href="" id="wspioctl"></a>[**WSPIoctl**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566296(v=vs.85))  
設定またはソケットに関連付けられた操作パラメーターを取得します。

<a href="" id="wsplisten"></a>[**WSPListen**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566297(v=vs.85))  
着信接続をリッスンするソケットを確立します。

<a href="" id="wsprecv"></a>[**WSPRecv**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566309(v=vs.85))  
接続されたソケット上のデータを受信します。

<a href="" id="wspsend"></a>[**WSPSend**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566316(v=vs.85))  
接続されたソケットにデータを送信します。

<a href="" id="wspsetsockopt"></a>[**WSPSetSockOpt**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566318(v=vs.85))  
ソケット オプションの値を設定します。

<a href="" id="wspsocket"></a>[**WSPSocket**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566319(v=vs.85))  
TCP/IP プロトコルと非同期 (重複) データ転送を使用するソケットを作成します。

 

 





