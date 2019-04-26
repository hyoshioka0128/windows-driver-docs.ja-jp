---
title: WIA ミニドライバーのデバッグ
description: WIA ミニドライバーのデバッグ
ms.assetid: 6466d0db-a2f9-4b3e-aa3e-8030b243f862
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6df7c6a5e6cb14575afc1bd1edc9aec20c871a8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352686"
---
# <a name="wia-minidriver-debugging"></a>WIA ミニドライバーのデバッグ





WIA ドライバーは、WIA のサービス プロセス内で実行されます。 したがって、これらのドライバーのユーザー モードのデバッグを実行するには、WIA サービスにデバッガーを接続する必要があります。 これにはいくつかの方法があります。このトピックでは、そのうち 2 つを示します。 (詳細については、Microsoft Windows SDK ドキュメントでのデバッグ サービスを参照してください。)

2 つの方法のいずれかで、デバッガーを開始できます。

-   によって自動的にデバッガーの下で、WIA サービスを開始しています。

-   によって実行時に適切なプロセスにデバッガーをアタッチします。

次に、2 つの点に注意してください。

シンボルと、デバッガー内から他のファイルへのネットワーク アクセスが必要な場合これらでは、デバッガーの下で、WIA サービスを自動的に開始する場合に表示される可能性がありますできません。 WIA では、Microsoft Windows Server 2003 およびそれ以降のオペレーティング システム バージョンの Windows XP では、LocalSystem サービスとは、LocalService としてを実行し、ネットワークにアクセスする適切な特権がありません。 そのため、場合でも、コンピューター「確認」できるすべてのネットワーク上、サービスを実行してデバッガーできないことがありますに。 WIA サービスの詳細についてには、特権レベルの変更後、参照してください[WIA ドライバーに関するセキュリティの問題](security-issues-for-wia-drivers.md)します。

-   ドライバーの読み込みまたはドライバーの STI 部分の初期化中に問題が発生した場合 (たとえば中、 [ **IStiUSD::Initialize**](https://msdn.microsoft.com/library/windows/hardware/ff543824))、デバッガーがアタッチされている時間で、エラーが既に発生し、有用な情報を取得するには遅すぎます。 この問題の一般的な症状は、デバイスが表示されないで、**マイ コンピューター**フォルダーが*は*に表示、**デバイス マネージャー**フォルダー。

### <a name="starting-the-wia-service-under-a-debugger"></a>デバッガーの下で、WIA サービスの開始

WIA サービスを開始すると、サービス コントロール マネージャー (SCM) は、サービス管理データベースにエントリを検索し、そのエントリが指す実行可能ファイルを起動します。 デバッガーの下で、WIA サービスを開始する簡単な方法では、デバッガーが含まれるいずれかでそのエントリを置き換えます。 エントリは、下のレジストリで見つかんだことができます。

**HKLM\\System\\CurrentControlSet\\Services\\StiSvc\\ImagePath**

最初に、 **ImagePath**キーは、次の文字列値に設定されます。

"**%SystemRoot%\\System32\\svchost.exe -k imgsvc**"

NTSD で WIA サービスを実行するには、よう、上記の値を変更など。

"**ntsd -g -G %SystemRoot%\\System32\\svchost.exe -k imgsvc**"

この変更により、WIA サービスは、常に NTSD で開始します。 サービスが既に実行されている場合にする必要があります停止および再起動この変更を反映する前に注意してください。 参照してください[の開始と停止もイメージ サービス](starting-and-stopping-the-still-image-service.md)詳細についてはします。

デバッガーのウィンドウを表示するには、別のレジストリ キーを変更する必要があります。 このレジストリ キーへのパスは次のとおりです。

**HKLM\\System\\CurrentControlSet\\Services\\StiSvc\\Type**

初期値、**型**キー、0X20、デバッガーのウィンドウが表示されないようにします。 値を変更、**型**0X120 DWORD 値をキー。

### <a name="attaching-the-debugger-at-run-time"></a>実行時に、デバッガーをアタッチします。

ほとんどのデバッガーでは、プロセスが既に開始した後、それにアタッチするには、実行中のプロセスの PID が必要です。 WIA がという汎用ホスト プロセスで実行されるので*svchost.exe*の適切なインスタンスを検索*svchost.exe*が不可欠です。

デバッガー パッケージを Microsoft のサイト (www.microsoft.com) からダウンロードした場合、ユーティリティ プログラムという名前にはが含まれます*tlist.exe*します。 *Tlist.exe*実行中のすべてのプロセスが表示されます。 実行する場合*tlist.exe*のスイッチを使用して、このユーティリティも表示するサービスをホストするプロセス。 たとえば、実行している*tlist.exe-s*次のような出力が生成されます。

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

前の例では、5 つのインスタンスで*svchost.exe*を実行しています。 WIA サービス**StiSvc** (Still Image service) を実行している、 *svchost.exe*の PID が 1076 インスタンス。 デバッグを開始する 1076 のプロセスにデバッガーをアタッチします。

などのユーティリティ プログラムを使用してではなく*tlist.exe、* 複数の 1 つのインスタンスを識別するために*svchost.exe* 、インスタンスのコピーを作成することができます*svchost.exe*の名前を変更(たとえば、 *stisvc.exe*)。 次に、サービス コントロールのエントリを変更**ImagePath**のこのコピーを使用する値*svchost.exe* (ここでは名前が 1 つ*stisvc.exe*)。 たとえば、パスがあるキーを設定することができます。

**HKLM\\System\\CurrentControlSet\\Control\\Services\\Stisvc\\ImagePath**

次の文字列値。

"**%SystemRoot%\\System32\\stisvc.exe -k imgsvc**"

ここで、WIA サービスの開始時に実行*stisvc.exe*の代わりに*svchost.exe*します。 インスタンスが 1 つだけがあるため、このプロセスの検索が簡単、 *stisvc.exe*します。 アプリを確認する PID を検索する必要はありません。 したがって、たとえば、Microsoft Visual Studio を使用してドライバーを開発している場合に進んで、**デバッグの開始**下にあるメニュー項目、**ビルド** メニューのをクリックして**プロセスにアタッチしています.**、選択および*stisvc.exe*一覧にします。
