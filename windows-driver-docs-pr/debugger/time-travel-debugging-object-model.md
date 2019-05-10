---
title: Time Travel Debugging - Time Travel Debugging オブジェクトの概要
description: クエリ時にデータ モデルを使用する方法を説明するトレースを移動します。
ms.date: 04/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: be0e207ee0588cc4e4c13fbb173d8c37b44e6a75
ms.sourcegitcommit: 944535d8e00393531f6b265317a64da3567e4f2c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106400"
---
![クロックが表示された短い時間旅行ロゴ](images/ttd-time-travel-debugging-logo.png)

# <a name="introduction-to-time-travel-debugging-objects"></a>オブジェクトのタイム トラベルのデバッグの概要
クエリ時にデータ モデルを使用する方法を説明するトレースを移動します。 これは、タイム トラベルのトレースにキャプチャされるコードの詳細については、上記のような質問に回答する強力なツールです。
* どのような例外は、トレース内にありますか。
* トレース内で時間のどの時点では固有のコード モジュールを読み込むか。
* ときにスレッドを作成/終了したトレースにしますか。
* トレース内の実行時間が最長のスレッドとは

データを追加する TTD 拡張機能は、*セッション*と*プロセス*データ モデル オブジェクト。 TTD データ モデルのオブジェクトを介してアクセスできる、 [dx (表示デバッガー オブジェクト モデルの式)](dx--display-visualizer-variables-.md)コマンド、WinDbg プレビューのモデルの windows で JavaScript とC++します。 タイム トラベルのトレースをデバッグするときに、TTD 拡張機能が自動的に読み込まれます。

## <a name="process-objects"></a>オブジェクトの処理

追加されたプライマリ オブジェクト*プロセス*でオブジェクトが見つかりません、 *TTD*からいずれかの名前空間*プロセス*オブジェクト。 たとえば、`@$curprocess.TTD` と記述します。

```dbgcmd
:000> dx @$curprocess.TTD
@$curprocess.TTD                
    Threads         
    Events          
    Lifetime         : [26:0, 464232:0]
    SetPosition      [Sets the debugger to point to the given position on this process.]
```

LINQ クエリとデバッガー オブジェクトの操作方法の概要については、次を参照してください。[デバッガー オブジェクトで LINQ を使用して](using-linq-with-the-debugger-objects.md)します。

### <a name="properties"></a>プロパティ

| オブジェクト | 説明 |
| --- | --- |
| 有効期間 | A [TTD range オブジェクト](time-travel-debugging-range-objects.md)全体のトレースの有効期間を記述します。 |
| スレッド数 | コレクションを含む[TTD スレッド オブジェクト](time-travel-debugging-thread-objects.md)トレースの有効期間中のすべてのスレッドの 1 つ。 |
| イベント | コレクションを含む[TTD イベント オブジェクト](time-travel-debugging-event-objects.md)トレースにイベントごとに 1 つ。 |

### <a name="methods"></a>メソッド

| メソッド | 説明 |
| --- | --- |
| SetPosition() | 入力として N:N 形式で 0 と 100 または文字列の間の整数を受け取り、その場所にトレースをジャンプします。 参照してください[! tt](time-travel-debugging-extension-tt.md)詳細についてはします。|

## <a name="session-objects"></a>セッション オブジェクト
追加されたプライマリ オブジェクト*セッション*でオブジェクトが見つかりません、 *TTD*からいずれかの名前空間*セッション*オブジェクト。 たとえば、`@$cursession.TTD` と記述します。

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
> 一部のオブジェクトと TTDAnalyze によって追加された拡張機能の内部の関数に使用されるメソッドがあります。 名前空間のすべては記載されていて、現在の名前空間には時間が経ちます。
>

### <a name="methods"></a>メソッド

