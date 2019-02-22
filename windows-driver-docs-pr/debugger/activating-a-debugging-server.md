---
title: デバッグ サーバー アクティブ化します。
description: デバッグ サーバーのアクティブ化の 2 つの方法はあります。
ms.assetid: aba75d2d-4077-415f-b847-023e47239e2e
keywords:
- デバッグ デバッグ サーバー Windows アクティブ化します。
ms.date: 03/02/2017
topic_type:
- apiref
api_name:
- Activating a Debugging Server
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4c2cac5496dcf0cf3b821773cea0e7b64b87a23a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558205"
---
# <a name="activating-a-debugging-server"></a>デバッグ サーバー アクティブ化します。


デバッグ サーバーのアクティブ化の 2 つの方法はあります。 使用して、デバッガーが開始されるとアクティブ化、 **-サーバー**管理者特権でコマンド プロンプト ウィンドウ (管理者として実行) でのコマンド ライン オプション。 また、デバッガーの実行後にもアクティブにできます。 管理者特権 (管理者として実行) でデバッガーを起動し、入力、 [ **.server** ](-server--create-debugging-server-.md)コマンド。

**注**  特権を昇格することがなくデバッグ サーバーをアクティブ化することができ、クライアントのデバッグはサーバーに接続することになります。 ただし、クライアントを昇格した特権でアクティブ化がない限り、デバッグ サーバーを検出することはできません。 デバッグ サーバーを検出する方法については、次を参照してください。[デバッグ サーバーの検索](searching-for-debugging-servers.md)します。

 

デバッガーは、いくつかのトランスポート プロトコルをサポートします。 名前付きパイプ (NPIPE)、TCP、COM ポート、セキュリティで保護されたパイプ (SPIPE) および secure socket layer (SSL)。

デバッグ サーバーをライセンス認証するための一般的な構文は、使用されるプロトコルに依存します。

```console
Debugger -server npipe:pipe=PipeName[,hidden][,password=Password][,IcfEnable] [-noio] [Options]

Debugger -server tcp:port=Socket[,hidden][,password=Password][,ipversion=6][,IcfEnable] [-noio] [Options]

Debugger -server tcp:port=Socket,clicon=Client[,password=Password][,ipversion=6] [-noio] [Options]

Debugger -server com:port=COMPort,baud=BaudRate,channel=COMChannel[,hidden][,password=Password] [-noio] [Options]

Debugger -server spipe:proto=Protocol,{certuser=Cert|machuser=Cert},pipe=PipeName[,hidden][,password=Password] [-noio] [Options]

Debugger -server ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket[,hidden][,password=Password] [-noio] [Options]

Debugger -server ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket,clicon=Client[,password=Password] [-noio] [Options]
```

デバッグ サーバーのアクティブ化のもう 1 つのメソッドは、使用する、 [ **.server (デバッグ サーバーの作成)** ](-server--create-debugging-server-.md)コマンドの後、デバッガーが既に開始されています。

```dbgcmd
.server npipe:pipe=PipeName[,hidden][,password=Password][,IcfEnable] 

.server tcp:port=Socket[,hidden][,password=Password][,ipversion=6][,IcfEnable] 

.server tcp:port=Socket,clicon=Client[,password=Password][,ipversion=6] 

.server com:port=COMPort,baud=BaudRate,channel=COMChannel[,hidden][,password=Password] 

.server spipe:proto=Protocol,{certuser=Cert|machuser=Cert},pipe=PipeName[,hidden][,password=Password] 

.server ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket[,hidden][,password=Password] 

.server ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket,clicon=Client[,password=Password] 
```

## <span id="ddk_activating_a_debugging_server_dbg"></span><span id="DDK_ACTIVATING_A_DEBUGGING_SERVER_DBG"></span>


前述のコマンドでパラメーターには、次の値があります。

<span id="________Debugger"></span><span id="________debugger"></span><span id="________DEBUGGER"></span> *デバッガー*  
KD、CDB、NTSD、または WinDbg を使用できます。

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span> **pipe=** *PipeName*  
NPIPE または SPIPE プロトコルを使用するとと、 *PipeName*はパイプの名前として使用する文字列です。 各パイプ名は一意なデバッグ サーバーを識別する必要があります。 パイプ名を再利用しようとした場合、エラー メッセージが表示されます。 *PipeName*スペースや引用符を含めることはできません。 *PipeName*数値を含めることができます**printf**-など、書式コードのスタイル設定 **%x**または **%d**します。 デバッガーは、デバッガーのプロセス ID でこれが置換されます。 このような 2 つ目のコードは、デバッガーのスレッド ID に置き換えられます。

