---
title: repeater のアクティブ化
description: Repeater 接続を有効にするには、通常は最初にサーバーを起動し、repeater を開始し、クライアントを起動します。Repeater を開始することも 1 つ目とし、サーバー。
ms.assetid: a2409b3d-48eb-46eb-8a53-7c4d505bb6ea
keywords:
- デバッグ Repeater Windows アクティブ化します。
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Activating a Repeater
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8472755660c478cd454d2ef644dd17ec1015226c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354004"
---
# <a name="activating-a-repeater"></a>repeater のアクティブ化


Repeater 接続を有効にするには、通常は最初にサーバーを起動し、repeater を開始し、クライアントを起動します。

Repeater を開始することも 1 つ目とし、サーバー。 使用している場合を除き、 **clicon**パラメーターを逆方向の接続、クライアントを確立するために常に開始する必要が最後です。

## <a name="span-idsteponestartingtheserverspanspan-idsteponestartingtheserverspanstep-one-starting-the-server"></a><span id="step_one__starting_the_server"></span><span id="STEP_ONE__STARTING_THE_SERVER"></span>手順 1:サーバーを起動


サーバー デバッグ サーバー、プロセス サーバー、または KD 接続のサーバーを使用できます。 開始するこれは、通常どおりクライアントではなく、repeater に接続するトランスポート プロトコルの設定が使用する点が異なります。 詳細については、次を参照してください[**デバッグ サーバー アクティブ化する**](activating-a-debugging-server.md)、 [**プロセス サーバーをアクティブ化する**](activating-a-process-server.md)、または[  **。KD 接続のサーバーをアクティブ化する**](activating-a-kd-connection-server.md)します。

サーバーを作成するときにパスワードを使用する場合は、クライアントの接続がリピータが作成されたときではなく、このパスワードが必要なります。

使用する場合、**隠し**パラメーター、サーバーは通常どおりに表示されません。 Repeater 自体は常に表示されません。

## <a name="span-idsteptwostartingtherepeaterspanspan-idsteptwostartingtherepeaterspanstep-two-starting-the-repeater"></a><span id="step_two__starting_the_repeater"></span><span id="STEP_TWO__STARTING_THE_REPEATER"></span>手順 2:リピータの開始


Windows のツールのデバッグに含まれている repeater は DbEngPrx (dbengprx.exe) と呼ばれます。

DbEngPrx、次のトランスポート プロトコルを理解する: 名前付きパイプ (NPIPE)、TCP、および COM ポート。

場合は、クライアントとサーバーは、secure sockets layer (SSL) プロトコルを使用して、repeater の TCP プロトコルを使用する必要があります。 場合は、クライアントとサーバーは、セキュリティで保護されたパイプ (SPIPE) プロトコルを使用して、repeater の NPIPE プロトコルを使用する必要があります。 Repeater を渡す受信 - すべてのデータの解釈、暗号化、したりしないすべての情報を復号化します。 すべての暗号化と復号化は、クライアントとサーバーで実行されます。

DbEnPrx コマンドラインの構文は次のとおりです。

## <span id="ddk_activating_a_repeater_dbg"></span><span id="DDK_ACTIVATING_A_REPEATER_DBG"></span>


**dbengprx \[-p\] -c** *ClientTransport* **-s** *ServerTransport*

前述のコマンドでパラメーターには、次の値があります。

<span id="________-p"></span><span id="________-P"></span> **-p**  
既存のすべての接続を削除した後も引き続き DbEngPrx をによりします。

<span id="ClientTransport"></span><span id="clienttransport"></span><span id="CLIENTTRANSPORT"></span>*ClientTransport*  
サーバーへの接続に使用するプロトコル設定を指定します。 プロトコルは、サーバーの作成時に使用と一致する必要があります。 プロトコル構文は次のとおりです。

```dbgcmd
npipe:server=Server,pipe=PipeName[,password=Password] 
tcp:server=Server,port=Socket[,password=Password][,ipversion=6] 
tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6] 
com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password] 
```

プロトコル パラメーターでは、次の意味があります。

<span id="Server"></span><span id="server"></span><span id="SERVER"></span>*サーバー*  
これは、ネットワーク名またはサーバーが作成されたコンピューターの IP アドレス。 2 つの初期の円記号 (\\ \)は省略可能です。

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span> **pipe=** *PipeName*  
NPIPE または SPIPE プロトコルを使用すると場合、 *PipeName*サーバーの作成時に、パイプに指定された名前を指定します。

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span> **ポート =** *ソケット*  
TCP または SSL プロトコルを使用すると場合、*ソケット*は、サーバーが作成されたときに使用された同じソケットのポート番号です。

