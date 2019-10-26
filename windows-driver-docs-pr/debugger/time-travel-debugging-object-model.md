---
title: Time Travel Debugging - Time Travel Debugging オブジェクトの概要
description: このセクションでは、データモデルを使用してタイムトラベルトレースをクエリする方法について説明します。
ms.date: 04/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 80012c5dc98ad8c049ef18fb53158857ff9c4b2a
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916185"
---
# <a name="introduction-to-time-travel-debugging-objects"></a>タイムトラベルデバッグオブジェクトの概要

![時計を示す短いタイムトラベルロゴ](images/ttd-time-travel-debugging-logo.png)

このセクションでは、データモデルを使用してタイムトラベルトレースをクエリする方法について説明します。 これは、タイムトラベルトレースでキャプチャされたコードに関して、次のような質問に回答するための強力なツールです。
* トレースにはどのような例外がありますか。
* トレースの特定の時点で、特定のコードモジュールが読み込まれました。
* トレースでスレッドを作成または終了したのはいつですか?
* トレースで実行中の最長スレッドは何ですか?

*セッション*および*プロセス*データモデルオブジェクトにデータを追加する TTD 拡張機能があります。 TTD data model オブジェクトには、 [dx (Display Debugger Object Model Expression)](dx--display-visualizer-variables-.md)コマンド、WinDbg Preview のモデルウィンドウ、JavaScript およびをC++使用してアクセスできます。 TTD 拡張機能は、タイムトラベルトレースのデバッグ時に自動的に読み込まれます。

## <a name="process-objects"></a>オブジェクトの処理

*プロセス*オブジェクトに追加されたプライマリオブジェクトは、*プロセス*オブジェクトの*TTD*名前空間にあります。 たとえば、`@$curprocess.TTD` と記述します。

```dbgcmd
:000> dx @$curprocess.TTD
@$curprocess.TTD                
    Threads         
    Events          
    Lifetime         : [26:0, 464232:0]
    SetPosition      [Sets the debugger to point to the given position on this process.]
```

LINQ クエリおよびデバッガーオブジェクトの操作に関する一般的な情報については、「[デバッガーオブジェクトでの linq の使用](using-linq-with-the-debugger-objects.md)」を参照してください。

### <a name="properties"></a>[プロパティ]

| オブジェクト | 説明 |
| --- | --- |
| 最短 | トレース全体の有効期間を記述する[TTD range オブジェクト](time-travel-debugging-range-objects.md)。 |
| スレッド数 | トレースの有効期間全体にわたってスレッドごとに1つずつ、 [TTD thread オブジェクト](time-travel-debugging-thread-objects.md)のコレクションを格納します。 |
| イベント | トレース内のすべてのイベントに対して1つずつ、 [TTD イベントオブジェクト](time-travel-debugging-event-objects.md)のコレクションを格納します。 |

### <a name="methods"></a>メソッド

| メソッド | 説明 |
| --- | --- |
| SetPosition () | 0 ~ 100 の整数、または N:N 形式の文字列を入力として受け取り、トレースをその場所に移動します。 詳細については、「 [! tt](time-travel-debugging-extension-tt.md) 」を参照してください。|

## <a name="session-objects"></a>セッションオブジェクト
*セッション*オブジェクトに追加されたプライマリオブジェクトは、*セッション*オブジェクトの*TTD*名前空間にあります。 たとえば、`@$cursession.TTD` と記述します。

```dbgcmd
0:000> dx @$cursession.TTD
@$cursession.TTD                 : [object Object]
    Calls            [Returns call information from the trace for the specified set of methods: TTD.Calls("module!method1", "module!method2", ...) For example: dx @$cursession.TTD.Calls("user32!SendMessageA")]
    Memory           [Returns memory access information for specified address range: TTD.Memory(startAddress, endAddress [, "rwec"])]
    DefaultParameterCount : 0x4
    AsyncQueryEnabled : false
    Resources       
    Data             : Normalized data sources based on the contents of the time travel trace
    Utility          : Methods that can be useful when analyzing time travel traces
```