**注**  ファイルとプリンターの共有、デバッグ サーバーを実行しているコンピューターを有効にする必要があります。 コントロール パネルに移動します。**ネットワークとインターネット&gt;ネットワークと共有センター&gt;共有の詳細設定**します。 選択**ファイルとプリンターの共有を有効に**します。

 

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span> **ポート =** *ソケット*  
TCP または SSL プロトコルを使用するとと、*ソケット*ソケットのポート番号です。

コロンで区切ってポートの範囲を指定することもできます。 デバッガーでは、無料かどうかをこの範囲内の各ポートを確認します。 空きポートが見つかるし、エラーが発生しない、デバッグ サーバーが作成されます。 デバッグ クライアントは、サーバーに接続するために使用される実際のポートを指定する必要があります。 を実際のポートを判断するで説明する方法のいずれかの操作を使用して[**デバッグ サーバーの検索**](searching-for-debugging-servers.md); このデバッグ サーバーが表示されたら、ポートの後、コロンで区切られた 2 つの数値。 最初の数値が使用されますが、実際のポートになります2 つ目は無視できます。 たとえば、として、ポートが指定されて**ポート = 51:60**、ポート 53 が実際に使用されるとは、検索結果が表示されます"ポート 53:60 ="。 (使用する場合、 **clicon**デバッグ クライアント リバース接続を確立するパラメーターは、サーバーが実際に使用されるポートを指定する必要がありますに、この方法でのポートの範囲を指定できます)。

<span id="________clicon_________Client"></span><span id="________clicon_________client"></span><span id="________CLICON_________CLIENT"></span> **clicon =** *クライアント*  
TCP または SSL プロトコルを使用する場合、 **clicon**パラメーターが指定されて、*接続を取り消す*が開きます。 これは、デバッグ サーバーがクライアントの連絡先を開始できるようにすることではなく、デバッグ、クライアントに接続しようとする、ことを意味します。 通常の方向での接続を妨げているファイアウォールがある場合に役立ちます。 ことができます。 *クライアント*ネットワーク名またはいるデバッグ クライアントが存在するか、作成は、コンピューターの IP アドレスを指定します。 2 つの初期の円記号 (\\ \)は省略可能です。

1 つの特定のクライアントをサーバーを検索するためは、このメソッドを使用する場合、サーバーに複数のクライアントを接続できません。 接続が拒否されるかが壊れている場合は、サーバー接続を再起動する必要があります。 逆接続サーバーは、別のデバッガーは、すべてのアクティブなサーバーを表示するときに表示されません。

**注**  とき**clicon**が使用することをお勧めですが、通常の順序 (クライアントの前にサーバー) は許可されても、デバッグのサーバーを作成する前にデバッグのクライアントを開始します。

 

<span id="port_________COMPort"></span><span id="port_________comport"></span><span id="PORT_________COMPORT"></span>**port=** *COMPort*  
COM のプロトコルを使用するとと、 *com ポート*使用する COM ポートを指定します。 プレフィックス"COM"は省略可能 - たとえば、"com2"および「2」の両方が許容されます。

<span id="baud_________BaudRate"></span><span id="baud_________baudrate"></span><span id="BAUD_________BAUDRATE"></span>**ボー =** *BaudRate*  
COM のプロトコルを使用するとと、 *BaudRate*接続を実行するボー レートを指定します。 ハードウェアでサポートされている任意のボー レートが許可されます。

<span id="channel_________COMChannel"></span><span id="channel_________comchannel"></span><span id="CHANNEL_________COMCHANNEL"></span>**channel=** *COMChannel*  
COM のプロトコルを使用すると場合、 *COMChannel*デバッグ クライアントとの通信に使用する COM チャネルを指定します。 0 ~ 254 の包括的な範囲の任意の値を指定できます。 別のチャンネル番号を使用して複数の接続の 1 つの COM ポートを使用することができます。 (これは、COM ポートを使用して、デバッグ ケーブル異なります--ような状況では、COM ポート内でチャネルを使うことはできません)。