| メソッド | 説明 |
| --- | --- |
| Data.Heap() | コレクション[オブジェクトのヒープ](time-travel-debugging-heap-objects.md)トレース中に割り当てることができます。 この関数は関数を実行するときにかかるため、計算を行うことに注意してください。|
| Calls() | コレクションを返します[オブジェクトを呼び出す](time-travel-debugging-calls-objects.md)入力文字列に一致します。 入力文字列には、ワイルドカードを含めることができます。 この関数は関数を実行するときにかかるため、計算を行うことに注意してください。  |
| Memory() | これを beginAddress、endAddress および dataAccessMask パラメーターを受け取りのコレクションを返すメソッドは、[メモリ オブジェクト](time-travel-debugging-memory-objects.md)します。 この関数は関数を実行するときにかかるため、計算を行うことに注意してください。  |


## <a name="sorting-query-output"></a>クエリの出力の並べ替え

1 つまたは複数の列で、クエリから返される行の並べ替えに OrderBy() メソッドを使用します。 この例は、TimeStart で昇順に並べ替えます。

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

データ モデル オブジェクトの追加の深さは、r2 の再帰レベルのオプションを表示するには、使用されます。 Dx コマンド オプションに関する詳細については、次を参照してください。 [dx (表示デバッガー オブジェクト モデルの式)](dx--display-visualizer-variables-.md)します。

この例は、TimeStart で降順に並べ替えます。

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

## <a name="specifying-elements-in-a-query"></a>クエリで要素の指定

特定の要素を選択するには、クエリに、さまざまな修飾子を追加できます。 たとえば、クエリには、"kernelbase を含む最初の呼び出しが表示されます。!GetLastError"。

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

## <a name="filtering-in-a-query"></a>クエリでフィルター処理

Select() メソッドを使用して、表示され、列を変更する列の表示名を選択します。

この例では、戻り値がゼロでないと、選択時間とエラーのカスタム表示名を持つ TimeStart と戻り値の列を表示する行を返します。

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

この例のグループの構造化された結果を使用して分析を実行するのにクエリによって返されるデータのエラー番号によって時間位置をグループ化するのにには、GroupBy() メソッドを使用します。

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

## <a name="assigning-result-of-a-query-to-a-variable"></a>クエリの結果を変数に代入

クエリの結果を変数に代入するには、この構文を使用して、 `dx @$var = <expression>`

この例では、クエリの結果を myResults に割り当てます

```dbgcmd
dx -r2 @$myResults = @$cursession.TTD.Calls("kernelbase!GetLastError").Where(c => c.ReturnValue != 0).Select(c => new { Time = c.TimeStart, Error = c.ReturnValue })
```

-G グリッドのオプションを使用して、新しく作成された変数を表示するのにには、dx コマンドを使用します。 Dx コマンドのオプションの詳細については、次を参照してください。 [dx (表示デバッガー オブジェクト モデルの式)](dx--display-visualizer-variables-.md)します。

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

### <a name="querying-for-exceptions"></a>例外のクエリを実行します。

この LINQ クエリを使用して、 [TTD です。イベント オブジェクト](time-travel-debugging-event-objects.md)トレースにすべての例外を表示します。

```dbgcmd
0:000> dx @$curprocess.TTD.Events.Where(t => t.Type == "Exception").Select(e => e.Exception)
@$curprocess.TTD.Events.Where(t => t.Type == "Exception").Select(e => e.Exception)
    [0x0]            : Exception 0x000006BA of type Software at PC: 0X777F51D0
    [0x1]            : Exception 0x000006BA of type Software at PC: 0X777F51D0
    [0x2]            : Exception 0xE06D7363 of type CPlusPlus at PC: 0X777F51D0
```

### <a name="querying-for-specific-api-calls"></a>特定の API 呼び出しのクエリを実行します。

使用[TTD です。呼び出しオブジェクト](time-travel-debugging-calls-objects.md)固有の API 呼び出しを照会します。 呼び出すときに、この例ではエラーが発生しましたが*user32!MessageBoxW*、メッセージ ボックスを表示する Windows API。 関数の開始時刻を並べ替え、および最後の呼び出しを選択し MessageBoxW に対するすべての呼び出しを一覧表示。

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