> [!NOTE]
> TTDAnalyze によって追加されたオブジェクトとメソッドの中には、拡張機能の内部関数に使用されるものがあります。 すべての名前空間が文書化されているわけではなく、現在の名前空間は時間の経過と共に進化します。
>

### <a name="methods"></a>メソッド

| メソッド | 説明 |
| --- | --- |
| データヒープ () | トレース中に割り当てられた[ヒープオブジェクト](time-travel-debugging-heap-objects.md)のコレクションです。 これは計算を実行する関数であるため、実行には時間がかかります。|
| 呼び出し () | 入力文字列に一致する[呼び出しオブジェクト](time-travel-debugging-calls-objects.md)のコレクションを返します。 入力文字列には、ワイルドカードを含めることができます。 これは計算を実行する関数であるため、実行には時間がかかります。  |
| メモリ () | これは、beginAddress、endAddress、および dataAccessMask パラメーターを受け取り、[メモリオブジェクト](time-travel-debugging-memory-objects.md)のコレクションを返すメソッドです。 これは計算を実行する関数であるため、実行には時間がかかります。  |


## <a name="sorting-query-output"></a>クエリ出力の並べ替え

OrderBy () メソッドを使用して、クエリから返された行を1つ以上の列で並べ替えます。 この例では、TimeStart で昇順に並べ替えます。

```dbgcmd
0:000> dx -r2 @$cursession.TTD.Calls("kernelbase!GetLastError").OrderBy(c => c.TimeStart)
@$cursession.TTD.Calls("kernelbase!GetLastError").OrderBy(c => c.TimeStart)                
    [0xb]           
        EventType        : Call
        ThreadId         : 0x3a10
        UniqueThreadId   : 0x2
        TimeStart        : 39:2DC [Time Travel]
        TimeEnd          : 39:2DF [Time Travel]
        Function         : UnknownOrMissingSymbols
        FunctionAddress  : 0x7561ccc0
        ReturnAddress    : 0x7593d24c
        ReturnValue      : 0x0
        Parameters      
    [0xe]           
        EventType        : Call
        ThreadId         : 0x3a10
        UniqueThreadId   : 0x2
        TimeStart        : AF:36 [Time Travel]
        TimeEnd          : AF:39 [Time Travel]
        Function         : UnknownOrMissingSymbols
        FunctionAddress  : 0x7561ccc0
        ReturnAddress    : 0x4723ef
        ReturnValue      : 0x0
        Parameters  
```

データモデルオブジェクトの詳細を表示するには、-r2 の再帰レベルオプションを使用します。 Dx コマンドオプションの詳細については、「 [dx (デバッガーオブジェクトモデル式の表示)](dx--display-visualizer-variables-.md)」を参照してください。

この例では、TimeStart で降順に並べ替えます。

```dbgcmd
0:000> dx -r2 @$cursession.TTD.Calls("kernelbase!GetLastError").OrderByDescending(c => c.TimeStart)
@$cursession.TTD.Calls("kernelbase!GetLastError").OrderByDescending(c => c.TimeStart)                
    [0x1896]        
        EventType        : Call
        ThreadId         : 0x3a10
        UniqueThreadId   : 0x2
        TimeStart        : 464224:34 [Time Travel]
        TimeEnd          : 464224:37 [Time Travel]
        Function         : UnknownOrMissingSymbols
        FunctionAddress  : 0x7561ccc0
        ReturnAddress    : 0x7594781c
        ReturnValue      : 0x0
        Parameters      
    [0x18a0]        
        EventType        : Call
        ThreadId         : 0x3a10
        UniqueThreadId   : 0x2
        TimeStart        : 464223:21 [Time Travel]
        TimeEnd          : 464223:24 [Time Travel]
        Function         : UnknownOrMissingSymbols
        FunctionAddress  : 0x7561ccc0
        ReturnAddress    : 0x7594781c
        ReturnValue      : 0x0
        Parameters    
```

## <a name="specifying-elements-in-a-query"></a>クエリでの要素の指定

