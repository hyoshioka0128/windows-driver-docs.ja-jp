---
title: スマート クライアントのアクティブ化
description: DbgSrv のプロセス サーバーがアクティブになるは、別のコンピューターでスマート クライアントを作成し、デバッグ セッションを開始します。
ms.assetid: 7199dc95-e8fc-4f58-ab6e-c0141681113e
keywords:
- デバッグ スマート クライアントの Windows アクティブ化します。
ms.date: 02/28/2019
topic_type:
- apiref
api_name:
- Activating a Smart Client
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e9db6fc4eead1efd0e893f62de4494a3f4be37f4
ms.sourcegitcommit: b13e6d44c71197971697f710c0ecb23db13fea91
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57203937"
---
# <a name="activating-a-smart-client"></a>スマート クライアントのアクティブ化


DbgSrv のプロセス サーバーがアクティブになるは、別のコンピューターでスマート クライアントを作成し、デバッグ セッションを開始します。

スマート クライアントを開始する 2 つの方法はあります: CDB または WinDbg を起動して、- premote で[コマンド ライン オプション](command-line-options.md)WinDbg のグラフィカル インターフェイスを使用して、または。

スマート クライアントのプロトコルは、プロセス サーバーのプロトコルと一致する必要があります。 スマート クライアントを起動するための一般的な構文は、使用されるプロトコルに依存します。 次のオプションがあります。

```console
Debugger -premote npipe:server=Server,pipe=PipeName[,password=Password] [Options]

Debugger -premote tcp:server=Server,port=Socket[,password=Password][,ipversion=6] [Options]

Debugger -premote tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6] [Options]

Debugger -premote com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password] [Options]

Debugger -premote spipe:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,pipe=PipeName[,password=Password] [Options]

Debugger -premote ssl:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,port=Socket[,password=Password] [Options]

Debugger -premote ssl:proto=Protocol,{certuser=Cert|machuser=Cert},clicon=Server,port=Socket[,password=Password] [Options]
```

グラフィカル インターフェイスを使用して、プロセス サーバーに接続する WinDbg は休止モードである必要があります--にする必要がありますか、開始されているコマンド ライン パラメーター、または前のデバッグ セッションが終了したする必要があります。 選択、**ファイル |リモートのスタブに接続する**メニュー コマンド。 ときに、**スタブのリモート サーバーへの接続**への文字列の次のいずれかを入力します ダイアログ ボックスが表示されたら、**接続文字列**テキスト ボックス。

```dbgcmd
npipe:server=Server,pipe=PipeName[,password=Password] 

tcp:server=Server,port=Socket[,password=Password][,ipversion=6] 

tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6] 

com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password] 

spipe:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,pipe=PipeName[,password=Password] 

ssl:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,port=Socket[,password=Password] 

ssl:proto=Protocol,{certuser=Cert|machuser=Cert},clicon=Server,port=Socket[,password=Password] 
```

また、使用することができます、**参照**アクティブなプロセス サーバーを検索するボタンをクリックします。 参照してください[ファイル |リモートのスタブに接続する](file---connect-to-remote-stub.md)詳細についてはします。

## <span id="ddk_activating_a_smart_client_dbg"></span><span id="DDK_ACTIVATING_A_SMART_CLIENT_DBG"></span>


前のコマンドでのパラメーターはある値は、次のとおりです。

<span id="________Debugger"></span><span id="________debugger"></span><span id="________DEBUGGER"></span> *デバッガー*  
これには、CDB または WinDbg を指定できます。

<span id="________Server"></span><span id="________server"></span><span id="________SERVER"></span> *サーバー*  
これは、ネットワーク名またはプロセス サーバーが作成されたコンピューターの IP アドレス。 2 つの初期の円記号 (\\ \)は、コマンドラインで省略できますが、WinDbg ダイアログ ボックスでは許可されません。

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span> **pipe=** *PipeName*  
NPIPE または SPIPE プロトコルを使用すると場合、 *PipeName*プロセス サーバーの作成時に、パイプに指定された名前を指定します。

サーバー コンピューターにアクセス権を持つアカウントを使用してクライアント コンピューターにログオンしていない場合は、ユーザー名とパスワードを指定する必要があります。 クライアント コンピューターでは、コマンド プロンプト ウィンドウで、次のコマンドを入力します。

**net \\ \\**  <em>Server</em>**\\ipc$/user:**<em>ユーザー名</em>

場所*サーバー* 、サーバー コンピューターの名前を指定し、*ユーザー名*をサーバー コンピューターへのアクセスを持つアカウントの名前を指定します。

メッセージが表示されたらのパスワードを入力します。 *UserName*します。

使用してスマート クライアントをアクティブ化できますこのコマンドが成功した後、 **-premote**コマンド ライン オプションまたは WinDbg のグラフィカル インターフェイスを使用しています。

