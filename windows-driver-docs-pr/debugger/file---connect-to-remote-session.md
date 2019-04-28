---
title: ファイルがリモート セッションに接続します。
description: ファイルがリモート セッションに接続します。
ms.assetid: 82c4900f-846b-41fb-afdc-3c73b524af9c
keywords:
- ファイルがリモート セッションに接続します。
- リモート デバッガーが、ファイルがリモート セッションに接続を通じてデバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b2022f1062a3ea2663ff234e5c8d5c8a841cb4f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361496"
---
# <a name="file--connect-to-remote-session"></a>File | Connect to Remote Session (ファイル | リモート セッションに接続)


## <span id="ddk_file_connect_to_remote_session_dbg"></span><span id="DDK_FILE_CONNECT_TO_REMOTE_SESSION_DBG"></span>


をクリックして**リモート セッションに接続する**上、**ファイル**WinDbg を実行するには、クライアントをデバッグし、アクティブなデバッグ サーバーに接続するためのメニュー。

このコマンドは、ctrl キーを押しながら R キーを押すと同じです。 このコマンドは、WinDbg が休止モードである場合にのみ使用できます。

このコマンドは、プロセス サーバーまたは KD 接続サーバーへの接続を使用することはできません。そのために、使用[ファイル |リモートのスタブに接続する](file---connect-to-remote-stub.md)代わりにします。

### <a name="span-idconnecttoremotedebuggersessiondialogboxspanspan-idconnecttoremotedebuggersessiondialogboxspanconnect-to-remote-debugger-session-dialog-box"></a><span id="connect_to_remote_debugger_session_dialog_box"></span><span id="CONNECT_TO_REMOTE_DEBUGGER_SESSION_DIALOG_BOX"></span>リモート デバッガー セッション ダイアログ ボックスへの接続します。

クリックすると**リモート セッションに接続する**、**リモート デバッガー セッションへの接続** ダイアログ ボックスが表示されます。 リモート接続パラメーターを入力するか、デバッグ サーバーの一覧を参照するこのダイアログ ボックスを使用することができます。

リモート接続パラメーターを手動で指定するには、次の文字列のいずれかを入力、**接続文字列**ボックス。

```text
npipe:server=Server,pipe=PipeName[,password=Password] 

tcp:server=Server,port=Socket[,password=Password][,ipversion=6]

tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6]

com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password] 

spipe:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,pipe=PipeName[,password=Password] 

ssl:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,port=Socket[,password=Password]

ssl:proto=Protocol,{certuser=Cert|machuser=Cert},clicon=Server,port=Socket[,password=Password]
```

これらのオプションでさまざまなパラメーターがある値は、次のとおり。

<span id="Server"></span><span id="server"></span><span id="SERVER"></span>*サーバー*  
デバッグ サーバーが作成されたコンピューターのネットワーク名。 この名前の円記号は付けません (**\\\\**)。

<span id="PipeName"></span><span id="pipename"></span><span id="PIPENAME"></span>*PipeName*  
NPIPE または SPIPE プロトコルを使用する場合*PipeName*サーバーの作成時に、パイプに指定された名前を指定します。

<span id="Socket"></span><span id="socket"></span><span id="SOCKET"></span>*ソケット*  
TCP または SSL プロトコルを使用する場合*ソケット*は、サーバーが作成されたときに使用された同じソケットのポート番号です。

<span id="COMPort"></span><span id="comport"></span><span id="COMPORT"></span>*COMPort*  
COM のプロトコルを使用する場合*com ポート*を使用する COM ポートを指定します。 "COM"プレフィックスは省略可能です (たとえば、"com2"および「2」の両方が正しい)。

<span id="BaudRate"></span><span id="baudrate"></span><span id="BAUDRATE"></span>*BaudRate*  
COM のプロトコルを使用する場合*BaudRate*サーバーの作成時に選択したボー レートが一致する必要があります。

<span id="COMChannel"></span><span id="comchannel"></span><span id="COMCHANNEL"></span>*COMChannel*  
COM のプロトコルを使用する場合*COMChannel*サーバーの作成時に選択したチャンネル番号が一致する必要があります。