特定の要素を選択するには、さまざまな修飾子をクエリに追加できます。 たとえば、クエリでは、"を含む最初の呼び出しが表示されます。GetLastError "。

```dbgcmd
0:000> dx @$cursession.TTD.Calls("kernelbase!GetLastError").First()
@$cursession.TTD.Calls("kernelbase!GetLastError").First()                
    EventType        : Call
    ThreadId         : 0x3a10
    UniqueThreadId   : 0x2
    TimeStart        : 77A:9 [Time Travel]
    TimeEnd          : 77A:C [Time Travel]
    Function         : UnknownOrMissingSymbols
    FunctionAddress  : 0x7561ccc0
    ReturnAddress    : 0x6cf12406
    ReturnValue      : 0x0
    Parameters    
```

## <a name="filtering-in-a-query"></a>クエリでのフィルター処理

Select () メソッドを使用して、表示する列を選択し、列の表示名を変更します。

この例では、戻り値が0ではない行を返し、TimeStart 列と戻り値の列に Time と Error のカスタム表示名を指定して表示します。

```dbgcmd
0:000> dx -r2 @$cursession.TTD.Calls("kernelbase!GetLastError").Where(c => c.ReturnValue != 0).Select(c => new { Time = c.TimeStart, Error = c.ReturnValue })
@$cursession.TTD.Calls("kernelbase!GetLastError").Where(c => c.ReturnValue != 0).Select(c => new { Time = c.TimeStart, Error = c.ReturnValue })                
    [0x13]          
        Time             : 3C64A:834 [Time Travel]
        Error            : 0x36b7
    [0x1c]          
        Time             : 3B3E7:D6 [Time Travel]
        Error            : 0x3f0
    [0x1d]          
        Time             : 3C666:857 [Time Travel]
        Error            : 0x36b7
    [0x20]          
        Time             : 3C67E:12D [Time Travel]
```

## <a name="grouping"></a>グループ化

GroupBy () メソッドを使用して、クエリによって返されるデータをグループ化し、構造化された結果を使用して分析を実行します。この例では、時間の場所をエラー番号でグループ化します。

```dbgcmd
0:000> dx -r2 @$cursession.TTD.Calls("kernelbase!GetLastError").Where(c => c.ReturnValue != 0).Select(c => new { Time = c.TimeStart, Error = c.ReturnValue }).GroupBy(x => x.Error)
@$s = @$cursession.TTD.Calls("kernelbase!GetLastError").Where(c => c.ReturnValue != 0).Select(c => new { Time = c.TimeStart, Error = c.ReturnValue }).GroupBy(x => x.Error)                
    [0x36b7]        
        [0x0]           
        [0x1]           
        [0x2]           
        [0x3]           
        [...]           
    [0x3f0]         
        [0x0]           
        [0x1]           
        [0x2]           
        [0x3]           
...
```

## <a name="assigning-result-of-a-query-to-a-variable"></a>変数へのクエリの結果の割り当て

この構文を使用して、クエリの結果を変数に割り当て `dx @$var = <expression>`

この例では、クエリの結果を myResults に割り当てます。

```dbgcmd
dx -r2 @$myResults = @$cursession.TTD.Calls("kernelbase!GetLastError").Where(c => c.ReturnValue != 0).Select(c => new { Time = c.TimeStart, Error = c.ReturnValue })
```

-G grid オプションを使用して、新しく作成された変数を表示するには、dx コマンドを使用します。 Dx コマンドオプションの詳細については、「 [dx (デバッガーオブジェクトモデル式の表示)](dx--display-visualizer-variables-.md)」を参照してください。

```dbgcmd
0:000> dx -g @$myResults
========================================
=           = (+) Time     = (+) Error =
========================================
= [0x13]    - 3C64A:834    - 0x36b7    =
= [0x1c]    - 3B3E7:D6     - 0x3f0     =
= [0x1d]    - 3C666:857    - 0x36b7    =
= [0x20]    - 3C67E:12D    - 0x2       =
= [0x21]    - 3C6F1:127    - 0x2       =
= [0x23]    - 3A547:D6     - 0x3f0     =
= [0x24]    - 3A59B:D0     - 0x3f0     =
```