<span id="________proto_________Protocol"></span><span id="________proto_________protocol"></span><span id="________PROTO_________PROTOCOL"></span> **proto =** *プロトコル*  
SSL または SPIPE プロトコルを使用すると場合、*プロトコル*Secure Channel (S チャネル) プロトコルを指定します。 文字列 tls1、pct1、ssl2、または ssl3 のいずれかにできます。

<span id="Cert"></span><span id="cert"></span><span id="CERT"></span>*証明書*  
SSL または SPIPE プロトコルを使用すると場合、 *Cert*証明書を指定します。 証明書の名前または証明書の拇印 (証明書のスナップインで指定された 16 進数の数字の文字列) を指定できます。 場合、構文**certuser =**<em>Cert</em>が使用すると、デバッガーがシステム ストア (既定のストア) に証明書を検索します。 場合、構文**machuser =**<em>証明書</em>が使用すると、デバッガーがコンピューターのストアに証明書を検索します。 指定された証明書は、サーバー認証をサポートする必要があります。

<span id="________hidden"></span><span id="________HIDDEN"></span> **非表示**  
サーバー、別のデバッガーは、すべてのアクティブなサーバーを表示するときに表示されません。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span> **パスワード =** *パスワード*  
クライアントのデバッグ セッションに接続するには、指定したパスワードを入力する必要があります。 *パスワード*12 文字の長さまでの任意の英数字文字列を指定できます。

**警告**  パスワードが暗号化されていないため、少量の保護を提供パスワード TCP、NPIPE、または COM のプロトコルを使用します。 パスワードを使用して、SSL または SPIPE プロトコルで、暗号化されます。 セキュリティで保護されたリモート セッションを確立する場合は、SSL または SPIPE プロトコルを使用する必要があります。

 

<span id="________ipversion_6"></span><span id="________IPVERSION_6"></span> **ipversion=6**  
(デバッグ ツールの Windows 6.6.07 以前のみ)強制的に IP version 6 を使用するデバッガー バージョン 4 TCP を使用して、インターネットに接続するのではなく。 Windows Vista およびそれ以降のバージョンでは、デバッガーは、IP バージョン 6、このオプションが不要なために既定値の自動を試みます。

<span id="-noio"></span><span id="-NOIO"></span>**-noio**  
デバッグ サーバーが作成された場合、 **- noio**オプション、いない入力または出力は、サーバー自体で実行できます。 デバッガーはデバッグのクライアントからの入力のみを受け入れます (さらに任意の最初のコマンドやコマンドのスクリプトで指定された、 **-c**コマンド ライン オプション)。 すべての出力は、デバッグのクライアントに転送されます。 **- Noio**オプションは、KD、CDB、NTSD と使用のみ。 サーバーの NTSD を使用する場合コンソール ウィンドウは作成されませんまったくです。

<span id="________IcfEnable"></span><span id="________icfenable"></span><span id="________ICFENABLE"></span> **IcfEnable**  
原因のデバッガーは、インターネット接続ファイアウォールは、アクティブなときに、TCP または名前付きパイプ通信のために必要なポートの接続を有効にします。 既定では、インターネット接続ファイアウォールには、これらのプロトコルで使用されるポートが無効にします。 ときに**IcfEnable**使用は、TCP 接続の場合、デバッガーが Windows によって指定されたポートを開く、*ソケット*パラメーター。 ときに**IcfEnable**される名前付きパイプ接続の場合、デバッガーが Windows 名前付きパイプ (ポート 139 と 445) を使用するポートを開きます。 デバッガーでは、接続が終了した後、これらのポートは終了しません。

<span id="Options_______"></span><span id="options_______"></span><span id="OPTIONS_______"></span>*オプション*   
ここに、追加のコマンド ライン パラメーターを配置することができます。 参照してください[コマンド ライン オプション](command-line-options.md)完全な一覧についてはします。

使用することができます、 [ **.server** ](-server--create-debugging-server-.md)別のプロトコル オプションを使用して複数のサーバーを起動するコマンド。 これにより、さまざまな種類のセッションに参加するクライアントをデバッグできます。


## <a name="see-also"></a>参照

[リモート デバッグ セッションを制御します。](controlling-a-remote-debugging-session.md)

[.endsrv (エンド サーバーのデバッグ)](-endsrv--end-debugging-server-.md)
 

------





