---
title: リモート デバッグ中のセキュリティ
description: リモート デバッグ中のセキュリティ
ms.assetid: 55e570d2-b005-4c09-ac8f-0632233a64bd
keywords:
- セキュリティに関する考慮事項、リモート デバッグ
- リモート デバッグを remote.exe、セキュリティに関する考慮事項
- リモート デバッグ、デバッガーのセキュリティに関する考慮事項
- プロセス サーバー、セキュリティに関する考慮事項
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d0ac7750e8e69100b9ac45c24d4dc21f3ffd64e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381990"
---
# <a name="security-during-remote-debugging"></a>リモート デバッグ中のセキュリティ


## <span id="ddk_security_during_remote_debugging_dbg"></span><span id="DDK_SECURITY_DURING_REMOTE_DEBUGGING_DBG"></span>


リモート デバッグ中にセキュリティを強化する 2 つの方法があります。 セッションに接続できるユーザーを制限することで、他の接続はユーザーの電源を制限することで。

### <a name="span-idcontrollingaccesstothedebuggingsessionspanspan-idcontrollingaccesstothedebuggingsessionspancontrolling-access-to-the-debugging-session"></a><span id="controlling_access_to_the_debugging_session"></span><span id="CONTROLLING_ACCESS_TO_THE_DEBUGGING_SESSION"></span>デバッグ セッションへのアクセスを制御します。

実行している場合[デバッガーからのリモート デバッグ](remote-debugging-through-the-debugger.md)、またはを使用して、[プロセス サーバー](process-servers--user-mode-.md)または[KD 接続サーバー](kd-connection-servers--kernel-mode-.md)、ローカル ネットワーク上の任意のコンピューターに試みることができますデバッグ セッションにアタッチします。

TCP、1394、COM を使用している場合や、名前付きパイプ プロトコル、パスワードを指定するクライアントをデバッグを要求できます。 ただし、このパスワードは、送信時に暗号化されませんし、したがってこれらのプロトコルは安全ではありません。

デバッグ サーバーで、セキュリティで保護する場合は、secure socket layer (SSL) またはセキュリティで保護されたパイプ (SPIPE) プロトコルを使用する必要があります。

実行する場合[remote.exe を通じてリモート デバッグ](remote-debugging-through-remote-exe.md)、使用することができます、 **/u**パラメーターが承認されていないユーザーからの接続を禁止します。

### <a name="span-idrestrictingthepowersoftheclientspanspan-idrestrictingthepowersoftheclientspanrestricting-the-powers-of-the-client"></a><span id="restricting_the_powers_of_the_client"></span><span id="RESTRICTING_THE_POWERS_OF_THE_CLIENT"></span>クライアントの電源を制限します。

カーネル モードのデバッグ セッションをセットアップする場合を使用して、ホスト マシンに干渉するデバッガーの機能を制限できます[保護モード](secure-mode.md)します。

ユーザー モードで、保護モードでは使用できません。 Microsoft MS-DOS のコマンドを発行および発行することによって外部プログラムの実行から侵入のクライアントを停止することができます、 [ **.noshell (シェルのコマンドを禁止)** ](-noshell--prohibit-shell-commands-.md)コマンド。 ただし、クライアント コンピューターに干渉するための他の多くの方法はあります。

なお両方をセキュリティで保護モードと **.noshell**特定の操作を行ってからクライアントをデバッグとデバッグ サーバーの両方が回避されます。 クライアントがサーバーではなく、制限を配置する方法はありません。

### <a name="span-idforgottenprocessserversspanspan-idforgottenprocessserversspanforgotten-process-servers"></a><span id="forgotten_process_servers"></span><span id="FORGOTTEN_PROCESS_SERVERS"></span>忘れられたプロセス サーバー

リモート コンピューターでプロセス サーバーを開始すると、プロセス サーバーをサイレント モードで実行します。

このプロセス サーバーをリモート デバッグを実行し、セッションを終了すると、プロセス サーバーを実行し続けます。

忘れられたプロセス サーバーは、潜在的な攻撃のターゲットです。 常に、不要なプロセス サーバーをシャット ダウンする必要があります。 プロセス サーバーを終了するのにには、Kill.exe ユーティリティまたはタスク マネージャーを使用します。

 

 





