---
title: Windows ソケットは必要ありません SPI 関数 San
description: Windows ソケットは必要ありません SPI 関数 San
ms.assetid: 995ff59e-8ee4-4468-914d-47c14d804c38
keywords:
- SAN サービス プロバイダー WDK、必須ではない関数
- WDK の San の機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81b8690c37dda4cdb43b38827073aeae97a46421
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557899"
---
# <a name="windows-sockets-spi-functions-not-required-for-sans"></a>Windows ソケットは必要ありません SPI 関数 San





このセクションでは、SAN サービス プロバイダーが実装する必要はない Windows Sockets SPI の機能について説明します。 これらの関数は、Ws2spi.h で定義されます。

<a href="" id="wspaddresstostring"></a>**WSPAddressToString**  
Windows Sockets スイッチでは、TCP/IP プロバイダーを使用して、SOCKADDR 構造体のすべてのコンポーネントをソケットの IP アドレスを表す人間が判読できる数値文字列に変換します。

<a href="" id="wspasyncselect"></a>**WSPAsyncSelect**  
Windows Sockets スイッチのセッション プロトコルを使用して内部的にソケットに関して、ネットワーク イベントの通知を処理するために必要な場合。

<a href="" id="wspcancelblockingcall"></a>**WSPCancelBlockingCall**  
Windows Sockets スイッチは、進行中の要求をブロックしてのキャンセルを内部的に処理します。 そのため、SAN サービス プロバイダーの DLL への呼び出しをブロックしているキャンセルを問題はありません。 Windows ソケットは、いずれかのことができますを切り替えます。

SAN のソケットを閉じることで、未処理の接続要求をキャンセルします。 SAN サービス プロバイダーの DLL には、接続要求を中止する必要があります。

未処理の送信を取り消すし、スイッチが内部的には、そのデータをバッファー処理している場合、それらの要求のデータを破棄することによって、またはアプリケーション バッファーとの間の RDMA 転送している場合、完了にそれらの要求を待機して、要求を受信します。 RDMA の転送時間がかかる場合、スイッチはまったくの接続を閉じることができます。

Microsoft Windows SDK の Windows Sockets SPI ドキュメントでは、ブロック呼び出しが取り消された場合、アプリケーションが保持されている接続に依存できないことを警告します。 ブロックの要求の取り消し後のソケットで成功が保証されている唯一の呼び出しは、この場合、 **WSPCloseSocket**します。

**WSPGetPeerName**スイッチがのピアへの接続が確立されるとき、Windows Sockets スイッチは、ピアの IP アドレスをキャッシュ、 **WSPConnect**のピアへの接続を受け入れるを呼び出したり、 **WSPAccept**呼び出します。 スイッチは、必要な場合に、アプリケーションにキャッシュされたこの値を提供します。

**WSPGetSockName**スイッチのソケット アドレスに ときに、Windows Sockets スイッチがソケットでのローカル IP アドレスをキャッシュ、 **WSPBind**のピアへの接続を受け入れるを呼び出したり、 **WSPAccept**呼び出します。 スイッチは、必要な場合に、アプリケーションにキャッシュされたこの値を提供します。

**WSPJoinLeaf** The Windows Sockets スイッチ排他的 multipoint セッションを処理するために TCP/IP プロバイダーに使用します。

**WSPRecvDisconnect** The Windows Sockets スイッチは、内部的にソケットでのデータ受信の終了を処理し、任意の受信を取得しますが、リモート パーティからデータを切断します。

**WSPRecvFrom** Windows Sockets ダイレクトの現在のバージョンはユーザー データグラム プロトコル (UDP) のセマンティクスを持つデータグラムを受信したソケットの処理、SAN サービス プロバイダーをサポートしていません。 そのため、SAN サービス プロバイダーの呼び出し、Windows Sockets スイッチ**WSPRecv**伝送制御プロトコル (TCP) のセマンティクスを持つデータのストリームを受信する接続されたソケット上の関数。

**WSPSelect** The Windows Sockets スイッチのセッション プロトコルを使用して内部的に TCP/IP プロバイダーと連携、ソケットのステータスを確認するために必要な場合。

**WSPSendDisconnect** The Windows Sockets スイッチは、ソケット接続の終了を内部的に処理し、切断、リモート パーティにデータを送信します。

**WSPSendTo** Windows Sockets ダイレクトの現在のバージョンはユーザー データグラム プロトコル (UDP) のセマンティクスを持つデータグラムを送信したソケットの処理、SAN サービス プロバイダーをサポートしていません。 そのため、SAN サービス プロバイダーの呼び出し、Windows Sockets スイッチ**WSPSend**伝送制御プロトコル (TCP) のセマンティクスでストリーム データを送信する接続されたソケット上の関数。

**WSPShutdown**ソケット上のデータの送受信に内部的には、Windows Sockets スイッチ無効にします。

**WSPStartup** The Windows Sockets スイッチは呼び出しません**WSPStartup** SAN サービス プロバイダーの操作を開始します。 スイッチは、SAN サービス プロバイダーの代わりに使用**WSPStatupEx**関数。

**WSPStringToAddress** The Windows Sockets スイッチでは、TCP/IP プロバイダーを使用して、Windows ソケットに渡すために適しているソケット アドレス構造 (SOCKADDR) に、ソケットの IP アドレスを表す人間が判読できる数値文字列に変換このような構造体を実行するルーチン。

 

 





