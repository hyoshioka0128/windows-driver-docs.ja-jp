---
title: Windows ソケットの SPI 関数のために必要な San
description: Windows ソケットの SPI 関数のために必要な San
ms.assetid: b41bd7e0-bb6c-4933-a5d0-18e4d067601b
keywords:
- SAN サービス プロバイダーに必要な関数
- WDK の San の機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9da03118f624130a3465120f7f6b8be82139315
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531844"
---
# <a name="windows-sockets-spi-functions-required-for-sans"></a>Windows ソケットの SPI 関数のために必要な San





このセクションでは、SAN サービス プロバイダーの DLL を指定する必要があります Windows Sockets SPI の機能について説明します。 これらの関数が Ws2spi.h で定義され、記載されて、 [Windows Sockets の直接参照](https://msdn.microsoft.com/library/windows/hardware/ff565857)セクション。

<a href="" id="wspaccept"></a>[**WSPAccept**](https://msdn.microsoft.com/library/windows/hardware/ff566266)  
条件付きで指定された条件関数の戻り値に基づいて、接続をリッスンするソケットの接続を受け入れます。

<a href="" id="wspbind"></a>[**WSPBind**](https://msdn.microsoft.com/library/windows/hardware/ff566268)  
ローカル IP アドレス、またはソケットでのネットワーク インターフェイスの名前を関連付けます。 このネットワーク インターフェイスは、SAN サービス プロバイダーによって処理されます。

<a href="" id="wspcleanup"></a>[**WSPCleanup**](https://msdn.microsoft.com/library/windows/hardware/ff566270)  
SAN サービス プロバイダーの DLL の使用を終了します。

<a href="" id="wspclosesocket"></a>[**WSPCloseSocket**](https://msdn.microsoft.com/library/windows/hardware/ff566273)  
ソケットを閉じます。

<a href="" id="wspconnect"></a>[**WSPConnect**](https://msdn.microsoft.com/library/windows/hardware/ff566275)  
接続を確立ピアへのソケットでの交換が、データを接続し、指定されたフローの仕様に基づいて service (QoS) の必要な品質を指定します。

<a href="" id="wspduplicatesocket"></a>[**WSPDuplicateSocket**](https://msdn.microsoft.com/library/windows/hardware/ff566282)  
取得、WSAPROTOCOL\_INFOW 構造別のプロセスのコンテキストで共有ソケットの新しいソケット記述子を作成するために使用できます。

<a href="" id="wspenumnetworkevents"></a>[**WSPEnumNetworkEvents**](https://msdn.microsoft.com/library/windows/hardware/ff566284)  
ソケットでのネットワーク イベントの発生を報告します。

<a href="" id="wspeventselect"></a>[**WSPEventSelect**](https://msdn.microsoft.com/library/windows/hardware/ff566287)  
ソケットでのイベント オブジェクトを指定します。 このイベント オブジェクトは、指定された一連のネットワーク イベントの発生によって後で設定されます。

<a href="" id="wspgetoverlappedresult"></a>[**WSPGetOverlappedResult**](https://msdn.microsoft.com/library/windows/hardware/ff566288)  
ソケットで非同期 (重複) 操作の結果を返します。 以前、この操作は、保留中の入力候補が示されます。

<a href="" id="wspgetqosbyname"></a>[**WSPGetQOSByName**](https://msdn.microsoft.com/library/windows/hardware/ff566290)  
名前付きのテンプレートに基づく QoS 構造体を初期化します。 または、使用可能なテンプレート名の列挙を取得します。

SAN サービス プロバイダーの QoS をサポートする DLL を完全に実装する必要があります**WSPGetQOSByName**します。 SAN サービスは、QoS をサポートしていませんが提供する場合、 **WSPGetQOSByName**関数 WSAEOPNOTSUPP エラーを返すには少なくとも必要があります。

<a href="" id="wspgetsockopt"></a>[**WSPGetSockOpt**](https://msdn.microsoft.com/library/windows/hardware/ff566292)  
ソケット オプションの現在の値を取得します。

<a href="" id="wspioctl"></a>[**WSPIoctl**](https://msdn.microsoft.com/library/windows/hardware/ff566296)  
設定またはソケットに関連付けられた操作パラメーターを取得します。

<a href="" id="wsplisten"></a>[**WSPListen**](https://msdn.microsoft.com/library/windows/hardware/ff566297)  
着信接続をリッスンするソケットを確立します。

<a href="" id="wsprecv"></a>[**WSPRecv**](https://msdn.microsoft.com/library/windows/hardware/ff566309)  
接続されたソケット上のデータを受信します。

<a href="" id="wspsend"></a>[**WSPSend**](https://msdn.microsoft.com/library/windows/hardware/ff566316)  
接続されたソケットにデータを送信します。

<a href="" id="wspsetsockopt"></a>[**WSPSetSockOpt**](https://msdn.microsoft.com/library/windows/hardware/ff566318)  
ソケット オプションの値を設定します。

<a href="" id="wspsocket"></a>[**WSPSocket**](https://msdn.microsoft.com/library/windows/hardware/ff566319)  
TCP/IP プロトコルと非同期 (重複) データ転送を使用するソケットを作成します。

 

 





