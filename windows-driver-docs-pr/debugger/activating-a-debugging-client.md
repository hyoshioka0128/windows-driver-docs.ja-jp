---
title: デバッグ クライアントのアクティブ化
description: デバッグ サーバーがアクティブになると、別のコンピューターでデバッグ クライアントを起動し、デバッグ セッションに接続できます。
ms.assetid: 45a7baa7-08dc-47ae-a137-874aaa4ec8aa
keywords:
- デバッグ デバッグ クライアント Windows アクティブ化します。
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Activating a Debugging Client
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 270529b9c1120e805c8de880d34666d778454d03
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353662"
---
# <a name="activating-a-debugging-client"></a>デバッグ クライアントのアクティブ化


デバッグ サーバーがアクティブになると、別のコンピューターでデバッグ クライアントを起動し、デバッグ セッションに接続できます。

デバッグ クライアントを起動する 2 つの方法はあります: を使用して、リモート[コマンド ライン オプション](command-line-options.md)WinDbg のグラフィカル インターフェイスを使用して、または。

クライアントのプロトコルは、サーバーのプロトコルと一致する必要があります。 デバッグ クライアントを起動するための一般的な構文は、使用されるプロトコルに依存します。 次のオプションがあります。

```dbgcmd
Debugger -remote npipe:server=Server,pipe=PipeName[,password=Password] 

Debugger -remote tcp:server=Server,port=Socket[,password=Password][,ipversion=6] 

Debugger -remote tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6] 

Debugger -remote com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password] 

Debugger -remote spipe:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,pipe=PipeName[,password=Password] 

Debugger -remote ssl:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,port=Socket[,password=Password] 

Debugger -remote ssl:proto=Protocol,{certuser=Cert|machuser=Cert},clicon=Server,port=Socket[,password=Password] 
```

グラフィカル インターフェイスを使用して、リモート デバッグ セッションに接続する WinDbg は休止モードである必要があります--にする必要がありますか、開始されているコマンド ライン パラメーター、または前のデバッグ セッションが終了したする必要があります。 選択、**ファイル |リモート セッションに接続する**メニュー コマンド、または、CTRL キーを押しながら R キーのショートカット キーを押します。 ときに、**リモート デバッガー セッションへの接続**への文字列の次のいずれかを入力します ダイアログ ボックスが表示されたら、**接続文字列**テキスト ボックス。

```dbgcmd
npipe:server=Server,pipe=PipeName[,password=Password] 

tcp:server=Server,port=Socket[,password=Password][,ipversion=6] 

tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6] 

com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password] 

spipe:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,pipe=PipeName[,password=Password] 

ssl:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,port=Socket[,password=Password] 

ssl:proto=Protocol,{certuser=Cert|machuser=Cert},clicon=Server,port=Socket[,password=Password] 
```

また、使用することができます、**参照**アクティブ デバッグ サーバーを検索するボタンをクリックします。 参照してください[ファイル |リモート セッションに接続する](file---connect-to-remote-session.md)詳細についてはします。

## <span id="ddk_activating_a_debugging_client_dbg"></span><span id="DDK_ACTIVATING_A_DEBUGGING_CLIENT_DBG"></span>


前のコマンドでのパラメーターはある値は、次のとおりです。

<span id="________Debugger"></span><span id="________debugger"></span><span id="________DEBUGGER"></span> *デバッガー*  
これは、デバッグのクライアントによって使用されるものと同じデバッガーにはありません--WinDbg、KD、CDB はすべて、デバッガーからのリモート デバッグの目的で交換可能です。

<span id="________Server"></span><span id="________server"></span><span id="________SERVER"></span> *サーバー*  
これは、ネットワーク名またはデバッグ サーバーが作成されたコンピューターの IP アドレス。 2 つの初期の円記号 (\\ \)は、コマンドラインで省略できますが、WinDbg ダイアログ ボックスでは許可されません。

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span> **pipe=** *PipeName*  
NPIPE または SPIPE プロトコルを使用すると場合、 *PipeName*サーバーの作成時に、パイプに指定された名前を指定します。

サーバー コンピューターにアクセス権を持つアカウントを使用してクライアント コンピューターにログオンしていない場合は、ユーザー名とパスワードを指定する必要があります。 クライアント コンピューターでは、コマンド プロンプト ウィンドウで、次のコマンドを入力します。

