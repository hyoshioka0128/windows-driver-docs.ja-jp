---
title: .endsrv (デバッグ サーバーの終了)
description: .Endsrv コマンドでは、アクティブなデバッグ サーバーをキャンセルするデバッガーを実行します。
ms.assetid: 6be6c774-fe6b-4bd4-8174-55ef207db3e6
keywords:
- .endsrv (エンド デバッグ サーバー) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .endsrv (End Debugging Server)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d2dbf56eebfa51b66db806433fdb10a94722ec8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571317"
---
# <a name="endsrv-end-debugging-server"></a>.endsrv (デバッグ サーバーの終了)


**.Endsrv**コマンドにより、デバッガーをアクティブなデバッグ サーバーを取り消します。

```dbgcmd
.endsrv ServerID 
```

## <a name="span-idddkmetaenddebuggingserverdbgspanspan-idddkmetaenddebuggingserverdbgspanparameters"></a><span id="ddk_meta_end_debugging_server_dbg"></span><span id="DDK_META_END_DEBUGGING_SERVER_DBG"></span>パラメーター


<span id="_______ServerID______"></span><span id="_______serverid______"></span><span id="_______SERVERID______"></span> *サーバー Id*   
デバッグ サーバーの ID を指定します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

このコマンドは、デバッガーからのリモート デバッグを実行している場合にのみ使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

リモート デバッグの詳細については、[リモート デバッグで、デバッガー](remote-debugging-through-the-debugger.md)を参照してください。

<a name="remarks"></a>コメント
-------

発行する必要があります、 **.endsrv**デバッグ サーバーまたは 1 つのデバッグのサーバーに接続されているデバッグ クライアントからコマンド。

デバッグ サーバーの ID を調べるには、 [ **.servers (デバッグ サーバーの一覧)** ](-servers--list-debugging-servers-.md)コマンド。

**.Endsrv**コマンドは、デバッグのサーバーを終了できますが、プロセス サーバー、または KD 接続サーバーので終了することはできません。 これらのサーバーを終了する方法については、[プロセス サーバーのセッションを制御する](controlling-a-process-server-session.md)と[KD 接続サーバー セッションを制御する](controlling-a-kd-connection-server-session.md)を参照してください。 (がある、ただし、1 つの例外的な場合 **.endsrv**をプログラムで起動されました詳細については、次を参照してください。 プロセス サーバーを終了できます[ **IDebugClient::StartProcessServer** 。](https://msdn.microsoft.com/library/windows/hardware/ff558810).)

デバッグ サーバーをキャンセルした場合、サーバーにアタッチ今後デバッグ クライアントを防ぐ。 ただし、デバッグ サーバーをキャンセルすると、サーバーから現在接続されているすべてのクライアントが切断できません。

次のような状況を検討してください。 次の例のようにデバッグの一部のサーバーを起動するとします。

```dbgcmd
0:000> .server npipe:pipe=rabbit
Server started with 'npipe:pipe=rabbit'
0:000> .server tcp:port=7
Server started with 'tcp:port=7'
```

次に、次の例として、パスワードを使用すること。

```dbgcmd
0:000> .server npipe:pipe=tiger,password=hardtoguess
Server started with 'npipe:pipe=tiger,password=hardtoguess'
```

ただし、以前のサーバーもを実行しているため、次の例のように、それらを取り消す必要があります。

```dbgcmd
0:000> .servers
0 - Debugger Server - npipe:Pipe=rabbit
1 - Debugger Server - tcp:Port=7
2 - Debugger Server - npipe:Pipe=tiger,Password=*
0:000> .endsrv 0
Server told to exit.  Actual exit may be delayed until
the next connection attempt.
0:000> .endsrv 1
Server told to exit.  Actual exit may be delayed until
the next connection attempt.
0:000> .servers
0 - <Disabled, exit pending>
1 - <Disabled, exit pending>
2 - Debugger Server - npipe:Pipe=tiger,Password=*
```

最後に、以前のサーバーにアクティブだったときに、コンピューターに接続された何もないように、使用、 [ **.clients (デバッグ クライアントを一覧表示)** ](-clients--list-debugging-clients-.md)コマンド。

```dbgcmd
0:000> .clients
HotMachine\HostUser, last active Mon Mar 04 16:05:21 2002
```

**注意**  パスワードが暗号化されていないため、少量の保護のみを提供するパスワード TCP、NPIPE、または COM のプロトコルを使用します。 SSL または SPIPE プロトコルと共にパスワードを使用する場合、パスワードは暗号化されます。 セキュリティで保護されたリモート セッションを確立する場合は、SSL または SPIPE プロトコルを使用する必要があります。

 

 

 





