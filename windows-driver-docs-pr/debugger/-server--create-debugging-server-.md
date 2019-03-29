---
title: .server (デバッグ サーバーの作成)
description: .Server コマンドでは、デバッグ サーバーは、現在のデバッグ セッションをリモート接続することを開始します。
ms.assetid: 39979a53-d6e7-4660-8884-3044da0b60de
keywords:
- デバッグ サーバー (.server) コマンドを作成します。
- リモート デバッグ、デバッガーはデバッグ サーバーの作成 (.server) コマンド
- .server (デバッグ サーバーを作成する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .server (Create Debugging Server)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bbdc4d1fdf3d16e42e98cb61a0d036ff67d6a5b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579671"
---
# <a name="server-create-debugging-server"></a>.server (デバッグ サーバーの作成)


**.Server**コマンドは、現在のデバッグ セッションへのリモート接続を許可する、デバッグのサーバーを起動します。

```dbgcmd
.server npipe:pipe=PipeName[,hidden][,password=Password][,IcfEnable] 
.server tcp:port=Socket[,hidden][,password=Password][,ipversion=6][,IcfEnable] 
.server tcp:port=Socket,clicon=Client[,password=Password][,ipversion=6] 
.server com:port=COMPort,baud=BaudRate,channel=COMChannel[,hidden][,password=Password] 
.server spipe:proto=Protocol,{certuser=Cert|machuser=Cert},pipe=PipeName[,hidden][,password=Password] 
.server ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket[,hidden][,password=Password] 
.server ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket,clicon=Client[,password=Password] 
```

## <a name="span-idddkmetacreatedebuggingserverdbgspanspan-idddkmetacreatedebuggingserverdbgspanparameters"></a><span id="ddk_meta_create_debugging_server_dbg"></span><span id="DDK_META_CREATE_DEBUGGING_SERVER_DBG"></span>パラメーター


<span id="_______PipeName______"></span><span id="_______pipename______"></span><span id="_______PIPENAME______"></span> *PipeName*   
NPIPE または SPIPE プロトコルを使用するとと、 *PipeName*はパイプの名前として使用する文字列です。 各パイプ名は一意なデバッグ サーバーを識別する必要があります。 パイプ名を再利用しようとした場合、エラー メッセージが表示されます。 *PipeName*スペースや引用符を含めることはできません。 *PipeName*数値を含めることができます**printf**-%x や %d などの形式のコードのスタイルを設定します。 デバッガーは、デバッガーのプロセス ID でこれが置換されます。 このような 2 つ目のコードは、デバッガーのスレッド ID に置き換えられます。

<span id="_______Socket______"></span><span id="_______socket______"></span><span id="_______SOCKET______"></span> *ソケット*   
TCP または SSL プロトコルを使用するとと、*ソケット*ソケットのポート番号です。

コロンで区切ってポートの範囲を指定することもできます。 デバッガーでは、無料かどうかをこの範囲内の各ポートを確認します。 空きポートが見つかるし、エラーが発生しない、デバッグ サーバーが作成されます。 デバッグ クライアントは、サーバーに接続するために使用される実際のポートを指定する必要があります。 を実際のポートを判断するで説明する方法のいずれかの操作を使用して[**デバッグ サーバーの検索**](searching-for-debugging-servers.md); このデバッグ サーバーが表示されたら、ポートの後、コロンで区切られた 2 つの数値。 最初の数値が使用されますが、実際のポートになります2 つ目は無視できます。 たとえば、次のポートとしてポートが指定されました = 51:60、ポート 53 が実際に使用されるとは、検索結果が表示されます"ポート 53:60 ="。 (使用する場合、 **clicon**デバッグ クライアント リバース接続を確立するパラメーターは、サーバーが実際に使用されるポートを指定する必要がありますに、この方法でのポートの範囲を指定できます)。

<span id="clicon_Client"></span><span id="clicon_client"></span><span id="CLICON_CLIENT"></span>**clicon =**<em>クライアント</em>  
TCP または SSL プロトコルを使用する場合、 **clicon**パラメーターが指定されて、*接続を取り消す*が開きます。 これは、デバッグ サーバーがクライアントの連絡先を開始できるようにすることではなく、デバッグ、クライアントに接続しようとする、ことを意味します。 通常の方向での接続を妨げているファイアウォールがある場合に役立ちます。 ことができます。 *クライアント*をデバッグのクライアントが存在するか、作成は、マシンのネットワーク名を指定します。 2 つの初期の円記号 (\\ \)は省略可能です。

ときに**clicon**が使用することをお勧めですが、通常の順序 (クライアントの前にサーバー) は許可されても、デバッグのサーバーを作成する前にデバッグのクライアントを開始します。 逆接続サーバーは、別のデバッガーは、すべてのアクティブなサーバーを表示するときに表示されません。

<span id="_______COMPort______"></span><span id="_______comport______"></span><span id="_______COMPORT______"></span> *COMPort*   
COM のプロトコルを使用するとと、 *com ポート*使用する COM ポートを指定します。 COM のプレフィックスは省略可能です (たとえば、"com2"および「2」の両方が許容される)。

<span id="_______BaudRate______"></span><span id="_______baudrate______"></span><span id="_______BAUDRATE______"></span> *BaudRate*   
COM のプロトコルを使用するとと、 *BaudRate*接続を実行するボー レートを指定します。 ハードウェアでサポートされている任意のボー レートが許可されます。

<span id="_______COMChannel______"></span><span id="_______comchannel______"></span><span id="_______COMCHANNEL______"></span> *COMChannel*   
COM のプロトコルを使用すると場合、 *COMChannel*デバッグ クライアントとの通信に使用する COM チャネルを指定します。 0 ~ 254 の包括的な範囲の任意の値を指定できます。

<span id="_______Protocol______"></span><span id="_______protocol______"></span><span id="_______PROTOCOL______"></span> *プロトコル*   
SSL または SPIPE プロトコルを使用すると場合、*プロトコル*Secure Channel (S チャネル) プロトコルを指定します。 文字列 tls1、pct1、ssl2、または ssl3 のいずれかにできます。

<span id="_______Cert______"></span><span id="_______cert______"></span><span id="_______CERT______"></span> *証明書*   
SSL または SPIPE プロトコルを使用すると場合、 *Cert*証明書を指定します。 証明書の名前または証明書の拇印 (証明書のスナップインで指定された 16 進数の数字の文字列) を指定できます。 場合、構文**certuser =**<em>Cert</em>が使用すると、デバッガーがシステム ストア (既定のストア) に証明書を検索します。 場合、構文**machuser =**<em>証明書</em>が使用すると、デバッガーがコンピューターのストアに証明書を検索します。 指定された証明書は、サーバー認証をサポートする必要があります。

<span id="_______hidden______"></span><span id="_______HIDDEN______"></span> **hidden**   
サーバー、別のデバッガーは、すべてのアクティブなサーバーを表示するときに表示されません。

<span id="password_Password"></span><span id="password_password"></span><span id="PASSWORD_PASSWORD"></span>**パスワード =**<em>パスワード</em>  
デバッグのクライアントのデバッグ セッションに接続するには、指定したパスワードを入力する必要があります。 *パスワード*12 文字の長さまでの任意の英数字文字列を指定できます。

<span id="_______ipversion_6______"></span><span id="_______IPVERSION_6______"></span> **ipversion=6**   
(デバッグ ツールの Windows 6.6.07 以前のみ)強制的に IP version 6 を使用するデバッガー バージョン 4 TCP を使用して、インターネットに接続するのではなく。 Windows Vista およびそれ以降のバージョンでは、デバッガーは、IP バージョン 6、このオプションが不要なために既定値の自動を試みます。

<span id="_______IcfEnable______"></span><span id="_______icfenable______"></span><span id="_______ICFENABLE______"></span> **IcfEnable**   
原因のデバッガーは、インターネット接続ファイアウォールは、アクティブなときに、TCP または名前付きパイプ通信のために必要なポートの接続を有効にします。 既定では、インターネット接続ファイアウォールには、これらのプロトコルで使用されるポートが無効にします。 ときに**IcfEnable**使用は、TCP 接続の場合、デバッガーが Windows ソケット パラメーターで指定されたポートを開きます。 ときに**IcfEnable**される名前付きパイプ接続の場合、デバッガーが Windows 名前付きパイプ (ポート 139 と 445) を使用するポートを開きます。 デバッガーでは、接続が終了した後、これらのポートは終了しません。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

デバッグ サーバーを起動する方法の完全な詳細については、次を参照してください。 [**デバッグ サーバー アクティブ化する**](activating-a-debugging-server.md)します。 例については、次を参照してください。[クライアントとサーバーの例](client-and-server-examples.md)します。

<a name="remarks"></a>コメント
-------

このコマンドは、デバッグのサーバーに現在のデバッガーをオンにします。 一方、デバッガーが既に実行されていた後サーバーを起動することができます - サーバー[コマンド ライン オプション](command-line-options.md)デバッガーの起動時にのみ実行できます。

これにより、現在のデバッグ セッションに接続するクライアントはデバッグします。 これは、さまざまな種類のセッションに参加するクライアントをデバッグできるように、さまざまなオプションを使用して複数のサーバーを開始することに注意してください。

 

 





