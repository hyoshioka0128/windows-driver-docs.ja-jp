---
title: .endsrv (デバッグ サーバーの終了)
description: Endsrv コマンドを実行すると、デバッガーはアクティブなデバッグサーバーをキャンセルします。
ms.assetid: 6be6c774-fe6b-4bd4-8174-55ef207db3e6
keywords:
- endsrv (デバッグサーバーの終了) Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .endsrv (End Debugging Server)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4f88bed3079c61ca88edb5f8beab9b0bb9ece48e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837603"
---
# <a name="endsrv-end-debugging-server"></a>.endsrv (デバッグ サーバーの終了)


**Endsrv**コマンドを実行すると、デバッガーはアクティブなデバッグサーバーをキャンセルします。

```dbgcmd
.endsrv ServerID 
```

## <a name="span-idddk_meta_end_debugging_server_dbgspanspan-idddk_meta_end_debugging_server_dbgspanparameters"></a><span id="ddk_meta_end_debugging_server_dbg"></span><span id="DDK_META_END_DEBUGGING_SERVER_DBG"></span>パラメータ


<span id="_______ServerID______"></span><span id="_______serverid______"></span><span id="_______SERVERID______"></span>*サーバー id*   
デバッグサーバーの ID を指定します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

このコマンドは、デバッガーを使用してリモートデバッグを実行している場合にのみ使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Modes</strong></p></td>
<td align="left"><p>ユーザーモードのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Platforms</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

リモートデバッグの詳細については、「[デバッガーを使用したリモートデバッグ](remote-debugging-through-the-debugger.md)」を参照してください。

<a name="remarks"></a>注釈
-------

デバッグサーバーから、またはデバッグサーバーに接続されているいずれかのデバッグクライアントから、 **endsrv**コマンドを発行する必要があります。

デバッグサーバーの ID を確認するには、 [ **. servers (List デバッグサーバー)** ](-servers--list-debugging-servers-.md)コマンドを使用します。

**Endsrv**コマンドはデバッグサーバーを終了できますが、プロセスサーバーまたは KD 接続サーバーを終了することはできません。 これらのサーバーを終了する方法の詳細については、「[プロセスサーバーセッションを制御](controlling-a-process-server-session.md)する」および「 [KD 接続サーバーセッションを制御](controlling-a-kd-connection-server-session.md)する」を参照してください。 (ただし、プログラムによって起動されたプロセスサーバーを**endsrv**が終了できる場合もあります。詳細については、「 [**IDebugClient:: StartProcessServer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-startprocessserver)」を参照してください)。

デバッグサーバーをキャンセルした場合は、今後のデバッグクライアントがサーバーにアタッチできなくなります。 ただし、デバッグサーバーをキャンセルした場合、サーバーを介して現在アタッチされているクライアントはデタッチされません。

次のような状況が考えられます。 次の例に示すように、いくつかのデバッグサーバーを起動するとします。

```dbgcmd
0:000> .server npipe:pipe=rabbit
Server started with 'npipe:pipe=rabbit'
0:000> .server tcp:port=7
Server started with 'tcp:port=7'
```

次の例に示すように、パスワードを使用することを決定します。

```dbgcmd
0:000> .server npipe:pipe=tiger,password=hardtoguess
Server started with 'npipe:pipe=tiger,password=hardtoguess'
```

ただし、次の例に示すように、以前のサーバーはまだ実行されているので、キャンセルする必要があります。

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

最後に、以前のサーバーがアクティブになっている間にコンピューターに何もアタッチされていないことを確認するには、[[**クライアント (デバッグクライアントの一覧)** ](-clients--list-debugging-clients-.md) ] コマンドを使用します。

```dbgcmd
0:000> .clients
HotMachine\HostUser, last active Mon Mar 04 16:05:21 2002
```

**注意**   TCP、npipe、または COM プロトコルでパスワードを使用すると、パスワードが暗号化されないため、わずかな保護しか提供されません。 SSL または SPIPE プロトコルと共にパスワードを使用すると、パスワードは暗号化されます。 セキュリティで保護されたリモートセッションを確立する場合は、SSL または SPIPE プロトコルを使用する必要があります。

 

 

 





