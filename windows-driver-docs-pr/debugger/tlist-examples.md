---
title: TList の例
description: TList の例
ms.assetid: 9c9a1e81-03c2-4b7c-b0da-b25942548aa9
keywords:
- TList、TList 例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d1f614e364bd4a576e2df44c825a2aa1713b8d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357002"
---
# <a name="tlist-examples"></a>TList の例


## <span id="ddk_tlist_examples_dtools"></span><span id="DDK_TLIST_EXAMPLES_DTOOLS"></span>


次の例では、TList を使用する方法を示します。

### <a name="span-idsimplesttlistcommandtlistspanspan-idsimplesttlistcommandtlistspansimplest-tlist-command-tlist"></a><span id="simplest_tlist_command__tlist_"></span><span id="SIMPLEST_TLIST_COMMAND__TLIST_"></span>最も簡単な TList コマンド (tlist)

入力**tlist**せず、追加のパラメーターが存在する場合は、プロセス、プロセス Id (Pid)、およびこれらは、実行しているウィンドウのタイトルを実行しているの一覧を表示します。

```console
c:\>tlist

   0 System Process  
   4 System          
 308 smss.exe        
 356 csrss.exe         
 380 winlogon.exe      NetDDE Agent
 424 services.exe    
 436 lsass.exe       
 604 svchost.exe     
 776 svchost.exe     
 852 spoolsv.exe     
1000 clisvcl.exe     
1036 InoRpc.exe      
1064 InoRT.exe       
1076 InoTask.exe     
1244 WTTSvc.exe        
1492 Sysparse_com.exe  OleMainThreadWndName
1980 explorer.exe      Program Manager
1764 launch32.exe      SMS Client User Application Launcher 
1832 msmsgs.exe        MSBLNetConn
2076 ctfmon.exe        
2128 ISATRAY.EXE       IsaTray
4068 tlist.exe   
```

### <a name="span-idfindaprocessidpspanspan-idfindaprocessidpspanfind-a-process-id--p"></a><span id="find_a_process_id___p_"></span><span id="FIND_A_PROCESS_ID___P_"></span>プロセス ID が見つかりません (-p)

次のコマンドを使用して、 **-p** Explorer.exe (エクスプ ローラー) プロセスのプロセス ID を検索するパラメーターとプロセスの名前。

応答、TList 328 エクスプ ローラーのプロセスのプロセス ID が表示されます。

```console
c:\>tlist -p explorer
328
```

### <a name="span-idfindprocessdetailsusingpidspanspan-idfindprocessdetailsusingpidspanfind-process-details-using-pid"></a><span id="find_process_details_using_pid"></span><span id="FIND_PROCESS_DETAILS_USING_PID"></span>PID を使用してプロセスの詳細を検索します。

次のコマンドは、エクスプ ローラーによるエクスプ ローラーのプロセスの詳細情報の検索が実行されているプロセスのプロセス ID を使用します。

```console
c:\>tlist 328
```

応答、TList は、次の要素を含むエクスプ ローラーのプロセスの詳細を表示します。

-   プロセス ID、実行可能ファイル名、プログラムの表示名。

-   現在の作業ディレクトリ (CWD)。

-   (CmdLine) プロセスを開始したコマンドライン。

-   現在の仮想アドレス空間の値。

-   スレッドの数。

-   プロセスの実行中のスレッドの一覧。 各スレッドでは、TList スレッド ID (TID)、スレッドを実行している関数、エントリ ポイントのアドレス (ある場合) の最後の報告されたエラー、およびスレッドの状態のアドレスが表示されます。

-   プロセスのモジュールの一覧が読み込まれます。 各モジュールのバージョン番号、属性、モジュール、およびモジュールの名前の仮想アドレス TList を表示します。

このコマンドによる出力の抜粋を次に示します。

