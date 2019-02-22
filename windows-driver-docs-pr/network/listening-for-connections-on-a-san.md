---
title: SAN 上の接続のリッスン
description: SAN 上の接続のリッスン
ms.assetid: 7e430bda-74f5-4a1a-90f0-3b2e44fb25a3
keywords:
- SAN 接続のセットアップ WDK、接続のリッスン
- WDK の San の操作をリッスンします。
- SAN 接続要求を拒否しています
- リモート ピア接続 refusals WDK San
- 非ブロッキング モード WDK San
- WSPListen
- SAN 接続のリッスン、WDK をソケットします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b895c4922ed64900ee7eeeaf1181c41377a1ea49
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553146"
---
# <a name="listening-for-connections-on-a-san"></a>SAN 上の接続のリッスン





-- リモート ピアからの着信接続要求のリッスン、次の図は、SAN ソケットに行わなければならないと--であるキューに Windows Sockets がセットに切り替える方法の概要を示します。 以下のトピックでは、リッスンしているプロセスの詳細について説明します。

![windows ソケットのスイッチの図の概要を認識し、リモート ピアからの着信接続要求をキューの san ソケットを設定します。](images/apiflow4.png)

受信 Windows Sockets を切り替えると、 **WSPListen**スイッチを常に、アプリケーションによって開始された呼び出しからの TCP/IP プロバイダーの**WSPListen** TCP/IP プロバイダーを設定するには、まず関数確認を受信接続要求をキューに登録するソケット。 SAN の NIC の IP アドレスか、またはワイルドカードの IP アドレスには、アプリケーションのソケットがバインド、スイッチは追加のソケットにバインドを作成し、適切な SAN サービス プロバイダーも使用します。 詳細については、次を参照してください。 [SAN のソケットをバインドの作成と](creating-and-binding-san-sockets.md)します。

### <a name="listening-for-incoming-connection-requests"></a>受信接続要求のリッスン

SAN サービス プロバイダーを作成し、SAN のソケットをバインドを要求すると後のスイッチを呼び出して、 [ **WSPListen** ](https://msdn.microsoft.com/library/windows/hardware/ff566297)着信接続をリッスンする SAN ソケットが SAN サービス プロバイダーの関数SAN サービス プロバイダーであることを要求できますキューに着信接続の数に制限を指定します。

### <a name="setting-up-to-accept-incoming-connections"></a>着信接続を受け入れるように設定します。

スイッチは、非ブロッキング モードでのみの受信接続を受け入れます。 スイッチの呼び出し、SAN サービス プロバイダーの[ **WSPEventSelect** ](https://msdn.microsoft.com/library/windows/hardware/ff566287)関数を非ブロッキング モード ソケットにおよび着信接続のイベントの通知を要求します。 この呼び出しでは、スイッチは、FD を渡します。\_同意コードとそのコードに関連するイベント オブジェクト。 SAN サービス プロバイダーが、Win32 を呼び出し、SAN サービス プロバイダーがリッスンするために確立された以前のソケットで接続要求を受け取った後**SetEvent**を関連付けられたイベント オブジェクトを通知します。 スイッチは、専用のスレッドで受信接続イベントをリッスンし、受け入れるか、イベント オブジェクトがシグナル通知された後に、接続を拒否します。 詳細については、次を参照してください。[接続要求を受け入れる](accepting-connection-requests.md)します。

### <a name="indicating-refusal-of-a-connection-request-to-a-remote-peer"></a>リモート ピアに接続要求の拒否されたことを示す

接続要求が到着すると、接続要求の SAN サービス プロバイダーのバックログがいっぱい、SAN サービス プロバイダーがすぐに示されますリモート ピアに接続要求を拒否したこと。 この場合、SAN サービス プロバイダーでは、接続要求を承認または拒否のスイッチを通知するために、イベント オブジェクトは通知しません。 リモート ピアの SAN サービス プロバイダーは、その接続の操作によって開始された、失敗する必要があります、 **WSPConnect**使いますエラー コードを呼び出します。

 

 





