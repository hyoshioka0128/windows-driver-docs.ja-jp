---
title: dx (デバッガー オブジェクト モデル式の表示)
description: Dx コマンドは、NatVis 拡張モデルを使用して C++ の式を表示します。 Dx コマンドは、デバッガーオブジェクトで動作します。
ms.assetid: 93047911-5195-4FB9-A015-5349084EDC0A
keywords:
- dx (デバッガーオブジェクトモデル式の表示) Windows デバッグ
ms.date: 05/28/2019
topic_type:
- apiref
api_name:
- dx (Display Debugger Object Model Expression)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1906e00abd0942ef0771ff31c0a3616d4fd38400
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968191"
---
# <a name="dx-display-debugger-object-model-expression"></a>dx (デバッガー オブジェクト モデル式の表示)


**Dx**コマンドは、NatVis 拡張モデルを使用して C++ の式を表示します。 NatVis の詳細については、「[ネイティブオブジェクトのカスタムビューを作成する](https://docs.microsoft.com/visualstudio/debugger/create-custom-views-of-native-objects?view=vs-2015)」を参照してください。

```dbgcmd
dx [-g|-gc #][-c #][-n|-v]-r[#] Expression[,<FormatSpecifier> ]
dx [{-?}|{-h}]
```

## <a name="span-idddk_cmd_display_type_dbgspanspan-idddk_cmd_display_type_dbgspanparameters"></a><span id="ddk_cmd_display_type_dbg"></span><span id="DDK_CMD_DISPLAY_TYPE_DBG"></span>パラメータ


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span>*式*   
表示される C++ 式。

<span id="_______-g______"></span><span id="_______-G______"></span>**-g**   
反復可能なのデータグリッドオブジェクトとして表示します。 反復される各要素はグリッド内の行であり、各子要素の子は列です。 これにより、構造体の配列などを表示できます。各配列要素は行に表示され、構造体の各フィールドは列に表示されます。

(利用可能な DML リンクがある) 列名を左クリックすると、その列で並べ替えられます。 その列によって既に並べ替えられている場合、並べ替え順序は逆になります。

反復可能なされているオブジェクトには、' Display as Grid ' という DML を使用して追加された右クリックコンテキストメニュー項目があります。 出力ウィンドウでオブジェクトを右クリックし、これを選択すると、標準のツリービューではなくグリッドビューにオブジェクトが表示されます。

列名によって表示される (+) は、右クリックと左クリックの両方の動作を提供します。

-   左クリックはその列を受け取り、それを独自のテーブルに分割します。 元の行と展開された列の子が表示されます。
-   右クリックすると、[グリッドに展開] が表示され、列を取得して、右端の列として現在のテーブルに再度追加します。

<span id="_______-gc________"></span><span id="_______-GC________"></span>**-gc \# **   
グリッドとして表示し、グリッドセルのサイズを指定した文字数 () に制限し \# ます。

<span id="_______-c________"></span><span id="_______-C________"></span>**-c \# **   
コンテナーの継続を表示 \# します (コンテナーの要素をスキップします)。このオプションは、通常、カスタム出力の自動化シナリオで使用され、"..." を提供します。リストの下部にある継続要素。

<span id="_______-n______"></span><span id="_______-N______"></span>**-n**   
データを表示する方法は2つあります。 NatVis ビジュアライゼーション (既定値) を使用するか、基になるネイティブ C/c + + 構造体を使用します。 -N パラメーターを指定すると、ネイティブの C/c + + 構造だけを使用して出力がレンダリングされ、NatVis の視覚化は表示されません。

<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
メソッドおよびその他の一般的でないオブジェクトを含む詳細情報を表示します。

<span id="_______-r_______"></span><span id="_______-R_______"></span>**-r**<em>\#</em>   
レベルまでのサブタイプ (フィールド) を再帰的に表示 *\#* します。 *\#* が指定されていない場合、再帰レベル1が既定値になります。

<span id="__________FormatSpecifier_________"></span><span id="__________formatspecifier_________"></span><span id="__________FORMATSPECIFIER_________"></span>** \[ &lt; 、Formatspecifier &gt; \] 子**   
次のいずれかの書式指定子を使用して、既定の表示を変更します。

**, x**:16 進数で序数を表示する

**, d**:10 進数で序数を表示する

**, o**: 序数を8進数で表示する

**, b**: 序数をバイナリで表示する

**, en**: 名前のみで列挙を表示する (値なし)

**, c**: 1 つの文字として表示します (文字列ではありません)

**, s**: 8 ビット文字列を ASCII 引用符で囲んで表示する

**, sb**: 8 ビット文字列を ASCII 引用符で囲まないで表示する

**, s8**: 8 ビット文字列を utf-8 引用符で囲んで表示します。

**, s8b**: 8 ビット文字列を utf-8 引用符で囲まないように表示します。

**, su**:16 ビット文字列を utf-16 引用符として表示します。

**, sub**:16 ビット文字列を utf-16 unqouted として表示します。

**,!**: Raw モードのみでオブジェクトを表示します (例: no NatVis)

**、 \# **: ポインター/配列/コンテナーの長さをリテラル値として指定します \# (数値で置き換えます)

**,\[&lt;&gt;式 \] **: 式の式として、ポインター/配列/コンテナーの長さを指定します &lt;&gt;

**、nd**: オブジェクトの派生 (runtype) 型が見つかりません。 静的な値のみを表示する


<span id="_______dx_-_______"></span><span id="_______DX_-_______"></span>**dx** {**-?**}   
コマンドラインヘルプを表示します。

<span id="_______dx_-h______"></span><span id="_______DX_-H______"></span>**dx** {**-h**}   
デバッガーで使用できるオブジェクトのヘルプを表示します。

<span id="_______dx_-id______"></span><span id="_______DX_-ID______"></span>**dx** {**-id**}   
マイクロソフト内部でのみ使用。 コマンド出力のデータモデルリンクに従うために使用されます。

## <a name="command-line-usage-example"></a>コマンドラインの使用例

[Dx 設定] コマンドを使用すると、デバッグ設定オブジェクトに関する情報を表示できます。 デバッグ設定オブジェクトの詳細については、「[**設定**](-settings--set-debug-settings-.md)」を参照してください。
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

-R1 再帰オプションを使用して、他のデバッガーオブジェクト (セッション、設定、状態) を表示します。

```dbgcmd
kd> dx -r1 Debugger
Debugger : 
  Sessions : 
  Settings : 
  State    : 
```

オブジェクトチェーンをさらに下に移動するには、-r3 再帰オプションを使用して Debugger オブジェクトを指定します。

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

X 書式指定子を追加して、16進数で序数値を表示します。

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

この例では、アクティブなデバッグセッションを使用して、最初のプロセスの最初のスレッドの呼び出し履歴を一覧表示します。

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

出力をデータグリッドとして表示するには、-g オプションを使用します。 並べ替える列をクリックします。

```dbgcmd
kd> dx -g @$curprocess.Modules
```

![表形式のグリッド出力を表示する dx-g @ $curprocess モジュールからの出力](images/dx-grid-example.png)

オブジェクトに関する情報を表示するには、-h オプションを使用します。
```dbgcmd
kd>  dx -h Debugger.State
Debugger.State   [State pertaining to the current execution of the debugger (e.g.: user variables)]
    DebuggerVariables [Debugger variables which are owned by the debugger and can be referenced by a pseudo-register prefix of @$]
    PseudoRegisters   [Categorizied debugger managed pseudo-registers which can be referenced by a pseudo-register prefix of @$]
    UserVariables     [User variables which are maintained by the debugger and can be referenced by a pseudo-register prefix of @$]
```

## <a name="displaying-teb-and-peb-information-using-the-environment-object"></a>環境オブジェクトを使用した TEB および PEB 情報の表示

環境オブジェクトを使用して、スレッドとプロセスに関連付けられている TEB と PEB の情報を表示します。

現在のスレッドに関連付けられている TEB を表示するには、次のコマンドを使用します。

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

現在のプロセスに関連付けられている PEB を表示するには、次のコマンドを使用します。

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


## <a name="kernel-iohandles-object"></a>カーネル Io。ハンドルオブジェクト

現在のプロセスの Io ハンドルオブジェクトを使用して、カーネルハンドル情報を表示します。

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

を使用します。First () 関数は、最初のハンドルに関する情報を表示します。

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

Io ハンドルオブジェクトはカーネルのみのオブジェクトであることに注意してください。


## <a name="working-around-symbol-file-limitations-with-casting"></a>キャストによるシンボルファイルの制限の回避

さまざまな Windows システム変数に関する情報を表示する場合、パブリックシンボルですべての型情報が使用できるとは限りません。 この例では、この状況を示します。

```dbgcmd
0: kd> dx nt!PsIdleProcess
Error: No type (or void) for object at Address 0xfffff800e1d50128
```

Dx コマンドは、型情報を持たない変数のアドレスを参照する機能をサポートしています。 このような "アドレス" 参照は "void" として扱われ、そのように \* キャストできます。 つまり、データ型がわかっている場合は、次の構文を使用して変数の型情報を表示できます。

```dbgcmd
dx (Datatype *)&VariableName
```

たとえば、nt!データ型が nt! \_ の PsIdleProcessEPROCESS、次のコマンドを使用します。

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

Dx コマンドでは、式エバリュエーターの @ @ MASM 構文への切り替えはサポートされていません。 式エバリュエーターの詳細については、「[式の評価](evaluating-expressions.md)」を参照してください。

## <a name="using-linq-with-the-debugger-objects"></a>デバッガー オブジェクトでの LINQ の使用

LINQ 構文をデバッガーオブジェクトと共に使用して、データの検索と操作を行うことができます。 LINQ は、概念的にはデータベースのクエリに使用される構造化照会言語 (SQL) と似ています。 さまざまな LINQ メソッドを使用して、デバッグデータの検索、フィルター処理、および解析を行うことができます。 デバッガーオブジェクトで LINQ を使用する方法については、「[デバッガーオブジェクト](using-linq-with-the-debugger-objects.md)での Linq の使用」を参照してください。

## <a name="using-debugger-objects-with-natvis-and-javascript"></a>NatVis と JavaScript でのデバッガーオブジェクトの使用

NatVis でのデバッガーオブジェクトの使用の詳細については、「 [NatVis のネイティブデバッガーオブジェクト](native-debugger-objects-in-natvis.md)」を参照してください。

JavaScript でのデバッガーオブジェクトの使用の詳細については、「 [Javascript 拡張機能でのネイティブデバッガーオブジェクト](native-objects-in-javascript-extensions.md)」を参照してください。


## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目

[デバッガー オブジェクトでの LINQ の使用](using-linq-with-the-debugger-objects.md)

[NatVis のネイティブ デバッガー オブジェクト](native-debugger-objects-in-natvis.md)

[JavaScript 拡張機能のネイティブ デバッガー オブジェクト](native-objects-in-javascript-extensions.md) 

---







