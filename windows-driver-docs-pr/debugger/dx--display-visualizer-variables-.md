---
title: dx (デバッガー オブジェクト モデル式の表示)
description: Dx コマンドでは、NatVis の拡張機能モデルを使用して、C++ の式が表示されます。 Dx コマンドは、デバッガー オブジェクトで動作します。
ms.assetid: 93047911-5195-4FB9-A015-5349084EDC0A
keywords:
- dx (表示デバッガー オブジェクト モデルの式) Windows のデバッグ
ms.date: 05/28/2019
topic_type:
- apiref
api_name:
- dx (Display Debugger Object Model Expression)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 65d63e3469b6e18f58eebcbbe245f81364156828
ms.sourcegitcommit: e123b8b69473c0ebc0383ef722452866bf6662d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2019
ms.locfileid: "66394278"
---
# <a name="dx-display-debugger-object-model-expression"></a>dx (デバッガー オブジェクト モデル式の表示)


**Dx**コマンドは、NatVis の拡張機能モデルを使用して、C++ の式を表示します。 NatVis の詳細については、次を参照してください。[ネイティブ オブジェクトのカスタム ビューを作成](https://msdn.microsoft.com/library/jj620914.aspx)です。

```dbgcmd
dx [-g|-gc #][-c #][-n|-v]-r[#] Expression[,<FormatSpecifier> ]
dx [{-?}|{-h}]
```

## <a name="span-idddkcmddisplaytypedbgspanspan-idddkcmddisplaytypedbgspanparameters"></a><span id="ddk_cmd_display_type_dbg"></span><span id="DDK_CMD_DISPLAY_TYPE_DBG"></span>パラメーター


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *式*   
表示する C++ の式。

<span id="_______-g______"></span><span id="_______-G______"></span> **-g**   
反復可能なデータ グリッド オブジェクトとして表示されます。 要素は、グリッド内の行と表示のそれぞれの子要素の列は、各反復処理されます。 これにより、配列などの構造体、配列の各要素が行に表示されます、構造体の各フィールドは、列に表示されるものを表示することができます。

列名を左クリックして (DML リンクの可用性がある)、その列で並べ替えられます。 その列で既に並べ替えられて場合、並べ替え順序が反転します。

これは、反復可能な任意のオブジェクトが必要で 'グリッドとして表示' と呼ばれる DML を使用して追加された項目を右クリック コンテキスト メニューがあります。 出力ウィンドウ内のオブジェクトを右クリックし、これを選択する標準のツリー ビューではなくグリッド ビューでは、オブジェクトが表示されます。

(+) が表示される列で提供することでという名前を右クリックし、動作を左クリックします。

-   左クリックは、その列を受け取り、独自のテーブルに分解することです。 元の行と展開された列の子を参照してください。
-   右クリックでは、"展開に Grid"列を取得し、適切なほとんどの列として、現在のテーブルに再度追加提供します。

<span id="_______-gc________"></span><span id="_______-GC________"></span> **-gc \#**    
グリッドとして表示し、グリッド セルのサイズを指定した数に制限 (\#) 文字。

<span id="_______-c________"></span><span id="_______-C________"></span> **-c \#**    
コンテナーの継続が表示されます (スキップ\#コンテナーの要素)。このオプションは、出力のカスタム自動化のシナリオで通常使用され、提供を「...」一覧の下部にある要素を継続します。

<span id="_______-n______"></span><span id="_______-N______"></span> **-n**   
データを表示できる 2 つの方法はあります。 NatVis 視覚化 (既定値) を使用して、または、基になるネイティブ C/C++ 構造体を使用します。 ネイティブの C/C++ 構造体だけと NatVis 視覚化ではないを使用して出力を表示するために-n パラメーターを指定します。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
メソッドとその他の非標準のオブジェクトを含む詳細な情報を表示します。

<span id="_______-r_______"></span><span id="_______-R_______"></span> **-r**<em>\#</em>   
再帰的に表示 (フィールド) を最大サブタイプ *\#* レベル。 場合 *\#* は既定値は、1 つの再帰レベルを指定しません。

<span id="__________FormatSpecifier_________"></span><span id="__________formatspecifier_________"></span><span id="__________FORMATSPECIFIER_________"></span> **\[&lt;、FormatSpecifier&gt;\]**    
既定のレンダリングを変更するのにには、次の書式指定子のいずれかを使用します。

|                         |                                                                                          |
|-------------------------|------------------------------------------------------------------------------------------|
| 、x                      | 序数を 16 進数で表示します。                                                          |
| 、d                      | 序数を 10 進数で表示します。                                                              |
| 、o                      | 序数を 8 進数で表示します。                                                                |
| 、b                      | バイナリ内の序数を表示します。                                                               |
| 、en                     | 名前のみ (値なし) で列挙型を表示します。                                                    |
| 、c                      | 単一の文字 (文字列ではなく) として表示します。                                               |
| 、s                      | 引用符で囲まれた ASCII 8 ビットの文字列を表示します。                                                    |
| 、sb                     | クォート ASCII として 8 ビットの文字列を表示                                                  |
| 、s8                     | Utf-8 の引用符で囲まれた 8 ビットの文字列を表示します。                                                    |
| 、s8b                    | Utf-8 引用符として 8 ビットの文字列を表示                                                  |
| 、su                     | 16 ビットの文字列を utf-16 に引用符で囲まれた表示します。                                                  |
| 、サブ                    | 16 ビットの文字列を utf-16 unqouted として表示します。                                                |
| ,!                      | Raw モードでのみオブジェクトを表示する (例:: NatVis なし)                                       |
| ,\#                     | リテラル値としてポインター/配列/コンテナーの長さを指定\#(数値に置き換えます) |
| 、\[&lt;式&gt;\] | 式と、ポインター/配列/コンテナーの長さを指定&lt;式&gt;           |
| 、nd                     | オブジェクトの派生 (runtype) 型が見つからない。 静的な値のみを表示します。          |

<span id="_______dx_-_______"></span><span id="_______DX_-_______"></span> **dx** { **-?** }   
コマンド ライン ヘルプを表示します。

<span id="_______dx_-h______"></span><span id="_______DX_-H______"></span> **dx** { **-h**}   
デバッガーで使用可能なオブジェクトのヘルプを表示します。

<span id="_______dx_-id______"></span><span id="_______DX_-ID______"></span> **dx** { **-id**}   
Microsoft 内部使用のみです。 コマンドの出力でデータ モデルのリンクをたどるために使用します。

## <a name="command-line-usage-example"></a>コマンドラインの使用例

デバッグの設定のオブジェクトに関する情報を表示する .dx 設定 コマンドを使用できます。 デバッグの設定オブジェクトの詳細については、次を参照してください。 [ **.settings** ](-settings--set-debug-settings-.md)します。
```dbgcmd
kd> dx -r1 Debugger.Settings
Debugger.Settings : 
    Display          : 
    EngineInitialization : 
    Extensions       : 
    Input            : 
    Sources          : 
    Symbols          : 
    AutoSaveSettings : false
```

オプションを使用する r1 再帰デバッガーの他のオブジェクトを表示する、セッション、設定と状態。

```dbgcmd
kd> dx -r1 Debugger
Debugger : 
  Sessions : 
  Settings : 
  State    : 
```

Debugger.Sessions を指定するオブジェクトを移動するは、r3 再帰オプションをさらに、オブジェクトのチェーンをダウンします。

```dbgcmd
kd> dx -r3 Debugger.Sessions
Debugger.Sessions : 
  [0]              : Remote KD: KdSrv:Server=@{<Local>},Trans=@{1394:Channel=0}
    Processes : 
      [0]              : <Unknown Image>
      [4]              : <Unknown Image>
      [304]            : smss.exe
      [388]            : csrss.exe
      [456]            : wininit.exe
      [468]            : csrss.exe
      [528]            : services.exe
      [536]            : lsass.exe
      [544]            : winlogon.exe
      [620]            : svchost.exe
       ...               ...
```

序数値を 16 進数で表示する、x 書式指定子を追加します。

```dbgcmd
kd> dx -r3 Debugger.Sessions,x
Debugger.Sessions,x : 
  [0x0]            : Remote KD: KdSrv:Server=@{<Local>},Trans=@{1394:Channel=0}
    Processes : 
      [0x0]            : <Unknown Image>
      [0x4]            : <Unknown Image>
      [0x130]          : smss.exe
      [0x184]          : csrss.exe
      [0x1c8]          : wininit.exe
      [0x1d4]          : csrss.exe
      [0x210]          : services.exe
      [0x218]          : lsass.exe
      [0x220]          : winlogon.exe
      [0x26c]          : svchost.exe
      [0x298]          : svchost.exe
      [0x308]          : dwm.exe
      [0x34c]          : nvvsvc.exe
      [0x37c]          : nvvsvc.exe
      [0x384]          : svchost.exe
       ...               ...
```

この例では、アクティブ デバッグ セッションを使用して、最初のプロセスの最初のスレッドの呼び出し履歴を一覧表示します。

```dbgcmd
kd> dx -r1 Debugger.Sessions.First().Processes.First().Threads.First().Stack.Frames
Debugger.Sessions.First().Processes.First().Threads.First().Stack.Frames : 
    [0x0]            : nt!RtlpBreakWithStatusInstruction
    [0x1]            : nt!KdCheckForDebugBreak + 0x7a006
    [0x2]            : nt!KiUpdateRunTime + 0x42
    [0x3]            : nt!KiUpdateTime + 0x129
    [0x4]            : nt!KeClockInterruptNotify + 0x1c3
    [0x5]            : hal!HalpTimerClockInterruptEpilogCommon + 0xa
    [0x6]            : hal!HalpTimerClockInterruptCommon + 0x3e
    [0x7]            : hal!HalpTimerClockInterrupt + 0x1cb
    [0x8]            : nt!KiIdleLoop + 0x1a
```

データ グリッドとして出力を表示するのにには、-g オプションを使用します。 並べ替えのキー列をクリックします。

```dbgcmd
kd> dx -g @$curprocess.Modules
```

![output from dx -g @$curprocess.modules showing columnar grid output](images/dx-grid-example.png)

オブジェクトに関する情報を表示するのにには、-h オプションを使用します。
```dbgcmd
kd>  dx -h Debugger.State
Debugger.State   [State pertaining to the current execution of the debugger (e.g.: user variables)]
    DebuggerVariables [Debugger variables which are owned by the debugger and can be referenced by a pseudo-register prefix of @$]
    PseudoRegisters   [Categorizied debugger managed pseudo-registers which can be referenced by a pseudo-register prefix of @$]
    UserVariables     [User variables which are maintained by the debugger and can be referenced by a pseudo-register prefix of @$]
```

## <a name="displaying-teb-and-peb-information-using-the-environment-object"></a>環境のオブジェクトを使用して TEB と PEB の情報を表示します。

スレッドとプロセスに関連付けられている TEB と PEB の情報を表示するのにには、環境のオブジェクトを使用します。

TEB を表示するに関連付けられている現在のスレッドの使用してこのコマンド。

```dbgcmd
0: kd> dx -r2 @$curthread.Environment
@$curthread.Environment                
    EnvironmentBlock [Type: _TEB]
        [+0x000] NtTib            [Type: _NT_TIB]
        [+0x038] EnvironmentPointer : Unable to read memory at Address 0x38
        [+0x040] ClientId         [Type: _CLIENT_ID]
        [+0x050] ActiveRpcHandle  : Unable to read memory at Address 0x50
        [+0x058] ThreadLocalStoragePointer : Unable to read memory at Address 0x58
        [+0x060] ProcessEnvironmentBlock : Unable to read memory at Address 0x60
        [+0x068] LastErrorValue   : Unable to read memory at Address 0x68
        [+0x06c] CountOfOwnedCriticalSections : Unable to read memory at Address 0x6c
        [+0x070] CsrClientThread  : Unable to read memory at Address 0x70
        [+0x078] Win32ThreadInfo  : Unable to read memory at Address 0x78
        [+0x080] User32Reserved   [Type: unsigned long [26]]
        [+0x0e8] UserReserved     [Type: unsigned long [5]]
        [+0x100] WOW32Reserved    : Unable to read memory at Address 0x100
        [+0x108] CurrentLocale    : Unable to read memory at Address 0x108
        [+0x10c] FpSoftwareStatusRegister : Unable to read memory at Address 0x10c
         ...
```

PEB を表示するには、このコマンドを現在のプロセス使用に伴います。

```dbgcmd
0: kd> dx -r2 @$curprocess.Environment
@$curprocess.Environment                
    EnvironmentBlock [Type: _PEB]
        [+0x000] InheritedAddressSpace : Unable to read memory at Address 0x0
        [+0x001] ReadImageFileExecOptions : Unable to read memory at Address 0x1
        [+0x002] BeingDebugged    : Unable to read memory at Address 0x2
        [+0x003] BitField         : Unable to read memory at Address 0x3
        [+0x003 ( 0: 0)] ImageUsesLargePages : Unable to read memory at Address 0x3
        [+0x003 ( 1: 1)] IsProtectedProcess : Unable to read memory at Address 0x3
        [+0x003 ( 2: 2)] IsImageDynamicallyRelocated : Unable to read memory at Address 0x3
        [+0x003 ( 3: 3)] SkipPatchingUser32Forwarders : Unable to read memory at Address 0x3
        [+0x003 ( 4: 4)] IsPackagedProcess : Unable to read memory at Address 0x3
        [+0x003 ( 5: 5)] IsAppContainer   : Unable to read memory at Address 0x3
        [+0x003 ( 6: 6)] IsProtectedProcessLight : Unable to read memory at Address 0x3
        [+0x003 ( 7: 7)] IsLongPathAwareProcess : Unable to read memory at Address 0x3
        [+0x004] Padding0         [Type: unsigned char [4]]
        [+0x008] Mutant           : Unable to read memory at Address 0x8
        [+0x010] ImageBaseAddress : Unable to read memory at Address 0x10
        [+0x018] Ldr              : Unable to read memory at Address 0x18
        [+0x020] ProcessParameters : Unable to read memory at Address 0x20
        ...
```


## <a name="kernel-iohandles-object"></a>カーネル Io.Handles オブジェクト

カーネル ハンドルの情報を表示するのにには、Io.Handles オブジェクトの現在のプロセスを使用します。

```dbgcmd
0: kd> dx -r1 @$curprocess.Io.Handles
@$curprocess.Io.Handles                
    [0x8]           
    [0xc]           
    [0x10]          
    [0x14]          
    [0x18]       
    ...
```

使用します。最初のハンドルに関する情報を表示する First() 関数。

```dbgcmd
0: kd> dx -r2 @$curprocess.Io.Handles.First()
@$curprocess.Io.Handles.First()                
    Handle           : 0x8
    Type             : Unexpected failure to dereference object
    GrantedAccess    : Unexpected failure to dereference object
    Object           [Type: _OBJECT_HEADER]
        [+0x000] PointerCount     : 228806 [Type: __int64]
        [+0x008] HandleCount      : 6 [Type: __int64]
        [+0x008] NextToFree       : 0x6 [Type: void *]
        [+0x010] Lock             [Type: _EX_PUSH_LOCK]
        [+0x018] TypeIndex        : 0xf2 [Type: unsigned char]
        [+0x019] TraceFlags       : 0x0 [Type: unsigned char]
        [+0x019 ( 0: 0)] DbgRefTrace      : 0x0 [Type: unsigned char]
        [+0x019 ( 1: 1)] DbgTracePermanent : 0x0 [Type: unsigned char]
        [+0x01a] InfoMask         : 0x0 [Type: unsigned char]
        [+0x01b] Flags            : 0x2 [Type: unsigned char]
        [+0x01b ( 0: 0)] NewObject        : 0x0 [Type: unsigned char]
        [+0x01b ( 1: 1)] KernelObject     : 0x1 [Type: unsigned char]
        [+0x01b ( 2: 2)] KernelOnlyAccess : 0x0 [Type: unsigned char]
        [+0x01b ( 3: 3)] ExclusiveObject  : 0x0 [Type: unsigned char]
        [+0x01b ( 4: 4)] PermanentObject  : 0x0 [Type: unsigned char]
        [+0x01b ( 5: 5)] DefaultSecurityQuota : 0x0 [Type: unsigned char]
        [+0x01b ( 6: 6)] SingleHandleEntry : 0x0 [Type: unsigned char]
        [+0x01b ( 7: 7)] DeletedInline    : 0x0 [Type: unsigned char]
        [+0x01c] Reserved         : 0x0 [Type: unsigned long]
        [+0x020] ObjectCreateInfo : 0xfffff801f6d9c6c0 [Type: _OBJECT_CREATE_INFORMATION *]
        [+0x020] QuotaBlockCharged : 0xfffff801f6d9c6c0 [Type: void *]
        [+0x028] SecurityDescriptor : 0xffffb984aa815d06 [Type: void *]
        [+0x030] Body             [Type: _QUAD]
        ObjectType       : Unexpected failure to dereference object
        UnderlyingObject : Unexpected failure to dereference object
```

Io.Handles オブジェクトは、カーネルのみオブジェクトであることに注意してください。


## <a name="working-around-symbol-file-limitations-with-casting"></a>シンボル ファイルの制限事項のキャストを回避します。

さまざまな Windows システム環境変数に関する情報を表示する場合がありますいないすべての型情報が使用可能なパブリック シンボル。 この例では、この状況を示します。

```dbgcmd
0: kd> dx nt!PsIdleProcess
Error: No type (or void) for object at Address 0xfffff800e1d50128
```

Dx コマンドには、型情報がない変数のアドレスを参照する機能がサポートしています。 このような「アドレスの」参照として扱われます"void \*"ようにキャストすることができます。 つまり、データ型がわかっている場合は、次の構文使用できることを変数の型情報を表示します。

```dbgcmd
dx (Datatype *)&VariableName
```

たとえばを nt!Nt のデータ型を含む PsIdleProcess!\_」プロセスでは、次のコマンドを使用します。

```dbgcmd
dx (nt!_EPROCESS *)&nt!PsIdleProcess
(nt!_EPROCESS *)&nt!PsIdleProcess                 : 0xfffff800e1d50128 [Type: _EPROCESS *]
    [+0x000] Pcb              [Type: _KPROCESS]
    [+0x2c8] ProcessLock      [Type: _EX_PUSH_LOCK]
    [+0x2d0] CreateTime       : {4160749568} [Type: _LARGE_INTEGER]
    [+0x2d8] RundownProtect   [Type: _EX_RUNDOWN_REF]
    [+0x2e0] UniqueProcessId  : 0x1000 [Type: void *]
    [+0x2e8] ActiveProcessLinks [Type: _LIST_ENTRY]
    [+0x2f8] Flags2           : 0x218230 [Type: unsigned long]
    [+0x2f8 ( 0: 0)] JobNotReallyActive : 0x0 [Type: unsigned long]
```

Dx コマンドは、@ MASM 構文を使用して、切り替えの式エバリュエーターをサポートしていません。 式エバリュエーターの詳細については、次を参照してください。[を評価する式](evaluating-expressions.md)します。

## <a name="using-linq-with-the-debugger-objects"></a>デバッガー オブジェクトでの LINQ の使用

LINQ 構文は、データを検索および操作デバッガー オブジェクトを使用できます。 LINQ に、構造化照会言語 (SQL) データベースのクエリに使用される概念的に似ています。 さまざまな LINQ メソッドを使用して、検索、フィルター、デバッグ データを解析することができます。 については、デバッガーのオブジェクトと、LINQ を使用して参照してください[デバッガー オブジェクトで LINQ を使用して](using-linq-with-the-debugger-objects.md)します。

## <a name="using-debugger-objects-with-natvis-and-javascript"></a>NatVis および JavaScript でデバッガー オブジェクトの使用

NatVis でデバッガー オブジェクトの使用方法の詳細については、次を参照してください。 [NatVis ネイティブ デバッガー オブジェクト](native-debugger-objects-in-natvis.md)します。

JavaScript でデバッガー オブジェクトの使用方法の詳細については、次を参照してください。 [JavaScript 拡張機能のネイティブ デバッガー オブジェクト](native-objects-in-javascript-extensions.md)します。


## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。

[デバッガー オブジェクトを LINQ で使用します。](using-linq-with-the-debugger-objects.md)

[NatVis でネイティブ デバッガー オブジェクト](native-debugger-objects-in-natvis.md)

[JavaScript の拡張機能のネイティブ デバッガー オブジェクト](native-objects-in-javascript-extensions.md) 

---







