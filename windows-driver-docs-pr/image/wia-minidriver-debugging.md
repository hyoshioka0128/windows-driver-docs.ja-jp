---
title: WIA ミニドライバーのデバッグ
description: WIA ミニドライバーのデバッグ
ms.assetid: 6466d0db-a2f9-4b3e-aa3e-8030b243f862
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0db7e17f8422d7128c767e041e06a5d6b28807fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840678"
---
# <a name="wia-minidriver-debugging"></a>WIA ミニドライバーのデバッグ





Wia ドライバーは、WIA サービスプロセス内で実行されます。 そのため、これらのドライバーのユーザーモードデバッグを実行するには、デバッガーを WIA サービスに接続する必要があります。 これを行うには、いくつかの方法があります。このトピックでは、その2つを紹介します。 (詳細については、Microsoft Windows SDK のドキュメントの「デバッグサービス」を参照してください)。

デバッガーは、次の2つの方法のいずれかで起動できます。

-   デバッガーで WIA サービスを自動的に開始します。

-   実行時に適切なプロセスにデバッガーをアタッチします。

次の2つの点に注意してください。

デバッガー内からシンボルおよびその他のファイルへのネットワークアクセスが必要な場合、デバッガーで WIA サービスを自動的に開始すると、これらのファイルが表示されないことがあります。 WIA は、Windows XP では LocalSystem サービスとして、Microsoft Windows Server 2003 以降のバージョンのオペレーティングシステムでは LocalService として実行され、ネットワークにアクセスするための適切な特権を持っていません。 このため、コンピューターがネットワーク上のすべてを "参照" できる場合でも、サービスを実行しているデバッガーができない可能性があります。 WIA サービスの変更された特権レベルの詳細については、「 [Wia ドライバーのセキュリティの問題](security-issues-for-wia-drivers.md)」を参照してください。

-   ドライバーのメッセージの読み込みまたは初期化中に問題が発生した場合 (例[ **: I後部 usd:: Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)の実行中)、デバッガーがアタッチされたときに、エラーが既に発生していて、役に立つ情報を取得するには遅すぎます。 この問題の一般的な症状は、デバイスが**マイコンピューター**フォルダーに表示されず、**デバイスマネージャー**フォルダー*に表示さ*れることです。

### <a name="starting-the-wia-service-under-a-debugger"></a>デバッガーでの WIA サービスの開始

WIA サービスが開始されると、サービスコントロールマネージャー (SCM) がサービスコントロールデータベースのエントリを参照し、そのエントリが指す実行可能ファイルを起動します。 デバッガーで WIA サービスを開始する簡単な方法は、そのエントリをデバッガーを含むエントリに置き換えることです。 エントリは、次のレジストリにあります。

**HKLM\\System\\CurrentControlSet\\Services\\StiSvc\\ImagePath**

最初に、 **ImagePath**キーは次の文字列値に設定されます。

" **% SystemRoot%\\System32\\svchost.exe-k imgsvc**"

たとえば、NTSD で WIA サービスを実行するには、前の値を次のように変更します。

"**ntsd-g-g% SystemRoot%\\System32\\svchost.exe-k imgsvc**"

この変更により、WIA サービスは常に NTSD で開始されます。 サービスが既に実行されている場合は、この変更が有効になる前に、サービスを停止して再起動する必要があることに注意してください。 詳細について[は、「イメージサービスの開始と停止](starting-and-stopping-the-still-image-service.md)」を参照してください。

デバッガーのウィンドウが表示されるようにするには、別のレジストリキーも変更する必要があります。 このレジストリキーへのパスは次のとおりです。

**HKLM\\System\\CurrentControlSet\\Services\\StiSvc\\型**

**型**キーの初期値0x20 は、デバッガーウィンドウが表示されないようにします。 **型**キーの値を DWORD 値0X120 に変更します。

### <a name="attaching-the-debugger-at-run-time"></a>実行時のデバッガーのアタッチ

ほとんどのデバッガーでは、プロセスが既に開始された後にアタッチするために、実行中のプロセスの PID が必要になります。 WIA は*svchost.exe*と呼ばれる汎用ホスティングプロセスで実行されるため、 *svchost.exe*の正しいインスタンスを見つけることが不可欠です。

Microsoft サイト (www.microsoft.com) からデバッガーパッケージをダウンロードした場合は、 *tlist.exe*という名前のユーティリティプログラムが含まれています。 *Tlist.exe*は、実行中のすべてのプロセスを表示します。 S スイッチを使用して*tlist.exe*を実行すると、このユーティリティは、どのプロセスがどのサービスをホストしているかも示します。 たとえば、 *tlist.exe-s*を実行すると、次のような出力が生成されます。

```console
   0 System Process
   4 System
 160 smss.exe
 216 csrss.exe       Title:
 208 winlogon.exe    Title: NetDDE Agent
 268 services.exe    Svcs:  Eventlog,PlugPlay
 280 lsass.exe       Svcs:  Netlogon,PolicyAgent,ProtectedStorage,SamSs
 416 svchost.exe     Svcs:  RpcSs
 444 svchost.exe     Svcs:  AudioSrv,CryptSvc,Dhcp,EventSystem,FastUserSwitching,CompatibilityServices,helpsvc,Irmon,lanmanserver,lanmanworkstation,Netman,Nla,Schedule,SENS,ShellHWDetection,srservice,TapiSrv,TermService,ThemeService,uploadmgr,W32Time,winmgmt,WmdmPmSp
 504 svchost.exe     Svcs:  Dnscache
 372 svchost.exe     Svcs:  LmHosts,Messenger,RemoteRegistry,SSDPSRV,WebClient
 616 spoolsv.exe     Svcs:  Spooler
 680 inojobsv.exe    Svcs:  Cheyenne InocuLAN Anti-Virus Server
 700 emsvc.exe       Svcs:  EMSVC
 912 fxssvc.exe      Svcs:  Fax
 192 explorer.exe    Title: Program Manager
1076 svchost.exe     Svcs:  stisvc
22824 tlist.exe
```

前の例では、 *svchost.exe*の5つのインスタンスが実行されています。 WIA サービスである**Stisvc** (静止イメージサービス) は、PID が1076の*svchost.exe*インスタンスで実行されています。 デバッガーをプロセス1076にアタッチして、デバッグを開始します。

*Tlist.exe*などのユーティリティプログラムを使用して複数の*svchost.exe*インスタンスの1つのインスタンスを識別する代わりに、 *svchost.exe*のコピーを作成して名前を変更できます (たとえば、 *stisvc .exe*)。 次に、この*svchost.exe*のコピーを使用するようにサービスコントロールエントリの**ImagePath**値を変更します (名前が*stisvc .exe*であるもの)。 たとえば、次のパスを持つキーを設定できます。

**HKLM\\System\\CurrentControlSet\\コントロール\\サービス\\Stisvc\\ImagePath**

次の文字列値になります。

" **% SystemRoot%\\System32\\stisvc .exe-k imgsvc**"

これで、WIA サービスが開始されると、 *svchost.exe*ではなく、 *stisvc .exe*の下で実行されます。 このプロセスは、 *stisvc .exe*のインスタンスが1つしかないため、簡単に見つけることができます。 PID を検索する必要はありません。 このため、Microsoft Visual Studio を使用してドライバーを開発している場合は、 **[ビルド]** メニューの **[デバッグの開始]** メニューをクリックし、 **[プロセスにアタッチ...]** をクリックして、一覧で [ *stisvc .exe* ] を選択します。