### <a name="querying-for-the-load-event-of-a-specific-module"></a>特定のモジュールの読み込みイベントのクエリを実行します。

まず、使用して、 [lm (読み込まれたモジュールの一覧)](lm--list-loaded-modules-.md)読み込まれたモジュールを表示するコマンド。

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

Dx の次のコマンドを使用して、トレースには、どのような位置にある特定のモジュールが読み込まれた、ntdll などを参照してください。

```dbgcmd
dx @$curprocess.TTD.Events.Where(t => t.Type == "ModuleLoaded").Where(t => t.Module.Name.Contains("ntdll.dll")) 
@$curprocess.TTD.Events.Where(t => t.Type == "ModuleLoaded").Where(t => t.Module.Name.Contains("ntdll.dll"))                 
    [0x0]            : Module Loaded at position: A:0 
```

この LINQ クエリでは、特定のモジュール読み込みイベントが表示されます。

```dbgcmd
0:000> dx @$curprocess.TTD.Events.Where(t => t.Type == "ModuleUnloaded").Where(t => t.Module.Name.Contains("ntdll.dll")) 
@$curprocess.TTD.Events.Where(t => t.Type == "ModuleUnloaded").Where(t => t.Module.Name.Contains("ntdll.dll"))                 
    [0x0]            : Module Unloaded at position: FFFFFFFFFFFFFFFE:0
```
FFFFFFFFFFFFFFFE:0 のアドレストレースの最後を示します。 



### <a name="querying-for-all-of-the-error-checks-in-the-trace"></a>トレースに、エラーのすべてのクエリを実行するを確認します。

このコマンドを使用して、エラーの数、すべてのトレースのエラー チェックの順に並べ替えます。

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

### <a name="querying-for-the-time-position-in-the-trace-when-threads-were-created"></a>スレッドが作成されたときに、トレースの時間位置のクエリを実行します。

この dx コマンドを使用して、グリッド形式でトレースにすべてのイベントを表示する (-g)。

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

使用して列のいずれかをクリックして、+ 記号を出力を並べ替えます。

スレッドが作成されたときに、時間位置では、トレースで、グリッド形式で表示するには、この LINQ クエリを使用 (型"ThreadCreated"= =)。

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

スレッドが終了したときに、グリッド形式で表示、トレース内に位置する場合は、この LINQ クエリを使用 (型"ThreadTerminated"= =)。

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

### <a name="sorting-output-to-determine-the-longest-running-threads"></a>最長の実行中のスレッドを決定する出力の並べ替え

トレース内の最も長い実行中のスレッドからおおよそグリッド形式で表示するには、この LINQ クエリを使用します。

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

### <a name="querying-for-read-accesses-to-a-memory-range"></a>メモリ範囲への読み取りアクセスに対してクエリを実行します。 

使用して、 [TTD です。メモリ オブジェクト](time-travel-debugging-memory-objects.md)読み取りがメモリの範囲にアクセスするためのクエリにクエリを実行します。

スレッドの状態に関するすべての情報を格納する構造体をスレッド終了) には、結果を含む GetLastError() によって返されます。 実行して、このデータ構造をクエリできます`dx @$teb`現在のスレッド。 TEB のメンバーの 1 つは、サイズが 4 バイト、LastErrorValue 変数です。 この構文を使用して TEB で LastErrorValue メンバーから参照できます。 `dx &@$teb->LastErrorValue` の順にクリックします。

例のクエリがメモリ内には、その範囲内で行うすべての読み取り操作を検索する前に発生するすべての読み取りを選択する方法を示しています、ダイアログ ボックスが作成され、最後の読み取り操作を検索する結果を並べ替えます。