**注**  ファイルとプリンターの共有サーバー コンピューターを有効にする必要があります。 コントロール パネルに移動します。**ネットワークとインターネット&gt;ネットワークと共有センター&gt;共有の詳細設定**します。 選択**ファイルとプリンターの共有を有効に**します。

 

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span> **ポート =** *ソケット*  
TCP または SSL プロトコルを使用すると場合、*ソケット*はプロセス サーバーが作成されたときに使用された同じソケットのポート番号です。

<span id="________clicon"></span><span id="________CLICON"></span> **clicon**  
プロセス サーバーが逆方向の接続を使用してスマート クライアントに接続しようとするを指定します。 クライアントを使用する必要があります**clicon**サーバーが使用する場合にのみ**clicon**します。 ほとんどの場合、逆方向の接続を使用すると、スマート クライアントは、プロセス サーバーの前に開始されます。

<span id="port_________COMPort"></span><span id="port_________comport"></span><span id="PORT_________COMPORT"></span>**port=** *COMPort*  
COM のプロトコルを使用すると場合、 *com ポート*使用する COM ポートを指定します。 プレフィックス"COM"は省略可能 - たとえば、"com2"および「2」の両方が許容されます。

<span id="baud_________BaudRate"></span><span id="baud_________baudrate"></span><span id="BAUD_________BAUDRATE"></span>**ボー =** *BaudRate*  
COM のプロトコルを使用すると場合、 *BaudRate*プロセス サーバーの作成時に選択したボー レートが一致する必要があります。

<span id="channel_________COMChannel"></span><span id="channel_________comchannel"></span><span id="CHANNEL_________COMCHANNEL"></span>**channel=** *COMChannel*  
COM のプロトコルを使用すると場合、 *COMChannel*プロセス サーバーの作成時に選択したチャンネル番号が一致する必要があります。

<span id="________proto_________Protocol"></span><span id="________proto_________protocol"></span><span id="________PROTO_________PROTOCOL"></span> **proto =** *プロトコル*  
SSL または SPIPE プロトコルを使用すると場合、*プロトコル*プロセス サーバーが作成されたときに使用されるセキュリティで保護されたプロトコルに一致する必要があります。

<span id="Cert"></span><span id="cert"></span><span id="CERT"></span>*証明書*  
同一を使用する必要があります SSL または SPIPE プロトコルを使用すると場合、 **certuser =**<em>Cert</em>または**machuser =**<em>Cert</em>がパラメーターときに使用プロセス サーバーが作成されました。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span> **パスワード =** *パスワード*  
パスワードが、プロセス サーバーが作成されたときに使用された場合*パスワード*スマート クライアントを作成するために指定する必要があります。 元のパスワードに一致する必要があります。 パスワードは大文字小文字が区別されます。 エラー メッセージが「エラー 0x80004005」を指定、間違ったパスワードが指定されている場合

<span id="________________ipversion_6"></span><span id="________________IPVERSION_6"></span> **ipversion=6**  
(デバッグ ツールの Windows 6.6.07 以前のみ)強制的に IP version 6 を使用するデバッガー バージョン 4 TCP を使用して、インターネットに接続するのではなく。 Windows Vista およびそれ以降のバージョンでは、デバッガーは、IP バージョン 6、このオプションが不要なために既定値の自動を試みます。

<span id="Options"></span><span id="options"></span><span id="OPTIONS"></span>*オプション*  
ここに、追加のコマンド ライン パラメーターを配置することができます。 参照してください[コマンド ライン オプション](command-line-options.md)完全な一覧についてはします。 CDB を使用している場合は、デバッグするプロセスを指定このする必要があります。 WinDbg を使用している場合は、コマンドラインで、またはグラフィカル インターフェイスからプロセスを指定できます。

プロセス サーバーが単にスマート クライアントの場合、その他のゲートウェイとして機能するので*オプション*はターゲット アプリケーションと同じコンピューター上、ユーザー モード デバッガーが起動された場合を使用するものと同じになります。

使用する場合、 **-premote**オプションと[ **.attach (プロセスにアタッチ)** ](-attach--attach-to-process-.md)または[ **(プロセスの作成) に関する**](-create--create-process-.md)、パラメーターは上記と同じです。

## <a name="troubleshooting"></a>トラブルシューティング

このメッセージ場合があります。*クライアントがサーバーとして同じバージョンのリモート処理プロトコルを使用しない*DbgSrv に接続しようとしているのバージョンが WinDbg のバージョンよりも、別のプロトコルのバージョンを使用することを示します。 

共通のプロトコルの変更が行われることはできません。 これが発生する場合は DbgSrv と WinDbg または WinDbg Preview の最新バージョンの一致するバージョンを使用してください。 最新バージョンをダウンロードする方法の詳細については、次を参照してください。[デバッグ ツールの Windows にダウンロード](debugger-download-tools.md)します。

 

 





