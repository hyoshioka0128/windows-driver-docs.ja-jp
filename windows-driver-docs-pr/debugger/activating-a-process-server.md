---
title: プロセス サーバーをアクティブ化します。
description: プロセス サーバーをアクティブ化するには、(管理者として実行)、管理者特権でコマンド プロンプト ウィンドウを開き dbgsrv コマンドを入力します。
ms.assetid: 566a4f64-8a14-469b-b50c-20e3c00aa2f8
keywords:
- デバッグ プロセス サーバーの Windows アクティブ化します。
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Activating a Process Server
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ecdda091634cab38db94f82ebcf2faf702898e45
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549132"
---
# <a name="activating-a-process-server"></a>プロセス サーバーをアクティブ化します。


ツールを Windows のデバッグに含まれているプロセス サーバーは、DbgSrv (dbgsrv.exe) と呼ばれます。 プロセス サーバーをアクティブ化する (管理者として実行)、管理者特権でコマンド プロンプト ウィンドウを開くし、入力、 **dbgsrv**コマンド。

**注**  特権を昇格することがなく、プロセス サーバーをアクティブ化することができ、クライアントのデバッグはサーバーに接続することになります。 ただし、クライアントを昇格した特権でアクティブ化がない限り、プロセス サーバーを検出することはできません。 デバッグ サーバーを検出する方法については、次を参照してください。[プロセス サーバーを探して](searching-for-process-servers.md)します。

 

DbgSrv がいくつかのトランスポート プロトコルをサポートしています。 名前付きパイプ (NPIPE)、TCP、COM ポート、セキュリティで保護されたパイプ (SPIPE) および secure socket layer (SSL)。

```console
dbgsrv -t npipe:pipe=PipeName[,hidden][,password=Password][,IcfEnable] [[-sifeo Executable] -c[s] AppCmdLine] [-x | -pc] 

dbgsrv -t tcp:port=Socket[,hidden][,password=Password][,ipversion=6][,IcfEnable] [[-sifeo Executable] -c[s] AppCmdLine] [-x | -pc] 

dbgsrv -t tcp:port=Socket,clicon=Client[,password=Password][,ipversion=6] [[-sifeo Executable] -c[s] AppCmdLine] [-x | -pc] 

dbgsrv -t com:port=COMPort,baud=BaudRate,channel=COMChannel[,hidden][,password=Password] [[-sifeo Executable] -c[s] AppCmdLine] [-x | -pc] 

dbgsrv -t spipe:proto=Protocol,{certuser=Cert|machuser=Cert},pipe=PipeName[,hidden][,password=Password] [[-sifeo Executable] -c[s] AppCmdLine] [-x | -pc] 

dbgsrv -t ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket[,hidden][,password=Password] [[-sifeo Executable] -c[s] AppCmdLine] [-x | -pc] 

dbgsrv -t ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket,clicon=Client[,password=Password] [[-sifeo Executable] -c[s] AppCmdLine] [-x | -pc] 
```

## <span id="ddk_activating_a_process_server_dbg"></span><span id="DDK_ACTIVATING_A_PROCESS_SERVER_DBG"></span>


前述のコマンドでパラメーターには、次の値があります。

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span> **pipe=** *PipeName*  
NPIPE または SPIPE プロトコルを使用するとと、 *PipeName*はパイプの名前として使用する文字列です。 各パイプ名は一意のプロセス サーバーを識別する必要があります。 パイプ名を再利用しようとした場合、エラー メッセージが表示されます。 *PipeName*スペースや引用符を含めることはできません。 *PipeName*数値を含めることができます**printf**-など、書式コードのスタイル設定 **%x**または **%d**します。 プロセス サーバーは、プロセス ID の DbgSrv でこれが置換されます。 このような 2 つ目のコードは、スレッド ID の DbgSrv に置き換えられます。

**注**  ファイルとプリンターの共有、プロセス サーバーを実行しているコンピューターを有効にする必要があります。 コントロール パネルに移動します。**ネットワークとインターネット&gt;ネットワークと共有センター&gt;共有の詳細設定**します。 選択**ファイルとプリンターの共有を有効に**します。

 

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span> **ポート =** *ソケット*  
TCP または SSL プロトコルを使用するとと、*ソケット*ソケットのポート番号です。

コロンで区切ってポートの範囲を指定することもできます。 DbgSrv では、無料かどうかをこの範囲内の各ポートを確認します。 空きポートが見つかるし、エラーが発生しない、プロセス サーバーが作成されます。 スマート クライアントは、サーバーに接続するために使用される実際のポートを指定する必要があります。 を実際のポートを判断するで説明する方法のいずれかの操作を使用して[**プロセス サーバーを検索**](searching-for-process-servers.md); このプロセス サーバーが表示されたら、ポートの後、コロンで区切られた 2 つの数値。 最初の数値が使用されますが、実際のポートになります2 つ目は無視できます。 たとえば、として、ポートが指定されて**ポート = 51:60**、ポート 53 が実際に使用されるとは、検索結果が表示されます"ポート 53:60 ="。 (使用する場合、 **clicon**スマート クライアント リバース接続を確立するパラメーターは、プロセス サーバーが実際に使用されるポートを指定する必要がありますに、この方法でのポートの範囲を指定できます)。

<span id="________clicon_________Client"></span><span id="________clicon_________client"></span><span id="________CLICON_________CLIENT"></span> **clicon =** *クライアント*  
TCP または SSL プロトコルを使用する場合、 **clicon**パラメーターが指定されて、*接続を取り消す*が開きます。 つまり、プロセス サーバーがクライアントの連絡先を開始できるようにすることではなく、スマート クライアントに接続しようとするされます。 通常の方向での接続を妨げているファイアウォールがある場合に役立ちます。 ことができます。 *クライアント*ネットワーク名またはをスマート クライアントが存在するか、作成は、コンピューターの IP アドレスを指定します。 2 つの初期の円記号 (\\ \)は省略可能です。