## <a name="examples"></a>例

### <a name="querying-for-exceptions"></a>例外のクエリ

この LINQ クエリでは、TTD を使用し[ます。](time-travel-debugging-event-objects.md)トレース内のすべての例外を表示するイベントオブジェクト。

```dbgcmd
0:000> dx @$curprocess.TTD.Events.Where(t => t.Type == "Exception").Select(e => e.Exception)
@$curprocess.TTD.Events.Where(t => t.Type == "Exception").Select(e => e.Exception)
    [0x0]            : Exception 0x000006BA of type Software at PC: 0X777F51D0
    [0x1]            : Exception 0x000006BA of type Software at PC: 0X777F51D0
    [0x2]            : Exception 0xE06D7363 of type CPlusPlus at PC: 0X777F51D0
```

### <a name="querying-for-specific-api-calls"></a>特定の API 呼び出しのクエリ

TTD を使用[します。](time-travel-debugging-calls-objects.md)特定の API 呼び出しを照会するためにオブジェクトを呼び出します。 この例では、user32.dll! を呼び出すときにエラーが発生しました *。* メッセージボックスを表示するための WINDOWS API である MessageBoxW。 MessageBoxW のすべての呼び出しを一覧表示し、関数の開始時刻で並べ替え、最後の呼び出しを選択します。

```dbgcmd
0:000> dx @$cursession.TTD.Calls("user32!MessageBoxW").OrderBy(c => c.TimeStart).Last()
@$cursession.TTD.Calls("user32!MessageBoxW").OrderBy(c => c.TimeStart).Last()                
    EventType        : Call
    ThreadId         : 0x3a10
    UniqueThreadId   : 0x2
    TimeStart        : 458310:539 [Time Travel]
    TimeEnd          : 45C648:61 [Time Travel]
    Function         : UnknownOrMissingSymbols
    FunctionAddress  : 0x750823a0
    ReturnAddress    : 0x40cb93
    ReturnValue      : 0x10a7000000000001
    Parameters

```

### <a name="querying-for-the-load-event-of-a-specific-module"></a>特定のモジュールの読み込みイベントを照会する

最初に、 [lm (リスト読み込みモジュール)](lm--list-loaded-modules-.md)コマンドを使用して、読み込まれたモジュールを表示します。

```dbgcmd
0:000> lm
start    end        module name
012b0000 012cf000   CDog_Console   (deferred)             
11570000 1158c000   VCRUNTIME140D   (deferred)             
11860000 119d1000   ucrtbased   (deferred)             
119e0000 11b63000   TTDRecordCPU   (deferred)             
11b70000 11cb1000   TTDWriter   (deferred)             
73770000 73803000   apphelp    (deferred)             
73ea0000 74062000   KERNELBASE   (deferred)             
75900000 759d0000   KERNEL32   (deferred)             
77070000 771fe000   ntdll      (private pdb symbols)
```

次に、次の dx コマンドを使用して、特定のモジュールが読み込まれたトレースの位置 (ntdll など) を確認します。

```dbgcmd
dx @$curprocess.TTD.Events.Where(t => t.Type == "ModuleLoaded").Where(t => t.Module.Name.Contains("ntdll.dll")) 
@$curprocess.TTD.Events.Where(t => t.Type == "ModuleLoaded").Where(t => t.Module.Name.Contains("ntdll.dll"))                 
    [0x0]            : Module Loaded at position: A:0 
```

この LINQ クエリは、特定のモジュールの読み込みイベントを表示します。

```dbgcmd
0:000> dx @$curprocess.TTD.Events.Where(t => t.Type == "ModuleUnloaded").Where(t => t.Module.Name.Contains("ntdll.dll")) 
@$curprocess.TTD.Events.Where(t => t.Type == "ModuleUnloaded").Where(t => t.Module.Name.Contains("ntdll.dll"))                 
    [0x0]            : Module Unloaded at position: FFFFFFFFFFFFFFFE:0
```
FFFFFFFFFFFFFFFE のアドレス: 0トレースの終了を示します。 