```dbgcmd
0:000> dx @$cursession.TTD.Memory(&@$teb->LastErrorValue, &@$teb->LastErrorValue + 0x4, "r")
@$cursession.TTD.Memory(&@$teb->LastErrorValue, &@$teb->LastErrorValue + 0x4, "r")
    [0x0]           
    [0x1]           
    [0x2]           
    [0x3]     
```

行われた場合、トレースで「ダイアログ」イベントがメモリ内には、その範囲内で行うすべての読み取り操作を検索するクエリを実行できます、ダイアログ ボックスが作成される前に発生し、最後の読み取り操作の検索結果の並べ替えをすべての読み取りを選択します。 結果として得られる時間位置に SeekTo() を呼び出すことによって時間を時間でその時点への移動し。

```dbgcmd

:000> dx @$cursession.TTD.Memory(&@$teb->LastErrorValue, &@$teb->LastErrorValue + 0x4, "r").Where(m => m.TimeStart < @$dialog).OrderBy(m => m.TimeStart).Last().TimeEnd.SeekTo()
Setting position: 458300:37
ModLoad: 6cee0000 6cf5b000   C:\WINDOWS\system32\uxtheme.dll
ModLoad: 75250000 752e6000   C:\WINDOWS\System32\OLEAUT32.dll
ModLoad: 76320000 7645d000   C:\WINDOWS\System32\MSCTF.dll
ModLoad: 76cc0000 76cce000   C:\WINDOWS\System32\MSASN1.dll
```

## <a name="github-ttd-query-lab"></a>GitHub TTD クエリ ラボ

デバッグする方法に関するチュートリアルについてはC++クエリを使用した問題のあるコードの実行に関する情報を問題の検索は、「タイム トラベル デバッグ記録を使用してコード https://github.com/Microsoft/WinDbg-Samples/blob/master/TTDQueries/tutorial-instructions.mdします。

ここで使用可能なすべてのラボで使用するコードが:https://github.com/Microsoft/WinDbg-Samples/tree/master/TTDQueries/app-sampleします。


## <a name="troubleshooting-ttd-queries"></a>TTD クエリのトラブルシューティング

### <a name="unknownormissingsymbols-as-the-function-names"></a>関数名として"UnknownOrMissingSymbols"

データ モデルの拡張機能には、関数名、パラメーター値などを提供するために完全なシンボル情報が必要があります。完全なシンボル情報が利用できない場合、デバッガーは関数名として"UnknownOrMissingSymbols"を使用します。

- プライベート シンボルがある場合、関数名とパラメーターの正しい一覧が表示されます。
- パブリック シンボルがある場合は、関数名および 4 つの符号なし 64 ビット整数のパラメーターの既定のセットを取得します。
- クエリを実行するモジュールのシンボル情報がない場合、"UnknownOrMissingSymbols"は、名前として使用されます。

### <a name="ttd-queries-for-calls"></a>呼び出しの TTD クエリ

クエリは何も返しません DLL への呼び出しに、いくつかの理由があります。

- 適切としたときに、呼び出しの構文はありません。  X のコマンドを使用して呼び出し構文を確認してください。"x <call>"。 X が大文字では、モジュール名がによって返される場合、それを使用します。
- DLL は、されませんがまだ読み込まれてされ、後でトレースに読み込まれます。 DLL が読み込まれた後のポイントにこの移動を回避し、クエリを再実行します。
- 呼び出しはインライン化、クエリ エンジンで追跡することはないです。
- クエリ パターンには、関数が多すぎるを返すワイルドカードが使用されます。  一致した関数の数が十分に小さいように、クエリ パターンを特定してください。

## <a name="see-also"></a>関連項目

[デバッガー オブジェクトを LINQ で使用します。](using-linq-with-the-debugger-objects.md)

[dx (表示デバッガー オブジェクト モデルの式)](dx--display-visualizer-variables-.md)

[旅行時間 - デバッグの概要](time-travel-debugging-overview.md)

[旅行時間 - JavaScript のオートメーションのデバッグ](time-travel-debugging-javascript-automation.md)

---
