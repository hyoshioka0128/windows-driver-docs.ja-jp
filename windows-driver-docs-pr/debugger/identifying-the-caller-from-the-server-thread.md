---
title: サーバーのスレッドから呼び出し元を識別します。
description: サーバーのスレッドから呼び出し元を識別します。
ms.assetid: d19dc242-1043-4e61-9fcb-eadac0ab63c8
keywords:
- RPC デバッグ、呼び出し元を識別します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecea5be6fff755074eebc25c1fc64dcf56af8dc5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552695"
---
# <a name="identifying-the-caller-from-the-server-thread"></a>サーバーのスレッドから呼び出し元を識別します。


## <span id="ddk_identifying_the_caller_from_the_server_thread_dbg"></span><span id="DDK_IDENTIFYING_THE_CALLER_FROM_THE_SERVER_THREAD_DBG"></span>


唯一の情報がある場合は、サーバー スレッドの呼び出しを処理する場合でも、指定された RPC 呼び出しが行われたものを特定することになります。

これが大変役立ちます - たとえば、RPC 呼び出しに無効なパラメーターが渡されるユーザーを確認します。

この特定の呼び出しでのメッセージを使用すると、どのプロトコル順序によっては、詳細度を可変を取得できます。 (NetBios) などの一部のプロトコルでは、この情報をまったくありません。

**サーバーのスレッドから呼び出し元を識別します。**

1.  サーバーのスレッドに、ターゲットとしてユーザー モード デバッガーを起動します。

2.  使用してプロセス ID を取得、 [ **|(プロセスの状態)** ](---process-status-.md)コマンド。
    ```dbgcmd
    0:001> |
      0     id: 3d4 name: rtsvr.exe
    ```

3.  使用して、このプロセスでアクティブな呼び出しを取得、 [ **! rpcexts.getcallinfo** ](-rpcexts-getcallinfo.md)拡張機能。 (構文の詳細については、リファレンス ページを参照してください)。0x3D4 のプロセス ID を指定する必要があります。

    ```dbgcmd
    0:001> !rpcexts.getcallinfo 0 0 FFFF 3d4
    Searching for call info ...
    PID  CELL ID   ST PNO IFSTART  THRDCELL  CALLFLAG CALLID   LASTTIME CONN/CLN
    ----------------------------------------------------------------------------
    03d4 0000.0004 02 000 19bb5061 0000.0002 00000001 00000001 00a1aced 0000.0003
    ```

    状態が 02 または 01 (ディスパッチまたはアクティブな) 呼び出しを探します。 この例で、プロセスでは、1 回の呼び出しがのみがあります。 詳細が、使用する必要があります、 [ **! rpcexts.getdbgcell** ](-rpcexts-getdbgcell.md) THRDCELL 列内のセル数の拡張機能。 これによってにより Id するどの呼び出しを調べるために関心がスレッドを調べます。

4.  興味のある呼び出しを確認した後 CONN/CLN 列のセル数を確認します。 これは、接続オブジェクトのセルの ID です。 この場合、セルの数は 0000.0003 です。 このセルの数とプロセス ID を渡す **! rpcexts.getdbgcell**:
    ```dbgcmd
    0:001> !rpcexts.getdbgcell 3d4 0.3
    Getting cell info ...
    Connection
    Connection flags: Exclusive
    Authentication Level: Default
    Authentication Service: None
    Last Transmit Fragment Size: 24 (0x6F56D)
    Endpoint for the connection: 0x0.1
    Last send time (in seconds since boot):10595.565 (0x2963.235)
    Last receive time (in seconds since boot):10595.565 (0x2963.235)
    Getting endpoint info ...
    Process object for caller is 0xFF9DF5F0
    ```

この拡張機能はすべて、使用可能なクライアントに関する情報のこの接続で表示されます。 実際の情報の量は、使用されているトランスポートによって異なります。

この例では、ローカル名前付きパイプは、トランスポートとして使用されているし、呼び出し元のプロセス オブジェクトのアドレスが表示されます。 カーネル デバッガーをアタッチ (またはローカル カーネル デバッガーを起動します) 場合、使用できます、 [ **! プロセス**](-process.md)このプロセスのアドレスを解釈する拡張機能。

LRPC をトランスポートとして使用する場合は、プロセス ID と、呼び出し元のスレッド ID が表示されます。

TCP をトランスポートとして使用する場合は、呼び出し元の IP アドレスが表示されます。

リモートの名前付きパイプをトランスポートとして使用する場合の情報は使用できません。

**注**  前の例は、サーバー スレッドがわかっている場合は、クライアント スレッドを見つける方法を示しています。 逆の手法の例は、次を参照してください。[呼び出しスタックしている問題を分析](analyzing-a-stuck-call-problem.md)します。

 

 

 