### <a name="querying-for-all-of-the-error-checks-in-the-trace"></a>トレース内のすべてのエラーチェックを照会する

このコマンドを使用すると、トレース内のエラーチェックのすべてをエラー数で並べ替えることができます。

```dbgcmd
0:000> dx -g @$cursession.TTD.Calls("kernelbase!GetLastError").Where( x=> x.ReturnValue != 0).GroupBy(x => x.ReturnValue).Select(x => new { ErrorNumber = x.First().ReturnValue, ErrorCount = x.Count()}).OrderByDescending(p => p.ErrorCount),d
==================================================
=                 = (+) ErrorNumber = ErrorCount =
==================================================
= [1008]          - 1008            - 8668       =
= [14007]         - 14007           - 4304       =
= [2]             - 2               - 1710       =
= [6]             - 6               - 1151       =
= [1400]          - 1400            - 385        =
= [87]            - 87              - 383        =
```

### <a name="querying-for-the-time-position-in-the-trace-when-threads-were-created"></a>スレッドが作成されたときのトレース内の時間位置を照会する

この dx コマンドを使用して、トレース内のすべてのイベントをグリッド形式 (-g) で表示します。

```dbgcmd
0:000> dx -g @$curprocess.TTD.Events
==================================================================================================================================================================================================
=                                                          = (+) Type            = (+) Position          = (+) Module                                                   = (+) Thread             =
==================================================================================================================================================================================================
= [0x0] : Module Loaded at position: 2:0                   - ModuleLoaded        - 2:0                   - Module C:\Users\USER1\Documents\Visual Studio 2015\Proje... -                        =
= [0x1] : Module Loaded at position: 3:0                   - ModuleLoaded        - 3:0                   - Module C:\WINDOWS\SYSTEM32\VCRUNTIME140D.dll at address 0... -                        =
= [0x2] : Module Loaded at position: 4:0                   - ModuleLoaded        - 4:0                   - Module C:\WINDOWS\SYSTEM32\ucrtbased.dll at address 0X118... -                        =
= [0x3] : Module Loaded at position: 5:0                   - ModuleLoaded        - 5:0                   - Module C:\Users\USER1\AppData\Local\Dbg\UI\Fast.20170907... -                        =
= [0x4] : Module Loaded at position: 6:0                   - ModuleLoaded        - 6:0                   - Module C:\Users\USER1\AppData\Local\Dbg\UI\Fast.20170907... -                        =
= [0x5] : Module Loaded at position: 7:0                   - ModuleLoaded        - 7:0                   - Module C:\WINDOWS\SYSTEM32\apphelp.dll at address 0X73770... -                        =
= [0x6] : Module Loaded at position: 8:0                   - ModuleLoaded        - 8:0                   - Module C:\WINDOWS\System32\KERNELBASE.dll at address 0X73... -                        =
= [0x7] : Module Loaded at position: 9:0                   - ModuleLoaded        - 9:0                   - Module C:\WINDOWS\System32\KERNEL32.DLL at address 0X7590... -                        =
= [0x8] : Module Loaded at position: A:0                   - ModuleLoaded        - A:0                   - Module C:\WINDOWS\SYSTEM32\ntdll.dll at address 0X7707000... -                        =
= [0x9] : Thread created at D:0                            - ThreadCreated       - D:0                   -                                                              - UID: 2, TID: 0x4C2C    =
= [0xa] : Thread terminated at 64:0                        - ThreadTerminated    - 64:0                  -                                                              - UID: 2, TID: 0x4C2C    =
= [0xb] : Thread created at 69:0                           - ThreadCreated       - 69:0                  -                                                              - UID: 3, TID: 0x4CFC    =
= [0xc] : Thread created at 6A:0                           - ThreadCreated       - 6A:0                  -                                                              - UID: 4, TID: 0x27B0    =
= [0xd] : Thread terminated at 89:0                        - ThreadTerminated    - 89:0                  -                                                              - UID: 4, TID: 0x27B0    =
= [0xe] : Thread terminated at 8A:0                        - ThreadTerminated    - 8A:0                  -                                                              - UID: 3, TID: 0x4CFC    =
= [0xf] : Module Unloaded at position: FFFFFFFFFFFFFFFE:0  - ModuleUnloaded      - FFFFFFFFFFFFFFFE:0    - Module C:\Users\USER1\Documents\Visual Studio 2015\Proje... -                        =
= [0x10] : Module Unloaded at position: FFFFFFFFFFFFFFFE:0 - ModuleUnloaded      - FFFFFFFFFFFFFFFE:0    - Module C:\Users\USER1\AppData\Local\Dbg\UI\Fast.20170907... -                        =
= [0x11] : Module Unloaded at position: FFFFFFFFFFFFFFFE:0 - ModuleUnloaded      - FFFFFFFFFFFFFFFE:0    - Module C:\WINDOWS\SYSTEM32\VCRUNTIME140D.dll at address 0... -                        =
= [0x12] : Module Unloaded at position: FFFFFFFFFFFFFFFE:0 - ModuleUnloaded      - FFFFFFFFFFFFFFFE:0    - Module C:\Users\USER1\AppData\Local\Dbg\UI\Fast.20170907... -                        =
= [0x13] : Module Unloaded at position: FFFFFFFFFFFFFFFE:0 - ModuleUnloaded      - FFFFFFFFFFFFFFFE:0    - Module C:\WINDOWS\SYSTEM32\ucrtbased.dll at address 0X118... -                        =
= [0x14] : Module Unloaded at position: FFFFFFFFFFFFFFFE:0 - ModuleUnloaded      - FFFFFFFFFFFFFFFE:0    - Module C:\WINDOWS\SYSTEM32\apphelp.dll at address 0X73770... -                        =
= [0x15] : Module Unloaded at position: FFFFFFFFFFFFFFFE:0 - ModuleUnloaded      - FFFFFFFFFFFFFFFE:0    - Module C:\WINDOWS\System32\KERNELBASE.dll at address 0X73... -                        =
= [0x16] : Module Unloaded at position: FFFFFFFFFFFFFFFE:0 - ModuleUnloaded      - FFFFFFFFFFFFFFFE:0    - Module C:\WINDOWS\System32\KERNEL32.DLL at address 0X7590... -                        =
= [0x17] : Module Unloaded at position: FFFFFFFFFFFFFFFE:0 - ModuleUnloaded      - FFFFFFFFFFFFFFFE:0    - Module C:\WINDOWS\SYSTEM32\ntdll.dll at address 0X7707000... -                        =
==================================================================================================================================================================================================
```

