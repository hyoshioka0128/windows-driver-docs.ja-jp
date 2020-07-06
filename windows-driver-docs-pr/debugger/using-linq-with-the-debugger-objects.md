---
title: デバッガー オブジェクトでの LINQ の使用
description: デバッガーオブジェクトでの LINQ の使用。 LINQ 構文をデバッガーオブジェクトと共に使用して、データの検索と操作を行うことができます。
keywords:
- デバッガー オブジェクトでの LINQ の使用
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0304df55a8655e4b637af954fb77ffc312e614e4
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968009"
---
# <a name="using-linq-with-the-debugger-objects"></a>デバッガー オブジェクトでの LINQ の使用

LINQ 構文をデバッガーオブジェクトと共に使用して、データの検索と操作を行うことができます。 Dx コマンドで LINQ 構文を使用すると、デバッガーコマンドを使用する場合と比較して、より一貫したエクスペリエンスを実現できます。 出力とオプションは、表示しているデバッガーオブジェクトに関係なく一貫しています。 LINQ クエリでは、"最も多くのスレッドを実行している上位5つのプロセスは何ですか" などの質問をすることができます。

デバッガーオブジェクトは、"デバッガー" で始まる名前空間に投影されます。 プロセス、モジュール、スレッド、スタック、スタックフレーム、およびローカル変数はすべて、LINQ クエリで使用できます。

LINQ は、概念的にはデータベースのクエリに使用される構造化照会言語 (SQL) と似ています。 さまざまな LINQ メソッドを使用して、デバッグデータの検索、フィルター処理、および解析を行うことができます。 LINQ C# メソッドの構文が使用されます。 Linq と LINQ C# の構文の詳細については、「 [C# での linq を使用したはじめに](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/getting-started-with-linq)」を参照してください。

デバッガーのサポートで使用される LINQ では、"クエリ構文" ではなく、LINQ の "メソッド構文" を使用します。 相違点の詳細については、 [「LINQ (統合言語クエリ)](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq)」を参照してください。

デバッガーオブジェクトでは、次のような LINQ コマンドを使用できます。 すべての。任意、。Count,。まずは。を平坦化します。GroupBy,。前の。OrderBy、。OrderByDescending、、、およびを選択します。どこ。 これらのメソッドは、C# の LINQ メソッドの形式に従って (可能な限り近い形で) 続きます。

## <a name="native-debugger-objects"></a>ネイティブデバッガーオブジェクト

ネイティブデバッガーオブジェクトは、デバッガー環境のさまざまな構造と動作を表します。 デバッガーオブジェクトの例を次に示します。

- Session
- スレッド/スレッド
- プロセス/プロセス
- スタックフレーム/スタックフレーム
- ローカル変数
- モジュール/モジュール
- ユーティリティ
- 状態
- 設定

NatVis を使用して、デバッガーオブジェクトを操作することもできます。 詳細については[、「NatVis のネイティブデバッガーオブジェクト](native-debugger-objects-in-natvis.md)」を参照してください。 JavaScript でのデバッガーオブジェクトの使用の詳細については、「 [Javascript 拡張機能でのネイティブデバッガーオブジェクト](native-objects-in-javascript-extensions.md)」を参照してください。 C++ およびドライバーオブジェクトの操作の詳細については、「[デバッガーデータモデル c++ の概要](data-model-cpp-overview.md)」を参照してください。

## <a name="dx-command"></a>Dx コマンド

次に示す例では、dx コマンドを使用します。 dx コマンドの操作の詳細については、「 [dx (Display Debugger Object Model Expression)](dx--display-visualizer-variables-.md)」を参照してください。

## <a name="developing-a-linq-query"></a>LINQ クエリの開発

LINQ デバッガーオブジェクトクエリを開発する方法の1つとして、表示される DML リンクを使用して、データモデルを調べて、クエリで使用されるデバッガーオブジェクトを最初に見つけることができます。

この例では、カーネルデバッグセッションのプロセスの一覧と、各プロセスのスレッド数を表示します。

この調査を開始するには、dx コマンドを使用して最上位レベルのデバッガーオブジェクトを表示します。

```dbgcmd
0: kd> dx Debugger
Debugger
    Sessions
    Settings
    State
    Utility
```

最上位レベルのトピックをクリックすると、セッションが最も興味深いものであると判断されます。そのため、DML リンクをクリックして、*プロセス*が含まれていることを確認します。 

```dbgcmd
0: kd> dx -r1 Debugger.Sessions[0]
Debugger.Sessions[0]                 : Remote KD: KdSrv:Server=@{<Local>},Trans=@{NET:Port=50005,Key=MyKey}
    Processes
    Id               : 0
    Attributes
```

次に、[詳細] をクリックして特定のプロセスを確認すると、そのプロセスに関連付けられている*スレッド*が使用可能になっていることがわかります。 いずれかのプロセスの [*スレッド*] をクリックすると、そのプロセスに関連付けられているすべてのスレッドが使用可能になります。


