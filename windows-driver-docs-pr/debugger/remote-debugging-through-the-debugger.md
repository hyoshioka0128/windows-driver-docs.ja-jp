---
title: デバッガーによるリモート デバッグ
description: デバッガーによるリモート デバッグ
ms.assetid: a9f6f355-e684-471f-a45c-b2235a5372b1
keywords:
- リモート デバッガーを使用して、デバッグ
- デバッガーをリモート デバッグの概要
- クライアントのデバッグ
- サーバーのデバッグ
- TCP (リモート デバッグのプロトコル)
- COM ポート (リモート デバッグのプロトコル)
- モデム (リモート デバッグのプロトコル)
- 名前付きパイプ (リモート debuggi
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcfd0480df9e266b7bd46c6a775ff0587c2de14d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353578"
---
# <a name="remote-debugging-through-the-debugger"></a>デバッガーによるリモート デバッグ


## <span id="ddk_remote_debugging_through_the_debugger_dbg"></span><span id="DDK_REMOTE_DEBUGGING_THROUGH_THE_DEBUGGER_DBG"></span>


デバッガーを使用して直接リモート デバッグは、通常は、リモート デバッグを実行するベストと最も簡単な方法です。

この手法では、異なる場所にある 2 つのデバッガーを実行している必要があります。 実際には、デバッグを行っている、デバッガーが呼び出され、*サーバー デバッグ*します。 遠くからセッションを制御する、デバッガーが呼び出され、*デバッグ クライアント*します。

2 台のコンピューターを Windows 以外の同じバージョンを実行する必要はありません。任意のバージョンの Windows が実行できます。 実際に使用されるデバッガー必要があります。 同じにできません。WinDbg デバッグ クライアントでは、CDB デバッグ サーバーに接続できにすることができます。

Windows のパッケージのデバッグ ツールの同じリリースから 2 台のコンピューターが両方のデバッガーのバイナリがあることをお勧め最近のリリースから両方の以降。

このリモート セッションをセットアップするデバッグ サーバーは、最初に設定し、デバッグ、クライアントがアクティブ化します。 デバッグ クライアントの任意の数は、デバッグのサーバーに接続できます。 1 つのデバッガー変えることができます自体デバッグ サーバーがいくつか同時に、さまざまな種類の接続を容易にします。

ただし、1 つのデバッガーはできません、デバッグのクライアントとデバッグ サーバーに同時に。

このセクションの内容:

[デバッグ サーバー アクティブ化します。](activating-a-debugging-server.md)

[デバッグ サーバーの検索](searching-for-debugging-servers.md)

[デバッグ クライアントをアクティブ化します。](activating-a-debugging-client.md)

[クライアントとサーバーの例](client-and-server-examples.md)

[リモート デバッグ セッションを制御します。](controlling-a-remote-debugging-session.md)

 

 





