---
title: ファイルがリモートのスタブに接続します。
description: ファイルがリモートのスタブに接続します。
ms.assetid: 7357db85-babe-4729-9a20-76ba284f5bf3
keywords:
- ファイルがリモートのスタブに接続します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17ac4cddbd21738c868914217c85a5d422abccd7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354908"
---
# <a name="file--connect-to-remote-stub"></a>File | Connect to Remote Stub (ファイル | リモート スタブに接続)


をクリックして**リモート スタブへの接続**上、**ファイル**WinDbg スマート クライアントを作成し、プロセス サーバー、または KD 接続のサーバーに接続するメニュー。

このコマンドを使用すると、ユーザー モード、または、-k kdsrv トランスポート プロトコル コマンド ライン オプションのカーネル モードでは、premote コマンド ライン オプション。 このコマンドは、WinDbg が休止モードである場合にのみ使用できます。

このコマンドは、デバッグ サーバーへの接続を使用することはできません。そのために、使用[ファイル |リモート セッションに接続する](file---connect-to-remote-session.md)代わりにします。

### <a name="span-idconnecttoremotestubserverdialogboxspanspan-idconnecttoremotestubserverdialogboxspanconnect-to-remote-stub-server-dialog-box"></a><span id="connect_to_remote_stub_server_dialog_box"></span><span id="CONNECT_TO_REMOTE_STUB_SERVER_DIALOG_BOX"></span>スタブのリモート サーバー ダイアログ ボックスへの接続します。

クリックすると**リモート スタブへの接続**、**スタブのリモート サーバーへの接続** ダイアログ ボックスが表示されます。 このダイアログ ボックスを使用して、リモート接続パラメーターを入力するか、プロセス サーバーと KD 接続のサーバーの一覧を参照します。

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
プロセス サーバー、または KD 接続のサーバーが作成されたコンピューターのネットワーク名。 この名前の円記号は付けません (**\\\\**)。

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
(Windows 2000 以降)SSL または SPIPE プロトコルを使用する場合*プロトコル*サーバーが作成されたときに使用したセキュリティで保護されたプロトコルに一致する必要があります。

<span id="Cert"></span><span id="cert"></span><span id="CERT"></span>*証明書*  
(Windows 2000 以降)同一を使用する必要があります、SSL または SPIPE プロトコルを使用する場合**certuser =**<em>Cert</em>または**machuser =**<em>Cert</em>使用されたパラメーターサーバーの作成時にします。

<span id="clicon"></span><span id="CLICON"></span>**clicon**  
プロセス サーバー、または KD 接続のサーバーは逆方向の接続を使用してクライアントに接続を試むことを指定します。 クライアントを使用する必要があります**clicon**サーバーが使用する場合にのみ**clicon**します。 ほとんどの場合、逆方向の接続を使用すると、スマート クライアントは、サーバーの前に開始されます。

<span id="Password"></span><span id="password"></span><span id="PASSWORD"></span>*パスワード*  
指定する必要がある場合は、サーバーの作成時にパスワードを使用して*パスワード*スマート クライアントを作成します。 この値は、元のパスワードと一致する必要があります。 パスワードは大文字小文字が区別されます。 間違ったパスワードが指定されている場合、エラー メッセージは「エラー 0x80004005」を指定します。

<span id="ipversion_6"></span><span id="IPVERSION_6"></span>**ipversion 6 を =**  
(デバッグ ツールの Windows 6.6.07 以前のみ)強制的に IP version 6 を使用するデバッガー バージョン 4、インターネットへの接続に TCP を使用しているときではなく。 Windows Vista およびそれ以降のバージョンでは、デバッガーは、IP バージョン 6、このオプションが不要なために既定値の自動を試みます。

リモート接続パラメーターを手動で指定するには、代わりにキーを押して、**参照**ボタン、**スタブのリモート サーバーへの接続** ダイアログ ボックスと使用、 **のリモートサーバーの参照**  ダイアログ ボックス。

### <a name="span-idbrowseremoteserversdialogboxspanspan-idbrowseremoteserversdialogboxspanbrowse-remote-servers-dialog-box"></a><span id="browse_remote_servers_dialog_box"></span><span id="BROWSE_REMOTE_SERVERS_DIALOG_BOX"></span>リモート サーバー ダイアログ ボックスの 参照 します。

**リモート サーバーの参照** ダイアログ ボックスで、**マシン**テキスト ボックスに、プロセス サーバー、または KD 接続のサーバーで実行しているコンピューターの名前を入力します。 (2 つの初期の円記号は省略可能です。"MyBox"と"\\\\MyBox"は、どちらも正しい)。次に、キーを押して、**更新**ボタンをクリックします。

**サーバー**領域には、すべてのプロセス サーバーとそのコンピューターで実行されている KD 接続のサーバーが一覧表示されます。 表示されているサーバーのいずれかを選択し、ENTER キーを押しますか をクリックして**OK**します。 (ダブルクリックすることも表示されているサーバーのいずれかです。)選択したプロセス サーバーの適切な接続文字列で表示されます、**接続文字列**ボックスに、**スタブのリモート サーバーへの接続** ダイアログ ボックス。

接続文字列を含む、サーバーがパスワードで保護されている場合は、**パスワード =\\**<em>します。アスタリスクを置き換える必要があります (</em>*\** *) 実際のパスワードを使用します。

サーバーとパスワードを指定した後にをクリックして**OK**接続を開きます。

サーバーの一覧、**リモート サーバーの参照** ダイアログ ボックスが存在しないが、正しくシャット ダウンされているサーバーを含めることもできます。 これらの存在しないサーバーのいずれかに接続する場合、エラー メッセージが表示されます。

サーバーの一覧では、サーバーのデバッグは含まれません。 これらのサーバーを表示する、[ファイル |リモート セッションに接続する](file---connect-to-remote-session.md)コマンド。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、および、他のメソッド スタブのリモート セッションに参加するは、「 [**スマート クライアントのアクティブ化**](activating-a-smart-client.md)と[**スマート クライアント (カーネル モード)をアクティブ化する**](activating-a-smart-client--kernel-mode-.md).

 

 