<span id="Protocol"></span><span id="protocol"></span><span id="PROTOCOL"></span>*プロトコル*  
SSL または SPIPE プロトコルを使用する場合*プロトコル*サーバーが作成されたときに使用したセキュリティで保護されたプロトコルに一致する必要があります。

<span id="Cert"></span><span id="cert"></span><span id="CERT"></span>*証明書*  
同一を使用する必要があります、SSL または SPIPE プロトコルを使用する場合**certuser =**<em>Cert</em>または**machuser =**<em>Cert</em>使用されたパラメーターサーバーの作成時にします。

<span id="clicon"></span><span id="CLICON"></span>**clicon**  
デバッグ サーバーが逆方向の接続を使用してクライアントに接続しようとするを指定します。 クライアントを使用する必要があります**clicon**サーバーが使用する場合にのみ**clicon**します。 ほとんどの場合、逆方向の接続を使用する場合、デバッグ クライアントはサーバーをデバッグする前に開始されます。

<span id="Password"></span><span id="password"></span><span id="PASSWORD"></span>*パスワード*  
指定する必要がある場合は、サーバーの作成時にパスワードを使用して*パスワード*デバッグのクライアントを作成します。 この値は、元のパスワードと一致する必要があります。 パスワードは大文字小文字が区別されます。 間違ったパスワードが指定されている場合、エラー メッセージは「エラー 0x80004005」を指定します。

<span id="ipversion_6"></span><span id="IPVERSION_6"></span>**ipversion 6 を =**  
(デバッグ ツールの Windows 6.6.07 以前のみ)強制的に IP version 6 を使用するデバッガー バージョン 4、インターネットへの接続に TCP を使用しているときではなく。 Windows Vista およびそれ以降のバージョンでは、デバッガーは、IP バージョン 6、このオプションが不要なために既定値の自動を試みます。

リモート接続パラメーターを手動で指定するには、代わりにキーを押して、**参照**ボタン、**リモート デバッガー セッションへの接続** ダイアログ ボックスと使用、**リモート サーバーの参照**  ダイアログ ボックス。

### <a name="span-idbrowseremoteserversdialogboxspanspan-idbrowseremoteserversdialogboxspanbrowse-remote-servers-dialog-box"></a><span id="browse_remote_servers_dialog_box"></span><span id="BROWSE_REMOTE_SERVERS_DIALOG_BOX"></span>リモート サーバー ダイアログ ボックスの 参照 します。

**リモート サーバーの参照** ダイアログ ボックスで、**マシン**テキスト ボックスで、デバッグ サーバーが実行されているコンピューターの名前を入力します。 (2 つの初期の円記号は省略可能です。"MyBox"と"\\\\MyBox"は、どちらも正しい)。次に、キーを押して、**更新**ボタンをクリックします。

**サーバー**領域には、そのコンピューターで実行されているデバッグ サーバーのすべてが一覧表示されます。 表示されているサーバーのいずれかを選択し、ENTER キーを押しますか をクリックして**OK**します。 (ダブルクリックすることも表示されているサーバーのいずれかです。)選択したデバッグ サーバーの適切な接続文字列で表示されます、**接続文字列**ボックスに、**リモート デバッガー セッションへの接続** ダイアログ ボックス。

接続文字列を含む、サーバーがパスワードで保護されている場合は、**パスワード =\\**<em>します。アスタリスクを置き換える必要があります (</em>*\** *) 実際のパスワードを使用します。

サーバーとパスワードを指定した後にをクリックして**OK**接続を開きます。

このサーバーの一覧、**リモート サーバーの参照** ダイアログ ボックスが存在しないが、正しくシャット ダウンされているサーバーを含めることもできます。 これらの存在しないサーバーのいずれかに接続する場合、エラー メッセージが表示されます。

サーバーの一覧は、プロセス サーバーと KD 接続のサーバーは含まれませんのみを使用してそれらのサーバーを一覧表示、[ファイル |リモートのスタブに接続する](file---connect-to-remote-stub.md)コマンドまたはを実行して**cdb QR** *Server*コマンド プロンプト ウィンドウから。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、リモートへの参加の他のメソッドのデバッグ セッションを参照してください[**デバッグ クライアントをアクティブ化する**](activating-a-debugging-client.md)します。

 

 