1 つの特定のクライアントをプロセス サーバーを検索するためは、このメソッドを使用する場合、サーバーに複数のクライアントを接続できません。 接続が拒否されるかが壊れている場合は、プロセス サーバーを再起動する必要があります。 別のユーザーが、接続が逆のプロセス サーバーは表示されない、 **-QR**すべてのアクティブなサーバーを表示するコマンド ライン オプション。

**注**  とき**clicon**が使用することをお勧めですが、通常の順序 (クライアントの前にサーバー) は許可されても、プロセス サーバーが作成される前に、スマート クライアントを開始します。

 

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
プロセス サーバーが別のユーザーが表示されることを防止、 **-QR**コマンド ライン オプションをすべてのアクティブなサーバーを表示します。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span> **パスワード =** *パスワード*  
プロセス サーバーに接続するには、指定したパスワードを入力するスマート クライアントが必要です。 *パスワード*12 文字の長さまでの任意の英数字文字列を指定できます。

**警告**  パスワードが暗号化されていないため、少量の保護を提供パスワード TCP、NPIPE、または COM のプロトコルを使用します。 パスワードを使用して、SSL または SPIPE プロトコルで、暗号化されます。 セキュリティで保護されたリモート セッションを確立する場合は、SSL または SPIPE プロトコルを使用する必要があります。

 

<span id="________ipversion_6"></span><span id="________IPVERSION_6"></span> **ipversion=6**  
(デバッグ ツールの Windows 6.6.07 以前のみ)強制的に IP version 6 を使用するデバッガー バージョン 4 TCP を使用して、インターネットに接続するのではなく。 Windows Vista およびそれ以降のバージョンでは、デバッガーは、IP バージョン 6、このオプションが不要なために既定値の自動を試みます。

<span id="________IcfEnable"></span><span id="________icfenable"></span><span id="________ICFENABLE"></span> **IcfEnable**  
原因のデバッガーは、インターネット接続ファイアウォールは、アクティブなときに、TCP または名前付きパイプ通信のために必要なポートの接続を有効にします。 既定では、インターネット接続ファイアウォールには、これらのプロトコルで使用されるポートが無効にします。 ときに**IcfEnable**使用は、TCP 接続の場合、デバッガーが Windows によって指定されたポートを開く、*ソケット*パラメーター。 ときに**IcfEnable**される名前付きパイプ接続の場合、デバッガーが Windows 名前付きパイプ (ポート 139 と 445) を使用するポートを開きます。 デバッガーでは、接続が終了した後、これらのポートは終了しません。

<span id="-sifeo__________Executable"></span><span id="-sifeo__________executable"></span><span id="-SIFEO__________EXECUTABLE"></span>**-sifeo** *実行可能ファイル*  
指定したイメージのイメージ ファイルの実行オプション (IFEO) 値を中断します。 *実行可能*ファイル名拡張子を含む、実行可能イメージのファイル名を含める必要があります。 **- Sifeo**オプションにより、によって作成されたイメージの IFEO デバッガーとして設定する DbgSrv、 **-c** IFEO 設定が原因の再帰呼び出しを発生させることがなく、オプションです。 場合にのみ、このオプションを使用できる **-c**使用されます。

<span id="________-c"></span><span id="________-C"></span> **-c**  
新しいプロセスを作成する DbgSrv をによりします。 これを使用して、デバッグするプロセスを作成することができます。 作成時、このプロセスはデバッグしない点を除き、デバッガーから新しいプロセスを生成することに似ています。 このプロセスをデバッグするその PID を判断し、使用、 **-p**オプション、このプロセスをデバッグするスマート クライアントを開始するときにします。

<span id="s"></span><span id="S"></span>**s**  
新しく作成されたプロセスをすぐに中断するさせます。 このオプションを使用している場合をお勧め CDB はスマート クライアントとして使用することと、スマート クライアントを起動する、 **-pb**コマンド ライン オプションを組み合わせて **-p PID**します。 含める場合は、 **-pb**デバッガーをアタッチすると、コマンドライン、プロセスのオプションは再開されますそれ以外の場合にプロセスを再開することができます、 [  **~ \*m。**](-m--resume-thread-.md)コマンド。

<span id="AppCmdLine"></span><span id="appcmdline"></span><span id="APPCMDLINE"></span>*AppCmdLine*  
作成するプロセスの完全なコマンドラインを指定します。 *AppCmdLine* Unicode または ASCII のいずれかの文字列を使用でき、印刷可能な文字を含めることができます。 後に表示されるすべてのテキスト、 **-c\[s\]** パラメーターは、文字列が形成される*AppCmdLine*します。

<span id="-x"></span><span id="-X"></span>**-x**  
無視するコマンドラインの残りの部分をによりします。 このオプションは、アプリケーションをコマンドラインに不要なテキストを追加することがありますから DbgSrv を起動する場合に便利です。

<span id="________-pc"></span><span id="________-PC"></span> **-pc**  
無視するコマンドラインの残りの部分をによりします。 このオプションは、アプリケーションをコマンドラインに不要なテキストを追加することがありますから DbgSrv を起動する場合に便利です。 構文エラーが発生**pc** DbgSrv コマンドラインで最終的な要素です。 この制限を除けば**pc**と同じです **-x**。

1 台のコンピューターで任意の数のプロセス サーバーを開始できます。 ただし、一般に必要ない、(別のデバッグ セッションで各進行中)、スマート クライアントの任意の数が 1 つのプロセス サーバーに使用されることができます。

 

 





