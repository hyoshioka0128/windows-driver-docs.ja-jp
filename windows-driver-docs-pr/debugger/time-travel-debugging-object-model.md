---
title: タイム トラベル デバッグ - オブジェクトのタイム トラベルのデバッグの概要
description: クエリ時にデータ モデルを使用する方法を説明するトレースを移動します。
ms.date: 12/19/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9089354463db0e453866b25ba6d626b7c33595e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548914"
---
![クロックが表示された短い時間旅行ロゴ](images/ttd-time-travel-debugging-logo.png) 

# <a name="introduction-to-time-travel-debugging-objects"></a>オブジェクトのタイム トラベルのデバッグの概要
クエリ時にデータ モデルを使用する方法を説明するトレースを移動します。 これは、タイム トラベルのトレースにキャプチャされるコードの詳細については、上記のような質問に回答する強力なツールです。
* どのような例外は、トレース内にありますか。
* トレース内で時間のどの時点では固有のコード モジュールを読み込むか。
* ときにスレッドを作成/終了したトレースにしますか。

データを追加する TTD 拡張機能は、*セッション*と*プロセス*データ モデル オブジェクト。 モデル オブジェクトを介してアクセスできる`dx`、WinDbg プレビューのモデルの windows、および JavaScript。 タイム トラベルのトレースをデバッグするときにこれらの拡張機能の両方に自動的に読み込まれます。

## <a name="process-objects"></a>オブジェクトの処理
追加されたプライマリ オブジェクト*プロセス*でオブジェクトが見つかりません、 *TTD*からいずれかの名前空間*プロセス*オブジェクト。 たとえば、`@$curprocess.TTD` と記述します。

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

> [!NOTE]
> 一部のオブジェクトと TTDAnalyze によって追加された拡張機能の内部の関数に使用されるメソッドがあります。 文書化されていないすべての名前空間と現在の名前空間は時間の経過に従って進化します。 
>

### <a name="methods"></a>メソッド

| メソッド | 説明 |
| --- | --- |
| Data.Heap() | コレクション[オブジェクトのヒープ](time-travel-debugging-heap-objects.md)トレース中に割り当てることができます。 この関数は関数を実行するときにかかるため、計算を行うことに注意してください。|
| Calls() | コレクションを返します[オブジェクトを呼び出す](time-travel-debugging-calls-objects.md)入力文字列に一致します。 入力文字列には、ワイルドカードを含めることができます。 この関数は関数を実行するときにかかるため、計算を行うことに注意してください。  |
| Memory() | これを beginAddress、endAddress および dataAccessMask パラメーターを受け取りのコレクションを返すメソッドは、[メモリ オブジェクト](time-travel-debugging-memory-objects.md)します。 この関数は関数を実行するときにかかるため、計算を行うことに注意してください。  |



## <a name="examples"></a>例

### <a name="querying-for-exceptions"></a>例外のクエリを実行します。

この LINQ クエリは、トレース内のすべての例外を表示します。

```dbgcmd
dx @$curprocess.TTD.Events.Where(t => t.Type == "Exception").Select(e => e.Exception) 
```

### <a name="querying-for-the-load-event-of-a-specific-module"></a>特定のモジュールの読み込みイベントのクエリを実行します。

使用して、 [lm (読み込まれたモジュールの一覧)](lm--list-loaded-modules-.md)読み込まれたモジュールを表示するコマンド。

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

Dx の次のコマンドを使用して、特定のモジュールが読み込まれたトレースには、どのような位置にあるを参照してください。

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





## <a name="see-also"></a>参照

[旅行時間 - デバッグの概要](time-travel-debugging-overview.md)

[旅行時間 - JavaScript のオートメーションのデバッグ](time-travel-debugging-javascript-automation.md)

---





