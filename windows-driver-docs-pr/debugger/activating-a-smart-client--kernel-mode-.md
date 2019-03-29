---
title: スマート クライアントのアクティブ化 (カーネル モード)
description: KD 接続のサーバーがアクティブになるは、別のコンピューターでスマート クライアントを作成し、デバッグ セッションを開始します。
ms.assetid: bf0f1dd5-e6dc-4168-8476-cf21e77bd335
keywords:
- デバッグ スマート クライアント (カーネル モード) の Windows アクティブ化します。
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Activating a Smart Client (Kernel Mode)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e0db7c53d27c0cfb5ae753b4f3c6160d7a8ef859
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574091"
---
# <a name="activating-a-smart-client-kernel-mode"></a>スマート クライアントのアクティブ化 (カーネル モード)


KD 接続のサーバーがアクティブになるは、別のコンピューターでスマート クライアントを作成し、デバッグ セッションを開始します。

スマート クライアントを開始する 2 つの方法はあります。 カーネル プロトコルを使用した KD または WinDbg を起動して**kdsrv**、WinDbg のグラフィカル インターフェイスを使用して、または。

KD 接続のサーバーで使用されるリモート転送プロトコルを指定する必要があります。 KD 接続のサーバーと、対象のコンピューター間の実際のカーネル接続用のプロトコルを指定することもできます。 または、既定値を使用することができます。

スマート クライアントを起動するための一般的な構文は、使用されるプロトコルに依存します。 次のオプションがあります。

```console
Debugger -k kdsrv:server=@{npipe:server=Server,pipe=PipeName[,password=Password]},trans=@{ConnectType} [Options]

Debugger -k kdsrv:server=@{tcp:server=Server,port=Socket[,password=Password][,ipversion=6]},trans=@{ConnectType} [Options]

Debugger -k kdsrv:server=@{tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6]},trans=@{ConnectType} [Options]

Debugger -k kdsrv:server=@{com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password]},trans=@{ConnectType} [Options]

Debugger -k kdsrv:server=@{spipe:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,pipe=PipeName[,password=Password]},trans=@{ConnectType} [Options]

Debugger -k kdsrv:server=@{ssl:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,port=Socket[,password=Password]},trans=@{ConnectType} [Options]

Debugger -k kdsrv:server=@{ssl:proto=Protocol,{certuser=Cert|machuser=Cert},clicon=Server,port=Socket[,password=Password]},trans=@{ConnectType} [Options]
```

グラフィカル インターフェイスを使用して、KD 接続のサーバーに接続する WinDbg は休止モードである必要があります--にする必要がありますか、開始されているコマンド ライン パラメーター、または前のデバッグ セッションが終了したする必要があります。 選択、**ファイル |リモートのスタブに接続する**メニュー コマンド。 ときに、**スタブのリモート サーバーへの接続**への文字列の次のいずれかを入力します ダイアログ ボックスが表示されたら、**接続文字列**テキスト ボックス。

```dbgcmd
npipe:server=Server,pipe=PipeName[,password=Password] 

tcp:server=Server,port=Socket[,password=Password][,ipversion=6] 

tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6] 

com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password] 

spipe:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,pipe=PipeName[,password=Password] 

ssl:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,port=Socket[,password=Password] 

ssl:proto=Protocol,{certuser=Cert|machuser=Cert},clicon=Server,port=Socket[,password=Password] 
```

また、使用することができます、**参照**KD 接続のアクティブなサーバーを検索するボタンをクリックします。 参照してください[ファイル |リモートのスタブに接続する](file---connect-to-remote-stub.md)詳細についてはします。

## <span id="ddk_activating_a_smart_client_kernel_mode__dbg"></span><span id="DDK_ACTIVATING_A_SMART_CLIENT_KERNEL_MODE__DBG"></span>


前のコマンドでのパラメーターはある値は、次のとおりです。

<span id="________Debugger"></span><span id="________debugger"></span><span id="________DEBUGGER"></span> *デバッガー*  
KD または WinDbg を使用できます。

<span id="Server"></span><span id="server"></span><span id="SERVER"></span>*サーバー*  
これは、ネットワーク名または KD 接続のサーバーが作成されたコンピューターの IP アドレス。2 つの初期の円記号 (\\ \)は、コマンドラインで省略できますが、WinDbg ダイアログ ボックスでは許可されません。

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span> **pipe=** *PipeName*  
NPIPE または SPIPE プロトコルを使用すると場合、 *PipeName* KD 接続のサーバーが作成されたときに、パイプに指定された名前を指定します。

サーバー コンピューターにアクセス権を持つアカウントを使用してクライアント コンピューターにログオンしていない場合は、ユーザー名とパスワードを指定する必要があります。 クライアント コンピューターでは、コマンド プロンプト ウィンドウで、次のコマンドを入力します。

**net \\ \\**  <em>Server</em>**\\ipc$/user:**<em>ユーザー名</em>