```dbgcmd
0: kd> dx -r1 Debugger.Sessions[0].Processes[1428].Threads
Debugger.Sessions[0].Processes[1428].Threads
    [0x598]          : <Unable to get stack trace> [Switch To]
    [0x1220]         : <Unable to get stack trace> [Switch To]
    [0x6f8]          : nt!KiSwapContext+0x76 (fffff806`4466a186)  [Switch To]
    [0x128c]         : <Unable to get stack trace> [Switch To]
    [0x27e4]         : nt!KiSwapContext+0x76 (fffff806`4466a186)  [Switch To] 
```

プロセスに関連付けられているスレッドの数を表示するために必要なデータが、デバッガーオブジェクトモデルで利用できることがわかりました。

LINQ クエリを少し短くするには、このトピックの後半で説明する[システム定義変数](#system-defined-variables)を使用して、現在のセッションに関連付けられているプロセスを表示します。

```dbgcmd
0: kd> dx @$cursession.Processes
@$cursession.Processes                
    [0x0]            : Idle [Switch To]
    [0x4]            : System [Switch To]
    [0x90]           : Registry [Switch To]
...
```

次に、select ステートメントを追加します。 まず、名前フィールドを指定できます。

```dbgcmd
0: kd> dx @$cursession.Processes.Select(p => p.Name)
@$cursession.Processes.Select(p => p.Name)                
    [0x0]            : Idle
    [0x4]            : System
    [0x90]           : Registry
...
```

このシナリオでは、スレッドの数も必要です。 2つのフィールドがあるため、「[ユーザー定義変数](#user-defined-variables)」で説明されている C# の匿名型の構文と同様に、 *new*を使用して匿名型を作成します。

```dbgcmd
dx @$cursession.Processes.Select(p => new {Name = p.Name, Threads = p.Threads})
```

このコマンドを使用すると、"dx" は実際に名前を出力しなくなります。そのため、名前とスレッドを表示するには、-r2 を追加します (2 つのレベルを再帰します)。

```dbgcmd
dx -r2 @$cursession.Processes.Select(p => new {Name = p.Name, Threads = p.Threads})
@$cursession.Processes.Select(p => new {Name = p.Name, Threads = p.Threads})                
    [0x0]           
        Name             : Idle
        Threads         
    [0x4]           
        Name             : System
        Threads         
    [0x90]          
        Name             : Registry
        Threads       
```

この時点で、プロセスの名前とスレッドの一覧が表示されます。 ThreadCount を表示するには、を使用し*ます。Count ()* メソッド。


```dbgcmd
0: kd> dx -r2 @$cursession.Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count()})
@$cursession.Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count()})                
    [0x0]           
        Name             : Idle
        ThreadCount      : 0x4
    [0x4]           
        Name             : System
        ThreadCount      : 0xe7
    [0x90]          
        Name             : Registry
        ThreadCount      : 0x4
...
```

スレッドの数が多いプロセスを確認するには、 *OrderByDescending*を使用して、スレッド数で一覧を並べ替えます。

```dbgcmd
0: kd> dx -r2 @$cursession.Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count()}).OrderByDescending(p => p.ThreadCount)
@$cursession.Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count()}).OrderByDescending(p => p.ThreadCount)                
    [0x4]           
        Name             : System
        ThreadCount      : 0xe7
    [0xa38]         
        Name             : svchost.exe
        ThreadCount      : 0x45
    [0x884]         
        Name             : MemCompression
        ThreadCount      : 0x3e
```

 書式設定されたグリッドでレンダリングするには、'-r2 ' を '-g ' に変更します。 [グリッド] オプションでは列が適切に表示されるため、再帰のレベルを指定する必要はありません。 最後に、", d" 書式指定子を追加して、10進値を出力します。

```dbgcmd
0: kd> dx -g @$cursession.Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count()}).OrderByDescending(p => p.ThreadCount),d
===========================================================================================
=            = Name                                                         = ThreadCount =
===========================================================================================
= [4]        - System                                                       - 231         =
= [2616]     - svchost.exe                                                  - 69          =
= [2180]     - MemCompression                                               - 62          =
= [968]      - explorer.exe                                                 - 61          =
```

## <a name="debugger-objects-examples"></a>デバッガーオブジェクトの例

この例は、最も多くのスレッドを実行する上位5つのプロセスを示しています。

```dbgcmd
0: kd> dx -r2 Debugger.Sessions.First().Processes.Select(p => new { Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.ThreadCount),5
Debugger.Sessions.First().Processes.Select(p => new { Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.ThreadCount),5 

: 
    [0x4]            : 
        Name             : <Unknown Image>
        ThreadCount      : 0x73
    [0x708]          : 
        Name             : explorer.exe
        ThreadCount      : 0x2d
    [0x37c]          : 
        Name             : svchost.exe
        ThreadCount      : 0x2c
    [0x6b0]          : 
        Name             : MsMpEng.exe
        ThreadCount      : 0x22
    [0x57c]          : 
        Name             : svchost.exe
        ThreadCount      : 0x15
    [...]       
```

この例では、プラグアンドプレイデバイスツリー内のデバイスを、物理デバイスオブジェクトのドライバーの名前でグループ化して示します。 すべての出力が表示されるわけではありません。

```dbgcmd
kd> dx -r2 Debugger.Sessions.First().Devices.DeviceTree.Flatten(n => n.Children).GroupBy(n => n.PhysicalDeviceObject->Driver->DriverName.ToDisplayString())
Debugger.Sessions.First().Devices.DeviceTree.Flatten(n => n.Children).GroupBy(n => n.PhysicalDeviceObject->Driver->DriverName.ToDisplayString()) 

: 
    ["\"\\Driver\\PnpManager\""] : 
        [0x0]            : HTREE\ROOT\0
        [0x1]            : ROOT\volmgr\0000 (volmgr)
        [0x2]            : ROOT\BasicDisplay\0000 (BasicDisplay)
        [0x3]            : ROOT\CompositeBus\0000 (CompositeBus)
        [0x4]            : ROOT\vdrvroot\0000 (vdrvroot)
         ...  
```

## <a name="dx-command-tab-auto-completion"></a>[Dx コマンド] タブのオートコンプリート

コンテキストタブのキーオートコンプリートは、LINQ クエリメソッドを認識し、ラムダのパラメーターに対して機能します。

例として、次のテキストをデバッガーに入力します (またはコピーして貼り付けます)。 次に、TAB キーを何度か押して、候補の候補を順番に切り替えます。

```dbgcmd
dx -r2 Debugger.Sessions.First().Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.
```

TAB キーを押します。Name "が表示されます。 終わりかっこ ")" を追加し、enter キーを押してコマンドを実行します。

```dbgcmd
kd> dx -r2 Debugger.Sessions.First().Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.Name)
Debugger.Sessions.First().Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.Name) : 
    [0x274]          : 
        Name             : winlogon.exe
        ThreadCount      : 0x4
    [0x204]          : 
        Name             : wininit.exe
        ThreadCount      : 0x2
    [0x6c4]          : 
        Name             : taskhostex.exe
        ThreadCount      : 0x8
         ...  
```

この例では、キー比較子メソッドを使用した完了を示します。 キーが文字列であるため、置換によって文字列メソッドが表示されます。

```dbgcmd
dx -r2 Debugger.Sessions.First().Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.Name, (a, b) => a.
```

TAB キーを押します。[長さ] が表示されます。 終わりかっこ ")" を追加し、enter キーを押してコマンドを実行します。

```dbgcmd
kd> dx -r2 Debugger.Sessions.First().Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.Name, (a, b) => a.Length)
Debugger.Sessions.First().Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.Name, (a, b) => a.Length) : 
    [0x544]          : 
        Name             : spoolsv.exe
        ThreadCount      : 0xc
    [0x4d4]          : 
        Name             : svchost.exe
        ThreadCount      : 0xa
    [0x438]          : 
        Name             : svchost.exe
```

## <a name="user-defined-variables"></a>ユーザー定義変数

変数名の前に @ $ を付けることで、ユーザー定義変数を定義できます。 ユーザー定義変数は、ラムダ、LINQ クエリの結果など、どのような dx でも使用できる任意のものに割り当てることができます。

このようなユーザー変数の値を作成および設定できます。

```dbgcmd
kd> dx @$String1="Test String"
```

定義されたユーザー変数は、 *Debugger. uservariables*または *@ $vars*を使用して表示できます。

```dbgcmd
kd> dx Debugger.State.UserVariables
Debugger.State.UserVariables : 
    mySessionVar     : 
    String1          : Test String
```

を使用して変数を削除できます。から.

```dbgcmd
kd> dx @$vars.Remove("String1")
```

この例では、Sesssions を参照するユーザー変数を定義する方法を示します。

```dbgcmd
kd> dx @$mySessionVar = Debugger.Sessions
```

次に示すように、ユーザー定義変数を使用できます。

```dbgcmd
kd> dx -r2 @$mySessionVar 
@$mySessionVar   : 
    [0x0]            : Remote KD: KdSrv:Server=@{<Local>},Trans=@{COM:Port=\\.\com3,Baud=115200,Timeout=4000}
        Processes        : 
        Devices     
```
## <a name="system-defined-variables"></a>システム定義変数

次のシステム定義変数は、任意の LINQ dx クエリで使用できます。

-   @ $cursession-現在のセッション

-   @ $curprocess-現在のプロセス

-   @ $curthread-現在のスレッド

この例では、システム定義変数の使用方法を示します。

```dbgcmd
kd> dx @$curprocess.Threads.Count()
@$curprocess.Threads.Count() : 0x4
```

```dbgcmd
kd> dx -r1 @$curprocess.Threads
@$curprocess.Threads : 
    [0x4adc]         : 
    [0x1ee8]         : 
    [0x51c8]         : 
    [0x62d8]         : 
     ...
```

## <a name="user-defined-variables---anonymous-types"></a>ユーザー定義変数-匿名型

この動的オブジェクトの作成は、C# の匿名型の構文 (new {...}) を使用して行われます。 詳細については、「匿名型について」を参照してください。「[匿名型 (C# プログラミングガイド)](https://docs.microsoft.com/dotnet/articles/csharp/programming-guide/classes-and-structs/anonymous-types)」を参照してください。 この例では、整数と文字列値を使用して匿名型を作成します。

```dbgcmd
kd> dx -r1 new { MyInt = 42, MyString = "Hello World" }
new { MyInt = 42, MyString = "Hello World" } : 
    MyInt            : 42
    MyString         : Hello World
```


## <a name="function-objects-lambda-expressions"></a>関数オブジェクト (ラムダ式)

データのクエリに使用されるメソッドの多くは、ユーザーが指定した関数をコレクション内のオブジェクト間で繰り返し実行するという概念に基づいています。 デバッガーでデータを照会して操作する機能をサポートするために、dx コマンドでは、同等の C# 構文を使用したラムダ式がサポートされています。 ラムダ式は、= 演算子の使用によって次のように定義され &gt; ます。

(引数) = &gt; (result)

Dx で LINQ を使用する方法については、この簡単な例で5と7を加算してみてください。

```dbgcmd
kd> dx ((x, y) => (x + y))(5, 7) 
```

Dx コマンドは、ラムダ式を表示し、結果として12を表示します。

```dbgcmd
((x, y) => (x + y))(5, 7)  : 12
```

この例のラムダ式では、文字列 "Hello" と "World" を組み合わせています。

```dbgcmd
kd> dx ((x, y) => (x + y))("Hello", "World")
((x, y) => (x + y))("Hello", "World") : HelloWorld
```


## <a name="supported-linq-syntax---query-methods"></a>サポートされている LINQ 構文-クエリメソッド

Dx が反復可能なとして定義する任意のオブジェクト (ネイティブ配列、NatVis をコンテナーとして記述した型、またはデバッガー拡張オブジェクト) には、一連の LINQ (または LINQ に相当する) メソッドが射影されています。 これらのクエリメソッドについて以下に説明します。 クエリメソッドの引数のシグネチャは、すべてのクエリメソッドの後に一覧表示されます。

フィルター処理メソッド

**.Where (PredicateMethod)**: 述語メソッドが true を返した入力コレクション内のすべてのオブジェクトを含むオブジェクトの新しいコレクションを返します。




射影メソッド

**.平坦化 ( \[ keyprojectormethod \] )**: コンテナー (ツリー) の入力コンテナーを取得し、それをツリー内のすべての要素を持つ1つのコンテナーに平坦化します。 オプションのキープロジェクターメソッドが指定されている場合、ツリーは、それ自体がコンテナーであるキーのコンテナーと見なされます。これらのキーは、射影メソッドの呼び出しによって決定されます。

**.Select (KeyProjectorMethod)**: 入力コレクション内のすべてのオブジェクトに対してプロジェクターメソッドを呼び出した結果を格納しているオブジェクトの新しいコレクションを返します。




グループ化メソッド

**.GroupBy (KeyKeyComparatorMethod Tormethod, \[ \] )**: キープロジェクターメソッドを呼び出すことによって決定されたのと同じキーを持つ入力コレクション内のすべてのオブジェクトをグループ化することにより、コレクションの新しいコレクションを返します。 オプションの比較子メソッドを指定できます。

**Join (InnerCollection、Outer key selector メソッド、内部キーセレクターメソッド、 \[ ComparatorMethod \] )**: キーセレクター関数に基づいて2つのシーケンスを結合し、値のペアを抽出します。 オプションの比較子メソッドを指定することもできます。

**Intersect (InnerCollection, \[ ComparatorMethod \] )**: 積集合を返します。これは、2つのコレクションのそれぞれに出現する要素を意味します。 オプションの比較子メソッドを指定することもできます。

**Union (InnerCollection, \[ ComparatorMethod \] )**: 和集合を返します。これは、2つのコレクションのいずれかに出現する一意の要素を意味します。 オプションの比較子メソッドを指定することもできます。




データセットのメソッド

**Contains (Object, \[ ComparatorMethod \] )**: 指定された要素がシーケンスに含まれるかどうかを判断します。 要素がシーケンス内のエントリと比較されるたびに呼び出されるオプションの比較メソッドを指定できます。

**Distinct ( \[ ComparatorMethod \] )**: コレクションから重複する値を削除します。 コレクション内のオブジェクトを比較する必要があるたびに、オプションの比較メソッドを呼び出して呼び出すことができます。

**Except (InnerCollection, \[ ComparatorMethod \] )**: セットの差を返します。これは、2番目のコレクションに表示されない1つのコレクションの要素を意味します。 オプションの比較子メソッドを指定できます。

**Concat (InnerCollection)**: 2 つのシーケンスを連結して1つのシーケンスを形成します。




並べ替えメソッド

**.OrderBy (KeyKeyComparatorMethod Tormethod, \[ \] )**: 入力コレクション内の各オブジェクトに対してキープロジェクションメソッドを呼び出すことによって提供されるキーに従って、コレクションを昇順に並べ替えます。 オプションの比較子メソッドを指定できます。

**.OrderByDescending (レジストリ tormethod, \[ KeyComparatorMethod \] )**: 入力コレクション内の各オブジェクトに対してキープロジェクションメソッドを呼び出すことによって提供されるキーに従って、コレクションを降順に並べ替えます。 オプションの比較子メソッドを指定できます。




集計メソッド

**Count ()**: コレクション内の要素の数を返すメソッド。

**Sum ( \[ ProjectionMethod \] )**: コレクション内の値の合計を計算します。 必要に応じて、合計が発生する前に要素を変換するためのプロジェクターメソッドを指定できます。




Skip メソッド

**Skip (Count)**: シーケンス内の指定された位置までの要素をスキップします。

**Skipwhile (PredicateMethod)**: 要素が条件を満たさない限り、述語関数に基づいて要素をスキップします。




Take メソッド

**Take (Count)**: シーケンス内の指定された位置までの要素を取得します。

**PredicateMethod (関数)**: 要素が条件を満たさない場合、述語関数に基づいて要素を取得します。




比較メソッド

**Sequenceequal (InnerCollection, \[ ComparatorMethod \] )**: ペアで要素を比較することによって、2つのシーケンスが等しいかどうかを判断します。 オプションの比較子を指定できます。




エラー処理メソッド

**Allnonerror (PredicateMethod)**: コレクションのすべてのエラー以外の要素が特定の条件を満たしているかどうかを返します。

**Firstnonerror ( \[ PredicateMethod \] )**: エラーではないコレクションの最初の要素を返します。

**Lastnonerror ( \[ PredicateMethod \] )**: エラーではないコレクションの最後の要素を返します。




その他の方法

**.All (PredicateMethod)**: 入力コレクション内のすべての要素に対して指定された述語メソッドを呼び出した結果が true であるかどうかを返します。

**.Any (PredicateMethod)**: 入力コレクション内の任意の要素に対して指定された述語メソッドを呼び出した結果が true であるかどうかを返します。

**.First ( \[ PredicateMethod \] )**: コレクション内の最初の要素を返します。 省略可能な述語が渡された場合、は、述語への呼び出しが true を返すコレクション内の最初の要素を返します。

**.Last ( \[ PredicateMethod \] )**: コレクション内の最後の要素を返します。 省略可能な述語が渡された場合、は、述語への呼び出しが true を返すコレクション内の最後の要素を返します。

**Min ( \[ keyprojectormethod \] )**: コレクションの最小要素を返します。 オプションのプロジェクターメソッドを指定して、他のメソッドと比較する前に各メソッドを射影することができます。

**Max ( \[ keyprojectormethod \] )**: コレクションの最大要素を返します。 オプションのプロジェクターメソッドを指定して、他のメソッドと比較する前に各メソッドを射影することができます。

**Single ( \[ PredicateMethod \] )**: リストから唯一の要素を返します (コレクションに複数の要素が含まれている場合はエラー)。 述語が指定されている場合、は、その述語を満たす1つの要素を返します (複数の要素がそれを満たす場合、関数は代わりにエラーを返します)。




**引数のシグニチャ**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">KeyProjectorMethod: (obj = &gt; 任意のキー)</td>
<td align="left">コレクションのオブジェクトを取得し、そのオブジェクトからキーを返します。</td>
</tr>
<tr class="even">
<td align="left">KeyComparatorMethod: ((a, b) = &gt; 整数値)</td>
<td align="left">2つのキーを受け取り、それを返します。
<p>(a b) の場合は-1 &lt;</p>
<p>0の場合は 0 (a = = b)</p>
<p>(a b) の場合は 1 &gt;</p></td>
</tr>
<tr class="odd">
<td align="left">PredicateMethod: (obj = &gt; ブール値)</td>
<td align="left">コレクションのオブジェクトを受け取り、そのオブジェクトが特定の条件を満たしているかどうかに基づいて true または false を返します。</td>
</tr>
</tbody>
</table>



## <a name="supported-linq-syntax---string-manipulation"></a>サポートされている LINQ 構文文字列操作

すべての string オブジェクトには、次のメソッドが射影されており、使用できるようになっています。

関連するメソッド & プロパティにクエリを実行する

**.Contains (OtherString)**: 入力文字列に OtherString が含まれているかどうかを示すブール値を返します。

**.EndsWith (OtherString)**: 入力文字列が otherstring で終わるかどうかを示すブール値を返します。

**Length**: 文字列の長さを返すプロパティ。

**.StartsWith (OtherString)**: 入力文字列が otherstring で始まるかどうかを示すブール値を返します。

**.Substring (StartPos, \[ Length \] )**: 入力文字列内の指定した開始位置から始まる部分文字列を返します。 省略可能な長さを指定した場合、返される部分文字列は、指定された長さになります。それ以外の場合は、文字列の末尾に入ります。




その他の方法

**.IndexOf (OtherString)**: 入力文字列内で最初に出現する OtherString のインデックスを返します。

**.LastIndexOf (OtherString)**: 入力文字列内で最後に出現する OtherString のインデックスを返します。




書式設定メソッド

**.PadLeft (TotalWidth)**: 文字列の長さの合計を指定された幅にするために、必要に応じて文字列の左側にスペースを追加します。

**.PadRight (TotalWidth)**: 文字列の長さの合計を指定された幅にするために、必要に応じて文字列の右側にスペースを追加します。

**.Remove (StartPos, \[ Length \] )**: 入力文字列の指定した開始位置から文字を削除します。 省略可能な長さのパラメーターを指定すると、その文字数が削除されます。それ以外の場合は、文字列の末尾までのすべての文字が削除されます。

**.Replace (SearchString, ReplaceString)**: 入力文字列内に出現するすべての SearchString を、指定された replacestring に置き換えます。




文字列オブジェクトのプロジェクション

文字列オブジェクトに直接射影されるメソッドに加えて、文字列変換を含むすべてのオブジェクトは、次のメソッドを射影して、そのメソッドを使用できるようにします。

**.ToDisplayString ()**: オブジェクトの文字列変換を返します。 これは、オブジェクトの dx 呼び出しで表示される文字列変換です。 書式指定子を指定して、ToDisplayString の出力を書式設定することができます。 詳細については、「 [Visual Studio デバッガーでの C++ の書式指定子](https://docs.microsoft.com/visualstudio/debugger/format-specifiers-in-cpp?view=vs-2019)」を参照してください。




次の例は、書式指定子の使用方法を示しています。

```dbgcmd
kd> dx (10).ToDisplayString("d")
(10).ToDisplayString("d") : 10

kd> dx (10).ToDisplayString("x")
(10).ToDisplayString("x") : 0xa

kd> dx (10).ToDisplayString("o")
(10).ToDisplayString("o") : 012

kd> dx (10).ToDisplayString("b") 
(10).ToDisplayString("b")  : 0y1010

kd> dx ("some wchar string here").ToDisplayString("su") 
("some wchar string here").ToDisplayString("su")  : "some wchar string here"

kd> dx ("some wchar string here").ToDisplayString("sub") 
("some wchar string here").ToDisplayString("sub")  : some wchar string here

```

## <a name="span-iddebugging_plug_and_playspanspan-iddebugging_plug_and_playspanspan-iddebugging_plug_and_playspandebugging-plug-and-play-example"></a><span id="Debugging_Plug_and_Play"></span><span id="debugging_plug_and_play"></span><span id="DEBUGGING_PLUG_AND_PLAY"></span>デバッグプラグアンドプレイの例


ここでは、LINQ クエリで使用される組み込みのデバッガーオブジェクトを使用して、プラグアンドプレイオブジェクトをデバッグする方法について説明します。

**すべてのデバイスを表示する**

デバイスツリーで*フラット*化を使用して、すべてのデバイスを表示します。 

```dbgcmd
 1: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children)                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ROOT\volmgr\0000 (volmgr)
    [0x2]            : ROOT\BasicDisplay\0000 (BasicDisplay)
    [0x3]            : ROOT\CompositeBus\0000 (CompositeBus)
    [0x4]            : ROOT\vdrvroot\0000 (vdrvroot)
    [0x5]            : ROOT\spaceport\0000 (spaceport)
    [0x6]            : ROOT\KDNIC\0000 (kdnic)
    [0x7]            : ROOT\UMBUS\0000 (umbus)
    [0x8]            : ROOT\ACPI_HAL\0000
...
```

**グリッドの表示**

他の dx コマンドと同様に、実行したコマンドを右クリックし、[グリッドとして表示] をクリックするか、コマンドに "-g" を追加して結果のグリッドビューを取得します。

```dbgcmd
# 0: kd> dx -g @$cursession.Devices.DeviceTree.Flatten(n => n.Children)
=====================================================================================================================================================================================================================================================================================================================
# =                                                              = (+) DeviceNodeObject = InstancePath                                                 = ServiceName               = (+) PhysicalDeviceObject                                    = State                          = (+) Resoures = (+) Children       =
=====================================================================================================================================================================================================================================================================================================================
= [0x0] : HTREE\ROOT\0                                         - {...}                - HTREE\ROOT\0                                                 -                           - 0xffffb6075614be40 : Device for "\Driver\PnpManager"        - DeviceNodeStarted (776)        - {...}        - [object Object]    =
= [0x1] : ROOT\volmgr\0000 (volmgr)                            - {...}                - ROOT\volmgr\0000                                             - volmgr                    - 0xffffb607561fbe40 : Device for "\Driver\PnpManager"        - DeviceNodeStarted (776)        - {...}        - [object Object]    =
= [0x2] : ROOT\BasicDisplay\0000 (BasicDisplay)                - {...}                - ROOT\BasicDisplay\0000                                       - BasicDisplay              - 0xffffb607560739b0 : Device for "\Driver\PnpManager"        - DeviceNodeStarted (776)        - {...}        - [object Object]    =
= [0x3] : ROOT\CompositeBus\0000 (CompositeBus)                - {...}                - ROOT\CompositeBus\0000                                       - CompositeBus              - 0xffffb607561f9060 : Device for "\Driver\PnpManager"        - DeviceNodeStarted (776)        - {...}        - [object Object]    =
...
```

**状態別のデバイスの表示**

特定のデバイスの状態を指定するには、 *Where*を使用します。

```dbgcmd
dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.State <operator> <state number>)
```

たとえば、状態が Devicのデバイスを表示するには、次のコマンドを使用します。

```dbgcmd
1: kd>  dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.State == 776)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.State == 776)                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ROOT\volmgr\0000 (volmgr)
    [0x2]            : ROOT\BasicDisplay\0000 (BasicDisplay)
    [0x3]            : ROOT\CompositeBus\0000 (CompositeBus)
    [0x4]            : ROOT\vdrvroot\0000 (vdrvroot)
...
```

**未開始のデバイスの表示**

このコマンドを使用すると、状態が Devicではないデバイスを表示できます。

```dbgcmd
1: kd>  dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.State != 776)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.State != 776)                
    [0x0]            : ACPI\PNP0C01\1
    [0x1]            : ACPI\PNP0000\4&215d0f95&0
    [0x2]            : ACPI\PNP0200\4&215d0f95&0
    [0x3]            : ACPI\PNP0100\4&215d0f95&0
    [0x4]            : ACPI\PNP0800\4&215d0f95&0
    [0x5]            : ACPI\PNP0C04\4&215d0f95&0
    [0x6]            : ACPI\PNP0700\4&215d0f95&0 (fdc)
    [0x7]            : ACPI\PNP0C02\1
    [0x8]            : ACPI\PNP0C02\2
```

**問題コード別のデバイスの表示**

特定の問題コードを持つデバイスを表示するには、 *devicの*オブジェクトを使用します。

```dbgcmd
dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem <operator> <problemCode>)
```

たとえば、問題がゼロではないデバイスを表示するには、次のコマンドを使用します。 これにより、"[**! devnode**](-devnode.md) 0 21" と同様の情報が得られます。

```dbgcmd
1: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem != 0)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem != 0)                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ACPI\PNP0700\4&215d0f95&0 (fdc)
```

**問題のないすべてのデバイスを表示する**

このコマンドを使用して、問題のないすべてのデバイスを表示します。

```dbgcmd
1: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem == 0)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem == 0)                
    [0x0]            : ROOT\volmgr\0000 (volmgr)
    [0x1]            : ROOT\BasicDisplay\0000 (BasicDisplay)
    [0x2]            : ROOT\CompositeBus\0000 (CompositeBus)
    [0x3]            : ROOT\vdrvroot\0000 (vdrvroot)
...
```

**特定の問題が発生しているすべてのデバイスを表示する**

このコマンドを使用して、0x16 の問題の状態にあるデバイスを表示します。

```dbgcmd
1: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem == 0x16)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem == 0x16)                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ACPI\PNP0700\4&215d0f95&0 (fdc)
```

**関数ドライバー別のデバイスの表示**

このコマンドを使用して、関数ドライバー別にデバイスを表示します。

```dbgcmd
dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.ServiceName <operator> <service name>)
```

特定の機能ドライバー (atapi など) を使用してデバイスを表示するには、次のコマンドを使用します。

```dbgcmd
1: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.ServiceName == "atapi")
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.ServiceName == "atapi")                
    [0x0]            : PCIIDE\IDEChannel\4&10bf2f88&0&0 (atapi)
    [0x1]            : PCIIDE\IDEChannel\4&10bf2f88&0&1 (atapi)
```

**ブート開始ドライバーの一覧を表示する**

ブート開始ドライバーとして読み込まれた winload.exe の一覧を表示するには、LoaderBlock にアクセスできるコンテキストで、LoaderBlock がまだ残っていることを確認する必要があります。 たとえば、nt ではIopInitializeBootDrivers. このコンテキストでは、ブレークポイントを停止するように設定できます。

```dbgcmd
1: kd> g
Breakpoint 0 hit
nt!IopInitializeBootDrivers:
8225c634 8bff            mov     edi,edi
```

?? 演算子を コマンドを実行して、ブートドライバーの構造を表示します。

```dbgcmd
1: kd> ?? LoaderBlock->BootDriverListHead
struct _LIST_ENTRY
 [ 0x808c9960 - 0x808c8728 ]
   +0x000 Flink            : 0x808c9960 _LIST_ENTRY [ 0x808c93e8 - 0x808a2e18 ]
   +0x004 Blink            : 0x808c8728 _LIST_ENTRY [ 0x808a2e18 - 0x808c8de0 ]
```

Nt \_ の開始アドレスを使用してデータを表示するには、FromListEntry デバッガーオブジェクトを使用します。\_エントリの構造を一覧表示します。

```dbgcmd
1: kd> dx Debugger.Utility.Collections.FromListEntry(*(nt!_LIST_ENTRY *)0x808c9960, "nt!_BOOT_DRIVER_LIST_ENTRY", "Link")
Debugger.Utility.Collections.FromListEntry(*(nt!_LIST_ENTRY *)0x808c9960, "nt!_BOOT_DRIVER_LIST_ENTRY", "Link")                
    [0x0]            [Type: _BOOT_DRIVER_LIST_ENTRY]
    [0x1]            [Type: _BOOT_DRIVER_LIST_ENTRY]
    [0x2]            [Type: _BOOT_DRIVER_LIST_ENTRY]
    [0x3]            [Type: _BOOT_DRIVER_LIST_ENTRY]
    [0x4]            [Type: _BOOT_DRIVER_LIST_ENTRY]
    [0x5]            [Type: _BOOT_DRIVER_LIST_ENTRY]
...
```

データのグリッドビューを作成するには、-g オプションを使用します。

```dbgcmd
dx -r1 -g Debugger.Utility.Collections.FromListEntry(*(nt!_LIST_ENTRY *)0x808c9960, "nt!_BOOT_DRIVER_LIST_ENTRY", "Link")
```

**機能別にデバイスを表示する**

DevicCapabilityFlags オブジェクトを使用して、機能別にデバイスを表示します。

```dbgcmd
dx -r1 @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => (n.DeviceNodeObject.CapabilityFlags & <flag>) != 0)
```

次の表は、一般的なデバイス機能フラグでの dx コマンドの使用方法をまとめたものです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">リムーバブル</td>
<td align="left"><div class="code">

<code>dbgcmd
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x10) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x10) != 0)                
    [0x0]            : SWD\PRINTENUM\{2F8DBBB6-F246-4D84-BB1D-AA8761353885}
    [0x1]            : SWD\PRINTENUM\{F210BC77-55A1-4FCA-AA80-013E2B408378}
    [0x2]            : SWD\PRINTENUM\{07940A8E-11F4-46C3-B714-7FF9B87738F8}
    [0x3]            : DISPLAY\Default_Monitor\6&1a097cd8&0&UID5527112 (monitor)</code>