\+ 記号を含む任意の列をクリックすると、出力が並べ替えられます。

この LINQ クエリを使用して、スレッドが作成されたときのトレース内の時間の位置 (型 = = "ThreadCreated") をグリッド形式で表示します。

```dbgcmd
dx -g @$curprocess.TTD.Events.Where(t => t.Type == "ThreadCreated").Select(t => t.Thread) 
===========================================================================================================
=                             = (+) UniqueId = (+) Id    = (+) Lifetime                 = (+) ActiveTime  =
===========================================================================================================
= [0x0] : UID: 2, TID: 0x4C2C - 0x2          - 0x4c2c    - [0:0, FFFFFFFFFFFFFFFE:0]    - [D:0, 64:0]     =
= [0x1] : UID: 3, TID: 0x4CFC - 0x3          - 0x4cfc    - [0:0, 8A:0]                  - [69:0, 8A:0]    =
= [0x2] : UID: 4, TID: 0x27B0 - 0x4          - 0x27b0    - [0:0, 89:0]                  - [6A:0, 89:0]    =
===========================================================================================================
```

この LINQ クエリを使用して、スレッドが終了したときのトレース内の時間の位置 (型 = = "ThreadTerminated") をグリッド形式で表示します。

```dbgcmd
0:000> dx -g @$curprocess.TTD.Events.Where(t => t.Type == "ThreadTerminated").Select(t => t.Thread) 
===========================================================================================================
=                             = (+) UniqueId = (+) Id    = (+) Lifetime                 = (+) ActiveTime  =
===========================================================================================================
= [0x0] : UID: 2, TID: 0x4C2C - 0x2          - 0x4c2c    - [0:0, FFFFFFFFFFFFFFFE:0]    - [D:0, 64:0]     =
= [0x1] : UID: 4, TID: 0x27B0 - 0x4          - 0x27b0    - [0:0, 89:0]                  - [6A:0, 89:0]    =
= [0x2] : UID: 3, TID: 0x4CFC - 0x3          - 0x4cfc    - [0:0, 8A:0]                  - [69:0, 8A:0]    =
===========================================================================================================
```