場所*サーバー* 、サーバー コンピューターの名前を指定し、*ユーザー名*をサーバー コンピューターへのアクセスを持つアカウントの名前を指定します。

メッセージが表示されたらのパスワードを入力します。 *UserName*します。

使用してスマート クライアントをアクティブ化できますこのコマンドが成功すると、 **-k kdsrv**または WinDbg のグラフィカル インターフェイスを使用しています。

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span> **ポート =** *ソケット*  
TCP または SSL プロトコルを使用すると場合、*ソケット*KD 接続のサーバーが作成されたときに使用された同じソケットのポート番号です。

<span id="clicon"></span><span id="CLICON"></span>**clicon**  
KD 接続のサーバーが逆方向の接続を使用してスマート クライアントに接続しようとするを指定します。 クライアントを使用する必要があります**clicon**サーバーが使用する場合にのみ**clicon**します。 ほとんどの場合、逆方向の接続を使用すると、スマート クライアントは KD 接続のサーバーの前に開始されます。

<span id="port_________COMPort"></span><span id="port_________comport"></span><span id="PORT_________COMPORT"></span>**port=** *COMPort*  
COM のプロトコルを使用すると場合、 *com ポート*使用する COM ポートを指定します。 プレフィックス"COM"は省略可能 - たとえば、"com2"および「2」の両方が許容されます。

<span id="baud_________BaudRate"></span><span id="baud_________baudrate"></span><span id="BAUD_________BAUDRATE"></span>**ボー =** *BaudRate*  
COM のプロトコルを使用すると場合、 *BaudRate* KD 接続のサーバーの作成時に選択したボー レートが一致する必要があります。

<span id="channel_________COMChannel"></span><span id="channel_________comchannel"></span><span id="CHANNEL_________COMCHANNEL"></span>**channel=** *COMChannel*  
COM のプロトコルを使用すると場合、 *COMChannel* KD 接続のサーバーの作成時に選択したチャンネル番号が一致する必要があります。

<span id="________proto_________Protocol"></span><span id="________proto_________protocol"></span><span id="________PROTO_________PROTOCOL"></span> **proto =** *プロトコル*  
SSL または SPIPE プロトコルを使用すると場合、*プロトコル*KD 接続のサーバーが作成されたときに使用するセキュリティで保護されたプロトコルに一致する必要があります。

<span id="________Cert"></span><span id="________cert"></span><span id="________CERT"></span> *証明書*  
同一を使用する必要があります SSL または SPIPE プロトコルを使用すると場合、 **certuser =**<em>Cert</em>または**machuser =**<em>Cert</em>がパラメーターときに使用KD 接続のサーバーが作成されました。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span> **パスワード =** *パスワード*  
パスワードが KD 接続のサーバーが作成されたときに使用された場合*パスワード*スマート クライアントを作成するために指定する必要があります。 元のパスワードに一致する必要があります。 パスワードは大文字小文字が区別されます。 エラー メッセージが「エラー 0x80004005」を指定、間違ったパスワードが指定されている場合

<span id="________ipversion_6"></span><span id="________IPVERSION_6"></span> **ipversion=6**  
(デバッグ ツールの Windows 6.6.07 以前のみ)強制的に IP version 6 を使用するデバッガー バージョン 4 TCP を使用して、インターネットに接続するのではなく。 Windows Vista およびそれ以降のバージョンでは、デバッガーは、IP バージョン 6、このオプションが不要なために既定値の自動を試みます。

<span id="________trans___________ConnectType_________"></span><span id="________trans___________connecttype_________"></span><span id="________TRANS___________CONNECTTYPE_________"></span> **trans=@{** *ConnectType* **}**  
デバッガーのターゲットに接続する方法を指示します。 次のカーネル接続プロトコルが許可されています。

```dbgcmd
com:port=ComPort,baud=BaudRate 
1394:channel=1394Channel[,symlink=1394Protocol] 
usb2:targetname=String 
com:pipe,port=\\VMHost\pipe\PipeName[,resets=0][,reconnect]
com:modem 
```

これらのプロトコルについては、次を参照してください。[を取得する設定をデバッグ用](getting-set-up-for-debugging.md)します。 これらのプロトコルのパラメーターのいずれかを省略できますなど言えます**trans=@{com:}** --KdSrv が実行されているコンピューター上の環境変数で指定された値をデバッガーは既定の設定。

<span id="Options"></span><span id="options"></span><span id="OPTIONS"></span>*オプション*  
ここに、追加のコマンド ライン パラメーターを配置することができます。 参照してください[コマンド ライン オプション](command-line-options.md)完全な一覧についてはします。

KD 接続のサーバーが単にスマート クライアントの場合、その他のゲートウェイとして機能するので*オプション*場合使用のコンピューターでカーネル デバッガーを開始した KdSrv が実行されているものと同じになります。 この例外は、パスを指定するオプションかファイル名は、コンピューター上のパスとしてスマート クライアントが実行されています。

 

 