**net \\ \\**  <em>Server</em>**\\ipc$/user:**<em>ユーザー名</em>

場所*サーバー* 、サーバー コンピューターの名前を指定し、*ユーザー名*をサーバー コンピューターへのアクセスを持つアカウントの名前を指定します。

メッセージが表示されたらのパスワードを入力します。 *UserName*します。

デバッグ クライアントをアクティブ化を使用してこのコマンドが成功した後にする、 **-リモート**コマンド ライン オプションまたは WinDbg のグラフィカル インターフェイスを使用しています。

**注**  ファイルとプリンターの共有サーバー コンピューターを有効にする必要があります。 コントロール パネルに移動します。**ネットワークとインターネット&gt;ネットワークと共有センター&gt;共有の詳細設定**します。 選択**ファイルとプリンターの共有を有効に**します。

 

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span> **ポート =** *ソケット*  
TCP または SSL プロトコルを使用すると場合、*ソケット*は、サーバーが作成されたときに使用された同じソケットのポート番号です。

<span id="clicon"></span><span id="CLICON"></span>**clicon**  
デバッグ サーバーが逆方向の接続を使用してクライアントに接続しようとするを指定します。 クライアントを使用する必要があります**clicon**サーバーが使用する場合にのみ**clicon**します。 ほとんどの場合、逆方向の接続を使用する場合、デバッグ クライアントはサーバーをデバッグする前に開始されます。

<span id="________port_________COMPort"></span><span id="________port_________comport"></span><span id="________PORT_________COMPORT"></span> **port=** *COMPort*  
COM のプロトコルを使用すると場合、 *com ポート*使用する COM ポートを指定します。 プレフィックス"COM"は省略可能 - たとえば、"com2"および「2」の両方が許容されます。

<span id="baud_________BaudRate"></span><span id="baud_________baudrate"></span><span id="BAUD_________BAUDRATE"></span>**ボー =** *BaudRate*  
COM のプロトコルを使用すると場合、 *BaudRate*サーバーの作成時に選択したボー レートが一致する必要があります。

<span id="channel_________COMChannel"></span><span id="channel_________comchannel"></span><span id="CHANNEL_________COMCHANNEL"></span>**channel=** *COMChannel*  
COM のプロトコルを使用すると場合、 *COMChannel*サーバーの作成時に選択したチャンネル番号が一致する必要があります。

<span id="________proto_________Protocol"></span><span id="________proto_________protocol"></span><span id="________PROTO_________PROTOCOL"></span> **proto =** *プロトコル*  
SSL または SPIPE プロトコルを使用すると場合、*プロトコル*サーバーが作成されたときに使用されるセキュリティで保護されたプロトコルに一致する必要があります。

<span id="________Cert"></span><span id="________cert"></span><span id="________CERT"></span> *証明書*  
同一を使用する必要があります SSL または SPIPE プロトコルを使用すると場合、 **certuser =**<em>Cert</em>または**machuser =** *Cert*がパラメーターときに使用サーバーが作成されました。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span> **パスワード =** *パスワード*  
パスワードが、サーバーが作成されたときに使用された場合*パスワード*デバッグのクライアントを作成するために指定する必要があります。 元のパスワードに一致する必要があります。 パスワードは大文字小文字が区別されます。 エラー メッセージが「エラー 0x80004005」を指定、間違ったパスワードが指定されている場合 パスワードは、12 文字、または以下である必要があります。

<span id="________ipversion_6"></span><span id="________IPVERSION_6"></span> **ipversion=6**  
(デバッグ ツールの Windows 6.6.07 以前のみ)強制的に IP version 6 を使用するデバッガー バージョン 4 TCP を使用して、インターネットに接続するのではなく。 Windows Vista およびそれ以降のバージョンでは、デバッガーは、IP バージョン 6、このオプションが不要なために既定値の自動を試みます。

新しいデバッグ セッションを開始するために使用するコマンド ライン オプション (など **-p**) デバッグのクライアントではなく、サーバー、のみは使用できません。 構成オプション (など **-n**) は、クライアントまたはサーバーのいずれかから動作します。

 

 





