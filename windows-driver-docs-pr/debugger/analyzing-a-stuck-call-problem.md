---
title: スタックした呼び出しの問題の分析
description: スタックした呼び出しの問題の分析
ms.assetid: e1a80cde-cf83-4a16-ae4b-5ddd5eb77b6d
keywords:
- RPC 呼び出しスタックをデバッグします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfdd02f84b9bff7f826339b87ac577636ee372f6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355414"
---
# <a name="analyzing-a-stuck-call-problem"></a>スタックした呼び出しの問題の分析


## <span id="ddk_analyzing_a_stuck_call_problem_dbg"></span><span id="DDK_ANALYZING_A_STUCK_CALL_PROBLEM_DBG"></span>


一般的な問題は、プロセスが、RPC 呼び出しを直接または間接的には、クリティカル セクションまたはリソースを保持しているときに発生します。 この場合、RPC 呼び出しは別のプロセスまたはコンピューターに移動し、これがハングし、または時間がかかりすぎる manager ルーチン (server ルーチン) にディスパッチします。 これにより、呼び出し元をクリティカル セクションのタイムアウトが発生します。

デバッガーを使用して調べ、RPC は、クリティカル セクションを所有しているスレッドのスタックの一番上が待機しているどのようなわかりにくいですが。

このようなスタックの 1 つの例を次に示します。 多くのバリエーションが可能です。

```dbgcmd
0:002> ~1k
ChildEBP RetAddr
0068fba0 77e9e8eb ntdll!ZwWaitForSingleObject+0xb
0068fbc8 4efeff73 KERNEL32!WaitForSingleObjectEx+0x5a
0068fbe8 4eff0012 RPCRT4!UTIL_WaitForSyncIO+0x21
0068fc0c 4efe6e2b RPCRT4!UTIL_GetOverlappedResultEx+0x44
0068fc44 4ef973bf RPCRT4!WS_SyncRecv+0x12a
0068fc68 4ef98d5a RPCRT4!OSF_CCONNECTION__TransSendReceive+0xcb
0068fce4 4ef9b682 RPCRT4!OSF_CCONNECTION__SendFragment+0x297
0068fd38 4ef9a5a8 RPCRT4!OSF_CCALL__SendNextFragment+0x272
0068fd88 4ef9a9cb RPCRT4!OSF_CCALL__FastSendReceive+0x165
0068fda8 4ef9a7f8 RPCRT4!OSF_CCALL__SendReceiveHelper+0xed
0068fdd4 4ef946a7 RPCRT4!OSF_CCALL__SendReceive+0x37
0068fdf0 4efd56b3 RPCRT4!I_RpcSendReceive+0xc4
0068fe08 01002850 RPCRT4!NdrSendReceive+0x4f
0068ff40 01001f32 rtclnt+0x2850
0068ffb4 77e92ca8 rtclnt+0x1f32
0068ffec 00000000 KERNEL32!CreateFileA+0x11b
```

この問題をトラブルシューティングする方法を次に示します。

 **スタックの呼び出しに関する問題のトラブルシューティング**

1.  デバッガーがスタックしているセルを所有するプロセスをデバッグすることを確認します。 (これは、RPC でハングの疑いがあるクライアントのスレッドを格納しているプロセスです)。

2.  このスレッドのスタック ポインターを取得します。 スタックは、前の例に示すようになります。 この例では、スタック ポインターは、0x0068FBA0 が。

3.  このスレッドの呼び出し情報を取得します。 そうために使用して、 [ **! rpcexts.rpcreadstack** ](-rpcexts-rpcreadstack.md)のスレッドに拡張機能のポインターからそのパラメーターとしての次のようにスタックします。

    ```dbgcmd
    0:001> !rpcexts.rpcreadstack 68fba0
    CallID: 1
    IfStart: 19bb5061
    ProcNum: 0
            Protocol Sequence:      "ncacn_ip_tcp"  (Address: 00692ED8)
            NetworkAddress: ""      (Address: 00692F38)
            Endpoint:       "1120"  (Address: 00693988)
    ```

    ここに表示される情報は、呼び出しをトレースできます。