```console
 328 explorer.exe      Program Manager
   CWD:     C:\Documents and Settings\user01\
   CmdLine: C:\WINDOWS\Explorer.EXE
   VirtualSize:    90120 KB   PeakVirtualSize:   104844 KB
   WorkingSetSize: 19676 KB   PeakWorkingSetSize: 35716 KB
   NumberOfThreads: 17
    332 Win32StartAddr:0x010160cc LastErr:0x00000008 State:Waiting
   1232 Win32StartAddr:0x70a7def2 LastErr:0x00000000 State:Waiting
   1400 Win32StartAddr:0x77f883de LastErr:0x00000000 State:Waiting
   1452 Win32StartAddr:0x77f91e38 LastErr:0x00000000 State:Waiting
   1484 Win32StartAddr:0x70a7def2 LastErr:0x00000006 State:Waiting
   1904 Win32StartAddr:0x74b02ed6 LastErr:0x00000000 State:Ready
   1948 Win32StartAddr:0x72d22ecc LastErr:0x00000000 State:Waiting
   ....  (thread data deleted here)

  6.0.2800.1106 shp  0x01000000  Explorer.EXE
  5.1.2600.1217 shp  0x77F50000  ntdll.dll
  5.1.2600.1106 shp  0x77E60000  kernel32.dll
  7.0.2600.1106 shp  0x77C10000  msvcrt.dll
  5.1.2600.1106 shp  0x77DD0000  ADVAPI32.dll
  5.1.2600.1254 shp  0x78000000  RPCRT4.dll
  5.1.2600.1106 shp  0x77C70000  GDI32.dll
  5.1.2600.1255 shp  0x77D40000  USER32.dll
  ....  (module data deleted here)
```

### <a name="span-idfindmultipleprocessespatternspanspan-idfindmultipleprocessespatternspanfind-multiple-processes-pattern"></a><span id="find_multiple_processes__pattern_"></span><span id="FIND_MULTIPLE_PROCESSES__PATTERN_"></span>複数のプロセス (パターン) を検索します。

次のコマンドは、プロセス名またはプロセスの 1 つまたは複数のウィンドウの名前を表す正規表現によって、プロセスを検索します。 この例では、プロセスをプロセス名でのコマンドは、検索またはウィンドウの名前が「次」で始まる

```console
c:\>tlist ino*
```

応答として、TList Inorpc.exe、Inort.exe、および Inotask.exe プロセスの詳細が表示されます。 上記"検索プロセスを使用して詳細 PID"サブセクションの出力の説明を参照してください。

### <a name="span-iddisplayaprocesstreetspanspan-iddisplayaprocesstreetspandisplay-a-process-tree-t"></a><span id="display_a_process_tree___t_"></span><span id="DISPLAY_A_PROCESS_TREE___T_"></span>プロセス ツリーを表示します (/t)

次のコマンドでは、コンピューターで実行中のプロセスを表すツリーを表示します。 プロセスは、作成したプロセスの子として表示されます。

```console
c:\>tlist /t
```

結果のプロセス ツリーに依存します。 このツリー、特に、作成が表示されます (4) のシステム プロセス Smss.exe プロセスは、Csrss.exe、Winlogon.exe、Lsass.exe、および Rundll32.exe を作成します。 また、Winlogon.exe には、Services.exe、作成したすべてのサービスに関連するプロセスが作成されます。

```console
System Process (0)
System (4)
  smss.exe (404)
    csrss.exe (452)
    winlogon.exe (476) NetDDE Agent
      services.exe (520)
        svchost.exe (700)
        svchost.exe (724)
        svchost.exe (864)
        svchost.exe (888)
        spoolsv.exe (996)
        scardsvr.exe (1040)
        alg.exe (1172)
        atievxx.exe (1200) ATI video bios poller
        InoRpc.exe (1248)
        InoRT.exe (1264)
        InoTask.exe (1308)
        mdm.exe (1392)
        dllhost.exe (2780)
      lsass.exe (532)
      rundll32.exe (500)
explorer.exe (328) Program Manager
  WLANMON.exe (1728) TI Wireless LAN Monitor
  ISATRAY.EXE (1712) IsaTray
  cmmon32.exe (456)
  WINWORD.EXE (844) Tlist.doc - Microsoft Word
  dexplore.exe (2096) Platform SDK - CreateThread
```

### <a name="span-idfindprocessbymodulemspanspan-idfindprocessbymodulemspanfind-process-by-module-m"></a><span id="find_process_by_module___m_"></span><span id="FIND_PROCESS_BY_MODULE___M_"></span>モジュールによってプロセスが見つかりません (/m)

次のコマンドは、すべてのコンピューターで実行されている、特定の DLL を読み込むプロセスを検索します。

```console
c:\>tlist /m 
```

応答として、TList Inorpc.exe、Inort.exe、および Inotask.exe プロセスの詳細が表示されます。 上記"検索プロセスを使用して詳細 PID"サブセクションの出力の説明を参照してください。

 

 





