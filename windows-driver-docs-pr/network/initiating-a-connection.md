---
title: 接続を開始します。
description: 接続を開始します。
ms.assetid: 5e5ab033-b01a-45e2-acd4-7ea8931a621d
keywords:
- SAN 接続のセットアップ WDK、接続の開始
- SAN 接続の開始
- SAN を破棄するソケットの WDK San
- セッションのネゴシエーション WDK San
- SAN 接続のセットアップ WDK、フロー図
- SAN 接続の開始、WDK をソケットします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff266f71080f3b8cee150d6344405dffde130562
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537602"
---
# <a name="initiating-a-connection"></a>接続を開始します。


スイッチの受信後、Windows ソケットを**WSPConnect**その SAN サービスの IP サブネットのスイッチのテーブル内のアドレスで接続要求の送信先アドレスを比較するが、スイッチ、アプリケーションによって開始された呼び出しプロバイダー サービスを提供します。 それらのサブネットのいずれかには、この宛先アドレスが含まれている場合、スイッチを呼び出す、 [ **WSPSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff566319)と[ **WSPBind** ](https://msdn.microsoft.com/library/windows/hardware/ff566268)の関数、」の説明に従って、対応する SAN サービス プロバイダーを作成し、ソケットをバインド[SAN のソケットをバインドの作成と](creating-and-binding-san-sockets.md)します。 アプリケーションが接続 's スイッチ プロセスでは、SAN のソケットの使用を要求します。 接続要求の送信先アドレスが SAN のサブネット上にない場合、または SAN サービス プロバイダーが作成して、ソケットをバインドに失敗した場合は、スイッチは、接続を確立するために TCP/IP プロバイダーを使用します。

次の図は、リモート ピアとの接続に Windows Sockets が要求を切り替える方法の概要を示します。 シーケンスと次のセクションには、さらに詳しく接続要求が説明します。

![リモート ピアとの接続を要求する windows ソケットのスイッチの図の概要](images/apiflow3.png)

スイッチを作成して、SAN のソケットをバインドした後で SAN ソケットを使用して、接続要求を実行します*非ブロッキング モード*、次の手順で説明します。

**接続要求を実行するには**

1.  スイッチの呼び出し、SAN サービス プロバイダーの[ **WSPEventSelect** ](https://msdn.microsoft.com/library/windows/hardware/ff566287)関数。 この呼び出しでは、スイッチは、FD を渡します。\_接続コードとそのコードに関連するイベント オブジェクト。 呼び出し**WSPEventSelect**接続イベントの通知を要求し、SAN サービス プロバイダーに通知する後続[ **WSPConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff566275)で呼び出しを実行します非ブロッキング モード。

2.  後に、 **WSPEventSelect**スイッチ呼び出し SAN サービス プロバイダーの関数が戻る**WSPConnect**関数。 この呼び出しで、スイッチはのいずれかの形式で宛先アドレスを渡す、 [WSK アドレス ファミリ](https://msdn.microsoft.com/library/windows/hardware/ff571151)します。 SAN サービス プロバイダーのプロキシ ドライバーでは、この変換先のアドレスをネイティブのアドレスにマップ、接続を確立しようとします。

3.  SAN サービス プロバイダーの場合**WSPConnect**関数が完了または失敗の接続操作をすぐに、成功または失敗の適切なコードを返します。 SAN サービス プロバイダーの場合**WSPConnect**関数では、接続要求をすぐに完了できず、SAN サービス プロバイダーの接続操作は、別のスレッドで非同期的が続行されます。 SAN サービス プロバイダーの**WSPConnect** WSAEWOULDBLOCK ソケットがマークされていることを示すエラーを返します非ブロッキングと接続操作はすぐに完了したことはできません。

4.  SAN サービス プロバイダーが、Win32 を呼び出して接続操作の完了後**SetEvent**をイベント オブジェクトに既に登録済みの通知、 **WSPEventSelect**呼び出します。

5.  スイッチに SAN サービス プロバイダーの呼び出し、イベント オブジェクトがシグナルを受信した後[ **WSPEnumNetworkEvents** ](https://msdn.microsoft.com/library/windows/hardware/ff566284)接続操作の結果を取得します。

**注**  スイッチがその接続で TCP/IP プロバイダーを使用できます不要になった、スイッチ、SAN サービス プロバイダー経由の接続を確立した後。 SAN サービス プロバイダーは、完全に確立された接続をサービスに必要なすべての機能を実装する必要があります。

 

### <a name="destroying-the-san-socket"></a>SAN のソケットを破棄します。

SAN サービス プロバイダーの場合**WSPConnect**関数が失敗した場合は、SAN サービス プロバイダーのスイッチ呼び出し[ **WSPCloseSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff566273) SAN ソケットを破棄します。 スイッチを呼び出して、TCP/IP サービス プロバイダーの**WSPConnect** SAN サービス プロバイダーの結果として次のエラー コードのいずれかが返されない限り、接続の操作を TCP/IP サービスのプロバイダーに転送するように関数の接続操作:

<a href="" id="wsaeconnreset"></a>**WSAECONNRESET**  
アプリケーションが宛先アドレスで指定されたポートでリッスンしていないことを示します

<a href="" id="wsaeconnrefused"></a>**使います**  
リモート アプリケーションが接続要求によって拒否されたことを示します

<a href="" id="wsaehostunreach"></a>**WSAEHOSTUNREACH**  
送信先アドレスが存在しないことを示します

これら上記のエラー コードは、TCP/IP 経由の接続を確立するために、試行は失敗もことを保証します。 その保証を確立できない場合、SAN サービス プロバイダーはこれらのエラー コードのいずれかを返すしない必要があります。 たとえば、対象のコンピュータが Windows Sockets 直接サポートされていない SAN 上に存在する NDIS を介して通信する場合は、SAN サービス プロバイダー返すことができません WSAEHOSTUNREACH SAN 接続の失敗した要求の結果としてこのターゲットのため、TCP/IP プロバイダー経由の接続要求が成功することがあります。 この場合、SAN サービス プロバイダーは、WSAETIMEDOUT を返す必要があります。

### <a name="session-negotiation"></a>セッションのネゴシエーション

スイッチに SAN サービス プロバイダーの呼び出し、スイッチ、SAN サービス プロバイダー経由の接続を確立した後[ **WSPRegisterMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566311)拡張関数をバッファーのメモリを事前登録受信メッセージを受信する配列。 スイッチは SAN サービス プロバイダーの次に呼び出す[ **WSPRecv** ](https://msdn.microsoft.com/library/windows/hardware/ff566309)リモート ピアからメッセージ データを受信する 1 つまたは複数のバッファーを投稿する関数。 スイッチは、1 組の初期フロー制御情報を含むメッセージを交換することで、そのリモート ピアとのセッションをネゴシエートします。 完了すると、スイッチには、セッションがネゴシエートし、後に、 **WSPConnect**が開始したアプリケーションを呼び出します。 アプリケーションは、接続でデータを送信側と受信を開始できます。 詳細については、次を参照してください。[接続要求を受け入れる](accepting-connection-requests.md)します。

スイッチでは、SAN サービス プロバイダーの呼び出しません SAN ソケット経由で接続が確立されると、 **WSPConnect**関数。 スイッチは、スイッチへの呼び出しを開始するアプリケーションを内部的に処理**WSPConnect**接続要求をポーリングする関数。

 

 