<span id="clicon"></span><span id="CLICON"></span>**clicon**  
サーバーが逆方向の接続を介して repeater に接続しようとするを指定します。 *ClientTransport*を使用する必要があります**clicon**サーバーが使用する場合にのみ**clicon**します。 ほとんどの場合は逆方向の接続を使用すると、サーバーの前に、repeater が開始されます。

<span id="port_________COMPort"></span><span id="port_________comport"></span><span id="PORT_________COMPORT"></span>**port=** *COMPort*  
COM のプロトコルを使用すると場合、 *com ポート*使用する COM ポートを指定します。 プレフィックス"COM"は省略可能 - たとえば、"com2"および「2」の両方が許容されます。

<span id="baud_________BaudRate"></span><span id="baud_________baudrate"></span><span id="BAUD_________BAUDRATE"></span>**ボー =** *BaudRate*  
COM のプロトコルを使用すると場合、 *BaudRate*サーバーの作成時に選択したボー レートが一致する必要があります。

<span id="channel_________COMChannel"></span><span id="channel_________comchannel"></span><span id="CHANNEL_________COMCHANNEL"></span>**channel=** *COMChannel*  
COM のプロトコルを使用すると場合、 *COMChannel*サーバーの作成時に選択したチャンネル番号が一致する必要があります。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span> **パスワード =** *パスワード*  
パスワードが、サーバーが作成されたときに使用された場合*パスワード*デバッグのクライアントを作成するために指定する必要があります。 元のパスワードに一致する必要があります。 パスワードは大文字小文字が区別されます。 エラー メッセージが「エラー 0x80004005」を指定、間違ったパスワードが指定されている場合

<span id="________ipversion_6"></span><span id="________IPVERSION_6"></span> **ipversion=6**  
(デバッグ ツールの Windows 6.6.07 以前のみ)強制的に IP version 6 を使用するデバッガー バージョン 4 TCP を使用して、インターネットに接続するのではなく。 Windows Vista およびそれ以降のバージョンでは、デバッガーは、IP バージョン 6、このオプションが不要なために既定値の自動を試みます。

<span id="ServerTransport"></span><span id="servertransport"></span><span id="SERVERTRANSPORT"></span>サーバトランスポート  
クライアントは、repeater に接続するときに使用されるプロトコルの設定を指定します。 可能なプロトコルの構文は次のとおりです。

```dbgcmd
npipe:pipe=PipeName[,hidden][,password=Password][,IcfEnable] 
tcp:port=Socket[,hidden][,password=Password][,IcfEnable] 
tcp:port=Socket,clicon=Client[,password=Password] 
com:port=COMPort,baud=BaudRate,channel=COMChannel[,hidden][,password=Password] 
```

プロトコル パラメーターでは、次の意味があります。

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span> **pipe=** *PipeName*  
NPIPE または SPIPE プロトコルを使用するとと、 *PipeName*はパイプの名前として使用する文字列です。 各パイプ名は一意 repeater を識別する必要があります。 パイプ名を再利用しようとした場合、エラー メッセージが表示されます。 *PipeName*スペースや引用符を含めることはできません。 *PipeName*数値を含めることができます**printf**-など、書式コードのスタイル設定 **%x**または **%d**します。 Repeater は、プロセス ID の DbEngPrx でこれが置換されます。 このような 2 つ目のコードは、スレッド ID の DbEngPrx に置き換えられます。

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span> **ポート =** *ソケット*  
TCP または SSL プロトコルを使用するとと、*ソケット*ソケットのポート番号です。

コロンで区切ってポートの範囲を指定することもできます。 DbEngPrx では、無料かどうかをこの範囲内の各ポートを確認します。 空きポートが見つかるし、エラーが発生しない、リピータが作成されます。 クライアントは、実際に、repeater に接続するために使用されているポートを指定する必要があります。 実際のポートを確認するのには、repeater; を検索します。この repeater が表示されたら、ポートは後ろにコロンで区切られた 2 つの数値。 最初の数値が使用されますが、実際のポートになります2 つ目は無視できます。 たとえば、として、ポートが指定されて**ポート = 51:60**、ポート 53 が実際に使用されるとは、検索結果が表示されます"ポート 53:60 ="。 (使用する場合、 **clicon**クライアント リバース接続を確立するパラメーターは、リピータが実際に使用されるポートを指定する必要があります中に、この方法でのポートの範囲を指定できます)。