</div></td>
</tr>
<tr class="even">
<td align="left">UniqueID</td>
<td align="left"><div class="code">

<code>dbgcmd
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x40) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x40) != 0)                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ROOT\volmgr\0000 (volmgr)
    [0x2]            : ROOT\spaceport\0000 (spaceport)
...</code>

</div></td>
</tr>
<tr class="odd">
<td align="left">SilentInstall</td>
<td align="left"><div class="code">

<code>dbgcmd
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x80) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x80) != 0)                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ROOT\volmgr\0000 (volmgr)
    [0x2]            : ROOT\spaceport\0000 (spaceport)
...</code>

</div></td>
</tr>
<tr class="even">
<td align="left">RawDeviceOk</td>
<td align="left"><div class="code">

<code>dbgcmd
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x100) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x100) != 0)                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : SWD\MMDEVAPI\MicrosoftGSWavetableSynth
    [0x2]            : SWD\IP_TUNNEL_VBUS\IP_TUNNEL_DEVICE_ROOT
...</code>

</div></td>
</tr>
<tr class="odd">
<td align="left">SurpriseRemovalOK</td>
<td align="left"><div class="code">

<code>dbgcmd
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x200) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x200) != 0)                
    [0x0]            : SWD\MMDEVAPI\MicrosoftGSWavetableSynth
    [0x1]            : SWD\IP_TUNNEL_VBUS\IP_TUNNEL_DEVICE_ROOT
    [0x2]            : SWD\PRINTENUM\PrintQueues
...</code>

</div></td>
</tr>
</tbody>
</table>


CapabilityFlags の詳細については、「[**デバイスの \_ 機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)」を参照してください。


## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目

[dx (デバッガー オブジェクト モデル式の表示)](dx--display-visualizer-variables-.md)

[NatVis のネイティブ デバッガー オブジェクト](native-debugger-objects-in-natvis.md)

[JavaScript 拡張機能のネイティブ デバッガー オブジェクト](native-objects-in-javascript-extensions.md) 

---