### <a name="sorting-output-to-determine-the-longest-running-threads"></a>実行時間の長いスレッドを特定するための出力の並べ替え

この LINQ クエリを使用して、トレース内で実行されている実行時間のおおよそのスレッドをグリッド形式で表示します。

```dbgcmd
0:000> dx -g @$curprocess.TTD.Events.Where(e => e.Type == "ThreadTerminated").Select(e => new { Thread = e.Thread, ActiveTimeLength = e.Thread.ActiveTime.MaxPosition.Sequence - e.Thread.ActiveTime.MinPosition.Sequence }).OrderByDescending(t => t.ActiveTimeLength)
=========================================================
=          = (+) Thread              = ActiveTimeLength =
=========================================================
= [0x0]    - UID: 2, TID: 0x1750     - 0x364030         =
= [0x1]    - UID: 3, TID: 0x420C     - 0x360fd4         =
= [0x2]    - UID: 7, TID: 0x352C     - 0x35da46         =
= [0x3]    - UID: 9, TID: 0x39F4     - 0x34a5b5         =
= [0x4]    - UID: 11, TID: 0x4288    - 0x326199         =
= [0x5]    - UID: 13, TID: 0x21C8    - 0x2fa8d8         =
= [0x6]    - UID: 14, TID: 0x2188    - 0x2a03e3         =
= [0x7]    - UID: 15, TID: 0x40E8    - 0x29e7d0         =
= [0x8]    - UID: 16, TID: 0x124     - 0x299677         =
= [0x9]    - UID: 4, TID: 0x2D74     - 0x250f43         =
= [0xa]    - UID: 5, TID: 0x2DC8     - 0x24f921         =
= [0xb]    - UID: 6, TID: 0x3B1C     - 0x24ec8e         =
= [0xc]    - UID: 10, TID: 0x3808    - 0xf916f          =
= [0xd]    - UID: 12, TID: 0x26B8    - 0x1ed3a          =
= [0xe]    - UID: 17, TID: 0x37D8    - 0xc65            =
= [0xf]    - UID: 8, TID: 0x45F8     - 0x1a2            =
=========================================================
```

### <a name="querying-for-read-accesses-to-a-memory-range"></a>メモリ範囲への読み取りアクセスのクエリ 

TTD を使用し[ます。](time-travel-debugging-memory-objects.md)メモリ範囲への読み取りアクセスをクエリするために照会するメモリオブジェクト。

スレッド環境ブロック (TEB) は、GetLastError () によって返される結果を含む、スレッドの状態に関するすべての情報を格納する構造体です。 現在のスレッドに対して `dx @$teb` を実行することで、このデータ構造に対してクエリを実行できます。 TEB のメンバーの1つは LastErrorValue 変数で、サイズは4バイトです。 この構文を使用して、TEB の LastErrorValue メンバーを参照できます。 `dx &@$teb->LastErrorValue`」をご覧ください。

この例のクエリでは、メモリ内のその範囲で実行されたすべての読み取り操作を検索し、ダイアログを作成する前に発生したすべての読み取りを選択して、結果を並べ替えて最後の読み取り操作を検索する方法を示します。

