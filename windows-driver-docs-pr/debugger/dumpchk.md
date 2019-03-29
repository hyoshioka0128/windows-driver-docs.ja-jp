---
title: DumpChk
description: DumpChk
ms.assetid: f7431207-562b-451a-843e-1c2be038e306
keywords:
- DumpChk
ms.date: 09/17/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3fbbd46c8ec6c4e361078394f208fc753dc97c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577898"
---
# <a name="dumpchk"></a>DumpChk


DumpChk (Microsoft クラッシュ ダンプ ファイル チェッカー ツール) は、クラッシュ ダンプ ファイルの簡単な分析を実行するプログラムです。 これにより、ダンプ ファイルの内容に関する概要情報を参照してください。 ダンプ ファイルが、デバッガーによって開くことができませんこのような方法で破損している場合は、この事実を DumpChk が表示されます。

## <a name="span-idwheretogetdumpchkspanspan-idwheretogetdumpchkspanspan-idwheretogetdumpchkspanwhere-to-get-dumpchk"></a><span id="Where_to_get_DumpChk"></span><span id="where_to_get_dumpchk"></span><span id="WHERE_TO_GET_DUMPCHK"></span>DumpChk の入手先


含まれている DumpChk.exe[ツールを Windows のデバッグ](index.md)します。

## <a name="span-iddumpchkcommand-lineoptionsspanspan-iddumpchkcommand-lineoptionsspanspan-iddumpchkcommand-lineoptionsspandumpchk-command-line-options"></a><span id="DumpChk_command-line_options"></span><span id="dumpchk_command-line_options"></span><span id="DUMPCHK_COMMAND-LINE_OPTIONS"></span>DumpChk コマンド ライン オプション


```dbgcmd
DumpChk [-y SymbolPath] DumpFile
```

### <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター

<span id="_______-y________SymbolPath______"></span><span id="_______-y________symbolpath______"></span><span id="_______-Y________SYMBOLPATH______"></span> **-y** *SymbolPath*   
*SymbolPath* DumpChk のシンボルの検索場所を指定します。 シンボル情報は、いくつかのダンプ ファイルに必要な可能性があります。 解決するのには、シンボル名を許可することで、ダンプ ファイルに表示される情報を向上させるためにも役立ちます。

<span id="_______DumpFile______"></span><span id="_______dumpfile______"></span><span id="_______DUMPFILE______"></span> *ダンプ ファイル*   
*DumpFile*を分析するのには、クラッシュ ダンプ ファイルを指定します。 これには、ディレクトリの絶対または相対パスまたは汎用名前付け規則 (UNC) パスを含めることができます。 場合*DumpFile*スペースが含まれることは、引用符で囲む必要があります。

## <a name="span-idusingdumpchkspanspan-idusingdumpchkspanspan-idusingdumpchkspanusing-dumpchk"></a><span id="Using_DumpChk"></span><span id="using_dumpchk"></span><span id="USING_DUMPCHK"></span>DumpChk を使用します。


ダンプ ファイルが壊れている例を示します。 最後に、表示されるエラー `DebugClient cannot open DumpFile`、ある種の破損が発生したことを示します。

```console
C:\Debuggers> dumpchk c:\mydir\dumpfile2.dmp 

Loading dump file c:\mydir\dumpfile2.dmp

Microsoft (R) Windows Debugger Version 6.9.0003.113 X86
Copyright (C) Microsoft. All rights reserved.


Loading Dump File [c:\mydir\dumpfile2.dmp]
Could not match Dump File signature - invalid file format
Could not open dump file [c:\mydir\dumpfile2.dmp], HRESULT 0x80004002
    "No such interface supported"
**** DebugClient cannot open DumpFile - error 80004002   
```

この表示で終わらない単語のため`Finished dump check`、ダンプ ファイルが壊れています。 最後に、エラー メッセージでは、ダンプ ファイルが開けませんについて説明します。

その他のエラーを表示する場合があります、その一部は実際には害のないことに注意してください。 たとえば、次のエラー メッセージは問題を表していません。

```dbgcmd
error 3 InitTypeRead( nt!_PEB at 7ffd5000) 
```

DumpChk 正常な状態のユーザー モードのミニダンプの実行の例を次に示します。 表示が、ダンプ ファイルの全体的要約をで始まり、ダンプ ファイルにどのようなデータが含まれているについての詳細を示します。

