---
title: KD 接続サーバー セッションの制御
description: KD 接続サーバー セッションの制御
ms.assetid: d927575f-f408-48d0-81f4-0711a09b0015
keywords:
- KD 接続のサーバー、セッションを制御します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66343156fd13ace296c6aed7f7079df155e60b55
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375562"
---
# <a name="controlling-a-kd-connection-server-session"></a>KD 接続サーバー セッションの制御


## <span id="ddk_controlling_a_kd_connection_server_session_dbg"></span><span id="DDK_CONTROLLING_A_KD_CONNECTION_SERVER_SESSION_DBG"></span>


リモート セッションが開始されると、スマート クライアントができます、コンピューターから対象コンピューターをデバッグした場合、KD 接続のサーバーが実行されています。 すべてのコマンドは、パスは、スマート クライアントのコンピューターを基準とする点を除いても、このような状況では、動作はなります。

### <a name="span-idusingwindbgasasmartclientspanspan-idusingwindbgasasmartclientspanusing-windbg-as-a-smart-client"></a><span id="using_windbg_as_a_smart_client"></span><span id="USING_WINDBG_AS_A_SMART_CLIENT"></span>スマート クライアントとして WinDbg を使用します。

使用することができます WinDbg、KD 接続サーバー用のスマート クライアントとして開始後、[デバッグ |デバッグの停止](debug---stop-debugging.md)デバッグ セッションを終了するコマンド。 その時点では、WinDbg では、休止モードになり、KD 接続のサーバーには接続されなくします。 すべての後続のデバッグは WinDbg が実行されているコンピューターで実行されます。 使用して KD 接続サービスを提供する再アタッチできません[ファイル |カーネル デバッグ](file---kernel-debug.md)-これは、コマンドラインからのみ実行できます。

### <a name="span-idendingthesessionspanspan-idendingthesessionspanending-the-session"></a><span id="ending_the_session"></span><span id="ENDING_THE_SESSION"></span>セッションの終了

KD または WinDbg が終了または通常の方法でデバッグ セッションを終了できます。 参照してください[WinDbg でデバッグ セッションを終了します。](ending-a-debugging-session-in-windbg.md)

詳しくは。 KD 接続のサーバーでは、操作でが保持され、必要に応じて何度もとして再利用できます。 (そのこともできますで任意の数の同時デバッグ セッションのです。)

KD 接続のサーバーは、どちらのコンピューターから終了できます。 スマート クライアントからそれを終了するには、使用、 [ **.endpsrv (エンド プロセス サーバー)** ](-endpsrv--end-process-server-.md)コマンド。 実行されているコンピューターから KD 接続のサーバーを終了するには、タスク マネージャーを使用して kdsrv.exe プロセスを終了します。

 

 