```dbgcmd
0:000> dx @$cursession.TTD.Memory(&@$teb->LastErrorValue, &@$teb->LastErrorValue + 0x4, "r")
@$cursession.TTD.Memory(&@$teb->LastErrorValue, &@$teb->LastErrorValue + 0x4, "r")
    [0x0]           
    [0x1]           
    [0x2]           
    [0x3]     
```

トレースの "dialog" イベントが発生した場合は、クエリを実行してメモリ内のその範囲で実行されたすべての読み取り操作を検索し、ダイアログが作成される前に発生したすべての読み取りを選択して、結果を並べ替えて最後の読み取り操作を検索できます。 次に、結果の時間位置で SeekTo () を呼び出して、その時点までの時間を移動します。

```dbgcmd

:000> dx @$cursession.TTD.Memory(&@$teb->LastErrorValue, &@$teb->LastErrorValue + 0x4, "r").Where(m => m.TimeStart < @$dialog).OrderBy(m => m.TimeStart).Last().TimeEnd.SeekTo()
Setting position: 458300:37
ModLoad: 6cee0000 6cf5b000   C:\WINDOWS\system32\uxtheme.dll
ModLoad: 75250000 752e6000   C:\WINDOWS\System32\OLEAUT32.dll
ModLoad: 76320000 7645d000   C:\WINDOWS\System32\MSCTF.dll
ModLoad: 76cc0000 76cce000   C:\WINDOWS\System32\MSASN1.dll
```

## <a name="github-ttd-query-lab"></a>GitHub TTD クエリラボ

タイムトラベルのデバッグ記録を使用C++してコードをデバッグする方法に関するチュートリアルについては、クエリを使用して問題のあるコードの実行に関する情報を検索する方法については、「 https://github.com/Microsoft/WinDbg-Samples/blob/master/TTDQueries/tutorial-instructions.md 」を参照してください。

ラボで使用されているすべてのコードは、「 https://github.com/Microsoft/WinDbg-Samples/tree/master/TTDQueries/app-sample 」を参照してください。


## <a name="troubleshooting-ttd-queries"></a>TTD クエリのトラブルシューティング

### <a name="unknownormissingsymbols-as-the-function-names"></a>関数名としての "UnknownOrMissingSymbols"

関数名、パラメーター値などを提供するために、データモデル拡張機能には完全なシンボル情報が必要です。シンボルの完全な情報が使用できない場合、デバッガーは関数名として "UnknownOrMissingSymbols" を使用します。

- プライベートシンボルがある場合は、関数名とパラメーターの正しいリストが取得されます。
- パブリックシンボルがある場合は、関数名とパラメーターの既定のセット (4 つの符号なし64ビット整数) が取得されます。
- クエリを実行するモジュールのシンボル情報がない場合は、名前として "UnknownOrMissingSymbols" が使用されます。

### <a name="ttd-queries-for-calls"></a>TTD の呼び出しのクエリ

クエリが DLL の呼び出しに対して何も返さない場合、いくつかの理由が考えられます。

- 呼び出しの構文が正しくありません。  X コマンド: "x <call>" を使用して、呼び出し構文を確認してみてください。 X によって返されたモジュール名が大文字の場合は、それを使用します。
- DLL がまだ読み込まれていないため、後でトレースに読み込まれています。 この問題を回避するには、DLL が読み込まれてから、クエリを再実行します。
- この呼び出しは、クエリエンジンが追跡できないインライン化されています。
- クエリパターンでは、関数を返すワイルドカードを使用します。  一致する関数の数が十分に小さくなるように、クエリパターンをより明確にしてください。

## <a name="see-also"></a>参照

[デバッガーオブジェクトでの LINQ の使用](using-linq-with-the-debugger-objects.md)

[dx (表示デバッガーオブジェクトモデル式)](dx--display-visualizer-variables-.md)

[タイムトラベルのデバッグ-概要](time-travel-debugging-overview.md)

[タイムトラベルデバッグ-JavaScript オートメーション](time-travel-debugging-javascript-automation.md)

---