```console
C:\Debuggers> dumpchk c:\mydir\dumpfile1.dmp 

Loading dump file c:\mydir\dumpfile1.dmp

Microsoft (R) Windows Debugger Version 6.9.0003.113 X86
Copyright (C) Microsoft. All rights reserved.


Loading Dump File [c:\mydir\dumpfile1.dmp]
User Mini Dump File with Full Memory: Only application data is available

Symbol search path is: srv*C:\CODE\LocalStore*\\symbols\symbols
Executable search path is: 
Windows Vista Version 6000 MP (2 procs) Free x86 compatible
Product: WinNt, suite: SingleUserTS
Debug session time: Tue Jun 17 02:28:23.000 2008 (GMT-7)
System Uptime: 0 days 15:43:52.861
Process Uptime: 0 days 0:00:26.000
...
This dump file has an exception of interest stored in it.
The stored exception information can be accessed via .ecxr.

----- User Mini Dump Analysis

MINIDUMP_HEADER:
Version         A793 (6903)
NumberOfStreams 12
Flags           1826
                0002 MiniDumpWithFullMemory
                0004 MiniDumpWithHandleData
                0020 MiniDumpWithUnloadedModules
                0800 MiniDumpWithFullMemoryInfo
                1000 MiniDumpWithThreadInfo

Streams:
Stream 0: type ThreadListStream (3), size 00000064, RVA 000001BC
  2 threads
  RVA 000001C0, ID 1738, Teb:000000007FFDF000
  RVA 000001F0, ID 1340, Teb:000000007FFDE000
Stream 1: type ThreadInfoListStream (17), size 0000008C, RVA 00000220
  RVA 0000022C, ID 1738
  RVA 0000026C, ID 1340
Stream 2: type ModuleListStream (4), size 00000148, RVA 000002AC
  3 modules
  RVA 000002B0, 00400000 - 00438000: 'C:\CODE\TimeTest\Debug\TimeTest.exe'
  RVA 0000031C, 779c0000 - 77ade000: 'C:\Windows\System32\ntdll.dll'
  RVA 00000388, 76830000 - 76908000: 'C:\Windows\System32\kernel32.dll'
Stream 3: type Memory64ListStream (9), size 00000290, RVA 00001D89
  40 memory ranges
  RVA 0x2019 BaseRva
  range#    RVA      Address      Size
       0 00002019    00010000   00010000
       1 00012019    00020000   00005000
       2 00017019    0012e000   00002000

 (additional stream data deleted)   

Stream 9: type UnusedStream (0), size 00000000, RVA 00000000
Stream 10: type UnusedStream (0), size 00000000, RVA 00000000
Stream 11: type UnusedStream (0), size 00000000, RVA 00000000


Windows Vista Version 6000 MP (2 procs) Free x86 compatible
Product: WinNt, suite: SingleUserTS
kernel32.dll version: 6.0.6000.16386 (vista_rtm.061101-2205)
Debug session time: Tue Jun 17 02:28:23.000 2008 (GMT-7)
System Uptime: 0 days 15:43:52.861
Process Uptime: 0 days 0:00:26.000
  Kernel time: 0 days 0:00:00.000
  User time: 0 days 0:00:00.000
PEB at 7ffd9000
    InheritedAddressSpace:    No
    ReadImageFileExecOptions: No
    BeingDebugged:            Yes
    ImageBaseAddress:         00400000
    Ldr                       77a85d00
    Ldr.Initialized:          Yes
    Ldr.InInitializationOrderModuleList: 002c1e30 . 002c2148
    Ldr.InLoadOrderModuleList:           002c1da0 . 002c2138
    Ldr.InMemoryOrderModuleList:         002c1da8 . 002c2140
            Base TimeStamp                     Module
          400000 47959d85 Jan 21 23:38:45 2008 C:\CODE\TimeTest\Debug\TimeTest.exe
        779c0000 4549bdc9 Nov 02 02:43:37 2006 C:\Windows\system32\ntdll.dll
        76830000 4549bd80 Nov 02 02:42:24 2006 C:\Windows\system32\kernel32.dll
    SubSystemData:     00000000
    ProcessHeap:       002c0000
    ProcessParameters: 002c14c0
    WindowTitle:  'C:\CODE\TimeTest\Debug\TimeTest.exe'
    ImageFile:    'C:\CODE\TimeTest\Debug\TimeTest.exe'
    CommandLine:  '\CODE\TimeTest\Debug\TimeTest.exe'
    DllPath:      'C:\CODE\TimeTest\Debug;C:\Windows\system32;C:\Windows\system;
    Environment:  002c0808
        =C:=C:\CODE
        =ExitCode=00000000
        ALLUSERSPROFILE=C:\ProgramData
        AVENGINE=C:\PROGRA~1\CA\SHARED~1\SCANEN~1
        CommonProgramFiles=C:\Program Files\Common Files
        COMPUTERNAME=EMNET
        ComSpec=C:\Windows\system32\cmd.exe
        configsetroot=C:\Windows\ConfigSetRoot
        FP_NO_HOST_CHECK=NO
        HOMEDRIVE=C:
        NUMBER_OF_PROCESSORS=2
        OS=Windows_NT
        Path=C:\DTFW\200804~2.113\winext\arcade;C:\Windows\system32
        PATHEXT=.COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC
        PROCESSOR_ARCHITECTURE=x86
        PROCESSOR_IDENTIFIER=x86 Family 6 Model 15 Stepping 13, GenuineIntel
        PROCESSOR_LEVEL=6
        PROCESSOR_REVISION=0f0d
        ProgramData=C:\ProgramData
        ProgramFiles=C:\Program Files
        PROMPT=$P$G
        PUBLIC=C:\Users\Public
        RoxioCentral=C:\Program Files\Common Files\Roxio Shared\9.0\Roxio Central33\
        SESSIONNAME=Console
        SystemDrive=C:
        SystemRoot=C:\Windows
        USERDNSDOMAIN=NORTHSIDE.COMPANY.COM
        USERDOMAIN=NORTHSIDE
        USERNAME=myname
        USERPROFILE=C:\Users\myname
        WINDBG_DIR=C:\DTFW\200804~2.113
        windir=C:\Windows
        WINLAYTEST=200804~2.113
        _NT_SOURCE_PATH=C:\mysources
        _NT_SYMBOL_PATH=C:\mysymbols
Finished dump check
```

ダンプ ファイル - ここでは、アプリケーション データがないオペレーティング システムのデータを含む、完全なメモリの情報をユーザー モードのミニダンプの特性を識別することによって、出力を開始します。 DumpChk、し、ダンプ ファイルの内容の概要で使用されているシンボル パスが続きます。

この表示は、単語で終わるため`Finished dump check`、ダンプ ファイルが壊れて、おそらくいないと、デバッガーによって開くことができます。 ただし、corrruption の他の微妙な形式をファイルに存在する可能性があります。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Windows 用デバッグ ツールに含まれるツール](extra-tools.md)

 

 






