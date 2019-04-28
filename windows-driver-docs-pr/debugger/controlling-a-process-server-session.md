---
title: プロセス サーバー セッションの制御
description: プロセス サーバー セッションの制御
ms.assetid: 4219b08a-d353-43dc-8640-96c504b8075b
keywords:
- プロセス サーバー、セッションを制御します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c193ba0539d8fed3ce7ff2c934275a4f32009da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375564"
---
# <a name="controlling-a-process-server-session"></a>プロセス サーバー セッションの制御


## <span id="ddk_controlling_a_process_server_session_dbg"></span><span id="DDK_CONTROLLING_A_PROCESS_SERVER_SESSION_DBG"></span>


リモート セッションが開始されたら、1 台のコンピューター上のターゲット アプリケーションをデバッグした場合、スマート クライアントを使用できます。 すべてのコマンドは、パスは、スマート クライアントのコンピューターを基準とする点を除いても、このような状況では、動作はなります。

### <a name="span-idusingwindbgasasmartclientspanspan-idusingwindbgasasmartclientspanusing-windbg-as-a-smart-client"></a><span id="using_windbg_as_a_smart_client"></span><span id="USING_WINDBG_AS_A_SMART_CLIENT"></span>スマート クライアントとして WinDbg を使用します。

ユーザー モードのプロセス サーバー用のスマート クライアントとして WinDbg が開始されると、ままになります、プロセス サーバーに接続されている永続的に。 デバッグ セッションが終了した場合、[ファイル |プロセスにアタッチする](file---attach-to-a-process.md)メニュー コマンド、または[ **.tlist (プロセス Id の一覧)** ](-tlist--list-process-ids-.md)コマンドは、プロセス サーバーを実行しているコンピューターで実行されているすべてのプロセスで表示されます。 WinDbg は、これらのプロセスのいずれかにアタッチできます。

[ファイル |実行可能ファイルを開く](file---open-executable.md)コマンドを使用することはできません。 新しいプロセスは、WinDbg コマンド ラインに含まれている場合にのみ生成できます。

この場合、WinDbg は場所が実行されていることも、できなくなりますカーネル デバッグ セッションを開始するコンピューター上のプロセスをデバッグできません。

### <a name="span-idendingthesessionspanspan-idendingthesessionspanending-the-session"></a><span id="ending_the_session"></span><span id="ENDING_THE_SESSION"></span>セッションの終了

CDB または WinDbg が終了または通常の方法でデバッグ セッションを終了できます。 参照してください[WinDbg でデバッグ セッションを終了する](ending-a-debugging-session-in-windbg.md)詳細についてはします。 プロセス サーバーは、操作でが保持され、必要に応じて何度もとして再利用できます。 (そのこともできますで任意の数の同時デバッグ セッションのです。)

どちらのコンピューターからプロセス サーバーを終了できます。 スマート クライアントからそれを終了するには、使用、 [ **.endpsrv (エンド プロセス サーバー)** ](-endpsrv--end-process-server-.md)コマンド。 実行されているコンピューターからプロセス サーバーを終了するには、タスク マネージャーを使用して dbgsrv.exe プロセスを終了します。

 

 