<span id="clicon_Client"></span><span id="clicon_client"></span><span id="CLICON_CLIENT"></span>**clicon =**<em>クライアント</em>  
TCP または SSL プロトコルを使用する場合、 **clicon**パラメーターが指定されて、*接続を取り消す*が開きます。 つまり、repeater は連絡先を開始するクライアントではなく、クライアントに接続する試みます。 通常の方向での接続を妨げているファイアウォールがある場合に役立ちます。 ことができます。 *クライアント*ネットワーク名またはをクライアントが存在するか、作成は、コンピューターの IP アドレスを指定します。 2 つの初期の円記号 (\\ \)は省略可能です。

リピータは 1 つの特定のクライアントを検索するためこのメソッドを使用する場合、repeater に複数のクライアントを接続することはできません。 接続が拒否されるかが壊れている場合は、repeater を再起動する必要があります。

ときに**clicon**が使用することをお勧めですが、通常の順序 (クライアントの前に repeater) は許可されても、リピータが作成される前に、クライアントを開始します。

<span id="port_________COMPort"></span><span id="port_________comport"></span><span id="PORT_________COMPORT"></span>**port=** *COMPort*  
COM のプロトコルを使用するとと、 *com ポート*使用する COM ポートを指定します。 プレフィックス"COM"は省略可能 - たとえば、"com2"および「2」の両方が許容されます。 内の同じ COM ポートを使用することはできません、 *ClientTransport*と*サーバトランスポート*します。

<span id="baud_________BaudRate"></span><span id="baud_________baudrate"></span><span id="BAUD_________BAUDRATE"></span>**ボー =** *BaudRate*  
COM のプロトコルを使用するとと、 *BaudRate*接続を実行するボー レートを指定します。 ハードウェアでサポートされている任意のボー レートが許可されます。 両方の COM のプロトコルを使用している場合、 *ClientTransport*と*サーバトランスポート*異なるボー レートを指定することがありますが、クライアントとサーバーがどの程度の速度で制限を低速のレートが自然になります互いと通信できます。

<span id="channel_________COMChannel"></span><span id="channel_________comchannel"></span><span id="CHANNEL_________COMCHANNEL"></span>**channel=** *COMChannel*  
COM のプロトコルを使用すると場合、 *COMChannel*クライアントとの通信に使用する COM チャネルを指定します。 0 ~ 254 の包括的な範囲の任意の値を指定できます。 別のチャンネル番号を使用して複数の接続の 1 つの COM ポートを使用することができます。 (これは、COM ポートを使用して、デバッグ ケーブル異なります--ような状況では、COM ポート内でチャネルを使うことはできません)。

<span id="hidden"></span><span id="HIDDEN"></span>**非表示**  
サーバー、別のデバッガーは、すべてのアクティブなサーバーを表示するときに表示されません。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span> **パスワード =** *パスワード*  
クライアントのデバッグ セッションに接続するには、指定したパスワードを入力する必要があります。 *パスワード*任意の英数字の文字列を指定できます。

<span id="IcfEnable"></span><span id="icfenable"></span><span id="ICFENABLE"></span>**IcfEnable**  
原因のデバッガーは、インターネット接続ファイアウォールは、アクティブなときに、TCP または名前付きパイプ通信のために必要なポートの接続を有効にします。 既定では、インターネット接続ファイアウォールには、これらのプロトコルで使用されるポートが無効にします。 ときに**IcfEnable**使用は、TCP 接続の場合、デバッガーが Windows によって指定されたポートを開く、*ソケット*パラメーター。 ときに**IcfEnable**される名前付きパイプ接続の場合、デバッガーが Windows 名前付きパイプ (ポート 139 と 445) を使用するポートを開きます。 デバッガーでは、接続が終了した後、これらのポートは終了しません。

### <a name="span-idstepthreestartingtheclientspanspan-idstepthreestartingtheclientspanstep-three-starting-the-client"></a><span id="step_three__starting_the_client"></span><span id="STEP_THREE__STARTING_THE_CLIENT"></span>手順 3:クライアントを起動

クライアントは、デバッグのクライアントまたはスマート クライアント--方は、サーバーの種類に対応します。 詳細については、次を参照してください[**デバッグ クライアントをアクティブ化する**](activating-a-debugging-client.md)、 [**スマート クライアントのアクティブ化**](activating-a-smart-client.md)、または[  **。スマート クライアント (カーネル モード) をアクティブ化する**](activating-a-smart-client--kernel-mode-.md)します。

サーバーは、(たとえば、間違ったパスワードを指定する場合) の接続を拒否する場合、repeater とクライアントの両方がシャット ダウンします。 サーバーとの接続を再確立することの両方を再起動する必要があります。

 

 