4.  ネットワーク アドレスは空で、ローカル コンピューターを示します。 エンドポイントは、1120 です。 このエンドポイントをホストしているプロセスを決定する必要があります。 これ行うには、このエンドポイント数を渡すことによって、 [ **! rpcexts.getendpointinfo** ](-rpcexts-getendpointinfo.md)次のように、拡張機能。

    ```dbgcmd
    0:001> !rpcexts.getendpointinfo 1120
    Searching for endpoint info ...
    PID  CELL ID   ST PROTSEQ        ENDPOINT
    --------------------------------------------
    0278 0000.0001 01            TCP 1120
    ```

5.  上記の点から、0x278 プロセスにこのエンドポイントが含まれているを確認できます。 かどうかはこのプロセスで認識しているこの呼び出しについての情報を使用するかを調べる、 [ **! rpcexts.getcallinfo** ](-rpcexts-getcallinfo.md)拡張機能。 この拡張機能では、4 つのパラメーターが必要です。*CallID*、 *IfStart*、および*ProcNum* (が見つかりました手順 3. で)、および*ProcessID* 0x278 の。

    ```dbgcmd
    0:001> !rpcexts.getcallinfo 1 19bb5061 0 278
    Searching for call info ...
    PID  CELL ID   ST PNO IFSTART  TIDNUMBER CALLFLAG CALLID   LASTTIME CONN/CLN
    ----------------------------------------------------------------------------
    0278 0000.0004 02 000 19bb5061 0000.0002 00000001 00000001 00072c09 0000.0003
    ```

6.  手順 5. で情報は、役立ちますが、ある程度の省略形です。 セルの ID は、2 番目の列で 0000.0004 として指定されます。 プロセス ID と、このセルの番号を渡すと、 [ **! rpcexts.getdbgcell** ](-rpcexts-getdbgcell.md)拡張機能では、このセルより読みやすい表示が表示されます。

    ```dbgcmd
    0:001> !rpcexts.getdbgcell 278 0.4
    Getting cell info ...
    Call
    Status: Dispatched
    Procedure Number: 0
    Interface UUID start (first DWORD only): 19BB5061
    Call ID: 0x1 (1)
    Servicing thread identifier: 0x0.2
    Call Flags: cached
    Last update time (in seconds since boot):470.25 (0x1D6.19)
    Owning connection identifier: 0x0.3
    ```

    呼び出しが、「ディスパッチ」状態が表示されますを意味すると RPC ランタイムがままです。 最終更新時刻は、470.25 です。 使用して、現在の時刻を確認できます、 [ **! rpcexts.rpctime** ](-rpcexts-rpctime.md)拡張機能。

    ```dbgcmd
    0:001> !rpcexts.rpctime
    Current time is: 6003, 422
    ```

    この呼び出しと最後の接続した約 5533 秒前は約 92 分が表示されます。 そのため、スタックしている呼び出しがあります。

7.  最後の手順として、サーバー プロセスにデバッガーをアタッチする前にサービスのスレッド識別子を使用して、呼び出しを処理する現在のスレッドを分離できます。 これは、別のセル数。手順 6 で"0x0.2"として表示します。 次のように使用することができます。

    ```dbgcmd
    0:001> !rpcexts.getdbgcell 278 0.2
    Getting cell info ...
    Thread
    Status: Dispatched
    Thread ID: 0x1A4 (420)
    Last update time (in seconds since boot):470.25 (0x1D6.19)
    ```

    今すぐ 0x278 のプロセス スレッド 0x1A4 を探していることがわかります。

スレッドが別の RPC 呼び出しを行っていることができます。 必要に応じて、この手順を繰り返すことによって、この呼び出しをトレースできます。

**注**  この手順は、クライアント スレッドがわかっている場合は、サーバー スレッドを見つける方法を示しています。 逆の手法の例は、次を参照してください。 [、呼び出し元から、サーバー スレッドを識別する](identifying-the-caller-from-the-server-thread.md)します。

 

 

 





