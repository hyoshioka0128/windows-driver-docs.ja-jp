---
title: デバッガー オブジェクトを LINQ で使用します。
description: デバッガー オブジェクトを LINQ で使用します。 LINQ 構文は、データを検索および操作デバッガー オブジェクトを使用できます。
keywords:
- デバッガー オブジェクトを LINQ で使用します。
ms.date: 08/10/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38ac8dabc17e446eac28706c309d099663184d09
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527824"
---
# <a name="using-linq-with-the-debugger-objects"></a>デバッガー オブジェクトを LINQ で使用します。

LINQ 構文は、データを検索および操作デバッガー オブジェクトを使用できます。 LINQ に、構造化照会言語 (SQL) データベースのクエリに使用される概念的に似ています。 さまざまな LINQ メソッドを使用して、検索、フィルター、デバッグ データを解析することができます。 LINQC#メソッド構文を使用します。 LINQ および LINQ の詳細についてはC#構文では、次のトピックを参照してください。

[LINQ (Language-integrated Query)](https://msdn.microsoft.com/library/bb397926.aspx)

[C# での LINQ の概要](https://msdn.microsoft.com/library/bb397933.aspx)

## <a name="native-debugger-objects"></a>ネイティブ デバッガー オブジェクト

ネイティブ デバッガー オブジェクトは、さまざまな構成要素とデバッガー環境の動作を表します。 デバッガー オブジェクトの例では、次に示します。

-   セッション
-   スレッド/スレッド
-   プロセス/処理
-   スタック フレームのスタック フレーム/
-   ローカル変数
-   モジュール/モジュール
-   ユーティリティ
-   状態
-   設定

NatVis デバッガー オブジェクトを使用することができます。 詳細については、[NatVis ネイティブ デバッガー オブジェクト](native-debugger-objects-in-natvis.md)を参照してください。 JavaScript でデバッガー オブジェクトの使用方法の詳細については、次を参照してください[JavaScript 拡張機能のネイティブ デバッガー オブジェクト。](native-objects-in-javascript-extensions.md)

## <a name="dx-command"></a>Dx コマンド

ここでの使用例については、dx コマンドの使用に関する詳細については、dx コマンドを[dx (表示デバッガー オブジェクト モデルの式)](dx--display-visualizer-variables-.md)します。


## <a name="function-objects-lambda-expressions"></a>関数オブジェクト (ラムダ式)

データのクエリに使用されるメソッドの多くは、ユーザーがコレクション内のオブジェクト間で関数を指定したを繰り返し実行するという考え方に基づいています。 クエリを実行し、デバッガーでのデータを操作する機能をサポートするためには、dx コマンドは、相当するものを使用してラムダ式をサポートしています。C#構文。 使用して、ラムダ式が定義されている、=&gt;演算子として次のとおりです。

(引数) =&gt; (結果)

Dx で LINQ を使用する方法については、この簡単な例 5 および 7 を加算するをお試しください。

```dbgcmd
kd> dx ((x, y) => (x + y))(5, 7) 
```

Dx コマンドの表示では、ラムダ式をバックアップし、12 の結果を表示します。

```dbgcmd
((x, y) => (x + y))(5, 7)  : 12
```

このラムダ式の例では、「こんにちは」と"World"の文字列を結合します。

```dbgcmd
kd> dx ((x, y) => (x + y))("Hello", "World")
((x, y) => (x + y))("Hello", "World") : HelloWorld
```

## <a name="debugger-objects-examples"></a>デバッガー オブジェクトの例

デバッガー オブジェクトは、「デバッガーの」ルート名前空間に射影されます。 プロセス、モジュール、スレッド、スタック、スタック フレーム、およびローカル変数は、LINQ クエリで使用するために利用します。

次のように LINQ コマンドを使用できます。すべての。存在する。カウントします。まずは。、フラット化します。GroupBy、します。前の。OrderBy、します。OrderByDescending、します。選択するとします。どこ。 これらのメソッドが (可能な限り) に従って、 C# LINQ メソッド フォーム。

この例では、ほとんどのスレッドを実行している上位 5 個のプロセスを示します。

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

この例では、物理デバイス オブジェクトのドライバーの名前でグループ化されたプラグ アンド プレイ デバイス ツリーでデバイスが表示されます。 すべての出力が表示されます。

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

## <a name="dx-command-tab-auto-completion"></a>Dx コマンド タブの自動補完

コンテキスト タブ キーの自動補完は、LINQ クエリ メソッドを認識しており、ラムダのパラメーターに対しては機能します。

たとえば、入力 (またはコピーして貼り付けます) デバッガーには、次のテキスト。 TAB キーを押して複数回を潜在的な入力候補を順番にします。

```dbgcmd
dx -r2 Debugger.Sessions.First().Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.
```

まで TAB キーを押す"。名前"が表示されます。 閉じかっこを追加")"し、enter キーを押してコマンドを実行します。

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

この例では、キーの比較子メソッドの完了を示します。 キーは文字列であるために、置換は string のメソッドを表示します。

```dbgcmd
dx -r2 Debugger.Sessions.First().Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.Name, (a, b) => a.
```

まで TAB キーを押す"。長さ"が表示されます。 閉じかっこを追加")"し、enter キーを押してコマンドを実行します。

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

@$、変数名を付けることで、ユーザー定義変数を定義できます。 ユーザー定義変数は、ラムダ、LINQ クエリの結果に dx を利用できます、たとえば、何も割り当てることができます。

作成し、このようなユーザー変数の値を設定できます。

```dbgcmd
kd> dx @$String1="Test String"
```

使用して定義済みのユーザー変数を表示する*Debugger.State.UserVariables*または *@$ var*します。

```dbgcmd
kd> dx Debugger.State.UserVariables
Debugger.State.UserVariables : 
    mySessionVar     : 
    String1          : Test String
```

変数を使用して、削除することができます。削除します。

```dbgcmd
kd> dx @$vars.Remove("String1")
```

この例では、参照 Debugger.Sesssions ユーザー変数を定義する方法を示します。

```dbgcmd
kd> dx @$mySessionVar = Debugger.Sessions
```

ユーザー定義変数は、次に示すように、使用できます。

```dbgcmd
kd> dx -r2 @$mySessionVar 
@$mySessionVar   : 
    [0x0]            : Remote KD: KdSrv:Server=@{<Local>},Trans=@{COM:Port=\\.\com3,Baud=115200,Timeout=4000}
        Processes        : 
        Devices     
```

**ユーザー定義変数、匿名型**

この動的オブジェクトの作成の完了を使用して、C#匿名型の構文 (新しい {...})。 詳細については、匿名型について詳細は、[匿名型 (C#プログラミング ガイド)](https://msdn.microsoft.com/library/bb397696.aspx)を参照してください。 この例では、整数、文字列値を持つ匿名型を作成します。

```dbgcmd
kd> dx -r1 new { MyInt = 42, MyString = "Hello World" }
new { MyInt = 42, MyString = "Hello World" } : 
    MyInt            : 42
    MyString         : Hello World
```

## <a name="system-defined-variables"></a>システム変数を定義します。

次のシステム定義変数は、任意の LINQ dx クエリで使用できます。

-   @$ cursession - 現在のセッション

-   @$ curprocess - 現在のプロセス

-   @$ 可能性のある curthread - 現在のスレッド

この例の表示、システムの使用は、変数を定義します。

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

## <a name="supported-linq-syntax---query-methods"></a>LINQ 構文のクエリ メソッドをサポート

どの dx 定義として反復可能な任意のオブジェクト (いることをネイティブの配列が NatVis コンテナー、またはデバッガーの拡張機能オブジェクトとしてそれを記述する型) に投影される一連の LINQ (または同等の LINQ) のメソッドがあります。 これらのクエリ メソッドを以下に示します。 クエリ メソッドへの引数の署名は、すべてのクエリ メソッドの後に一覧表示されます。

フィルター処理メソッド

|                            |                                                                                                                                   |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| .場所 (PredicateMethod) | 述語のメソッドが true を返す入力コレクションのすべてのオブジェクトを格納するオブジェクトの新しいコレクションを返します。 |



投影メソッド

|                                     |                                                                                                                                                                                                                                                                                                                             |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .平坦化 ( \[KeyProjectorMethod\] ) | コンテナー (ツリー) の入力のコンテナーを受け取り、ツリー内のすべての要素を持つ 1 つのコンテナーに平坦化します。 キー プロジェクターの省略可能なメソッドは、指定した場合、ツリーは、コンテナーのキー コンテナーとそのキーはプロジェクション メソッドの呼び出しによって決まります自体であると見なされます。 |
| .(KeyProjectorMethod) を選択します。      | 入力コレクション内のすべてのオブジェクトでプロジェクター メソッドの呼び出しの結果を格納するオブジェクトの新しいコレクションを返します。                                                                                                                                                                                          |



グループ化メソッド

|                                                                                                                            |                                                                                                                                                                                                               |
|----------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .GroupBy (KeyProjectorMethod、 \[KeyComparatorMethod\] )                                                                   | キーのプロジェクター メソッドを呼び出すことによって決定される同じキーを持つ入力コレクション内のすべてのオブジェクトをグループ化して、コレクションの新しいコレクションを返します。 比較子を省略可能なメソッドを指定することができます。 |
| 結合 (キー セレクター メソッドの外部、内部キー セレクター メソッド、結果セレクターのメソッドは InnerCollection \[ComparatorMethod\]) | キー セレクター関数に基づいて 2 つのシーケンスを結合し、値のペアを抽出します。 比較子を省略可能なメソッドも指定できます。                                                                        |
| Intersect (InnerCollection、 \[ComparatorMethod\])                                                                          | 積集合、2 つのコレクションのそれぞれに出現する要素を返します。 比較子を省略可能なメソッドも指定できます。                                                               |
| 共用体 (InnerCollection、 \[ComparatorMethod\])                                                                              | 和集合、2 つのコレクションのいずれかに出現する一意の要素を返します。 比較子を省略可能なメソッドも指定できます。                                                             |



データ セット メソッド

|                                                |                                                                                                                                                                                                   |
|------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 含まれています (オブジェクト、 \[ComparatorMethod\])        | シーケンスが、指定された要素を含めるかどうかを判断します。 比較子を省略可能なメソッドには、提供たびに、要素は、シーケンス内のエントリと比較を呼び出すことができます。 |
| Distinct (\[ComparatorMethod\])                | 重複するコレクションの値を削除します。 比較子を省略可能なメソッドを指定するには、各時のオブジェクトをコレクション内で呼び出されるを比較する必要があります。                                      |
| 除く (InnerCollection、 \[ComparatorMethod\]) | 差集合を 2 番目のコレクションに表示されない 1 つのコレクションの要素を返します。 省略可能な比較演算子、メソッドを指定できます。                                 |
| Concat (InnerCollection)                       | 1 つのシーケンスを形成する 2 つのシーケンスを連結します。                                                                                                                                                  |



並べ替えメソッド

|                                                                    |                                                                                                                                                                                                      |
|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .OrderBy (KeyProjectorMethod、 \[KeyComparatorMethod\] )           | 入力コレクション内のすべてのオブジェクトのキーの射影メソッドを呼び出すことによって提供されるキーに従って昇順でコレクションを並べ替えます。 比較子を省略可能なメソッドを指定することができます。  |
| .OrderByDescending (KeyProjectorMethod、 \[KeyComparatorMethod\] ) | 入力コレクション内のすべてのオブジェクトのキーの射影メソッドを呼び出すことによって提供されるキーに従って降順でコレクションを並べ替えます。 比較子を省略可能なメソッドを指定することができます。 |



集計メソッド

|                            |                                                                                                                                                |
|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| カウント)                   | コレクション内の要素の数を返すメソッド。                                                                                |
| Sum (\[ProjectionMethod\]) | コレクション内の値の合計を計算します。 必要に応じて、合計が発生する前に要素を変換するプロジェクター メソッドを指定できます。 |



Skip メソッド

|                             |                                                                                               |
|-----------------------------|-----------------------------------------------------------------------------------------------|
| スキップ (数)                | シーケンス内の指定位置までの要素をスキップします。                                      |
| SkipWhile (PredicateMethod) | 述語関数に基づき、条件を満たさない要素までの要素をスキップします。 |



メソッドを実行します。

|                             |                                                                                               |
|-----------------------------|-----------------------------------------------------------------------------------------------|
| 取得 (カウント)                | シーケンス内の指定した位置まで要素を取得します。                                      |
| TakeWhile (PredicateMethod) | 述語関数に基づき、条件を満たさない要素までの要素を取得します。 |



比較メソッド

|                                                       |                                                                                                                                  |
|-------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| SequenceEqual (InnerCollection、 \[ComparatorMethod\]) | ペアに要素を比較することで、2 つのシーケンスが等しいかどうかを判断します。 オプションの比較子を指定することができます。 |



エラー処理メソッド

|                                     |                                                                                   |
|-------------------------------------|-----------------------------------------------------------------------------------|
| AllNonError (PredicateMethod)       | コレクションのすべてのエラーのない要素が指定された条件を満たすかどうかを返します。 |
| FirstNonError (\[PredicateMethod\]) | エラーのないコレクションの最初の要素を返します。                    |
| LastNonError (\[PredicateMethod\])  | エラーのないコレクションの最後の要素を返します。                     |



その他の方法

|                                |                                                                                                                                                                                                                                                                              |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .すべて (PredicateMethod)       | 入力コレクション内のすべての要素で指定された述語メソッドの呼び出しの結果が true かどうかを返します。                                                                                                                                                       |
| .任意 (PredicateMethod)       | 入力コレクション内の要素で指定された述語メソッドを呼び出した結果が true かどうかを返します。                                                                                                                                                         |
| .最初 ( \[PredicateMethod\] ) | コレクション内の最初の要素を返します。 省略可能な述語が渡された場合は、述語への呼び出しが true を返すコレクションの最初の要素を返します。                                                                                                |
| .最後 ( \[PredicateMethod\] )  | コレクション内の最後の要素を返します。 省略可能な述語が渡された場合は、述語への呼び出しが true を返すコレクションの最後の要素を返します。                                                                                                  |
| Min (\[KeyProjectorMethod\])    | コレクションの最小の要素を返します。 他のユーザーに比較する前に、各メソッドをプロジェクトには、省略可能なプロジェクター メソッドを指定できます。                                                                                                                         |
| 最大 (\[KeyProjectorMethod\])    | コレクションの最大の要素を返します。 他のユーザーに比較する前に、各メソッドをプロジェクトには、省略可能なプロジェクター メソッドを指定できます。                                                                                                                         |
| 1 つ (\[PredicateMethod\])    | リスト (またはエラー コレクションには、1 つ以上の要素が含まれている場合) からの唯一の要素を返します。 述語を指定すると、その述語を満たす 1 つの要素を返します (1 つ以上の要素が満たしている場合、関数はエラーを返します代わりに)。 |



**引数の署名**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">KeyProjectorMethod: (obj =&gt;任意のキー)</td>
<td align="left">コレクションのオブジェクトを受け取り、そのオブジェクトからキーを返します。</td>
</tr>
<tr class="even">
<td align="left">KeyComparatorMethod: ((a、b) =&gt;整数値)</td>
<td align="left">2 つのキーを受け取り、それらを比較を取得します。
<p>場合は-1 (、 &lt; b)。</p>
<p>場合は 0 (、= = b)。</p>
<p>場合は 1 (、 &gt; b)。</p></td>
</tr>
<tr class="odd">
<td align="left">PredicateMethod: (obj =&gt;ブール値)</td>
<td align="left">コレクションのオブジェクトを受け取り、true またはそのオブジェクトが特定の条件を満たしているかどうかに基づいて false を返します。</td>
</tr>
</tbody>
</table>



## <a name="supported-linq-syntax---string-manipulation"></a>サポートされている LINQ 構文 - 文字列操作

すべての文字列オブジェクトでは、使用できるように射影には、次の方法があります。

クエリの関連するメソッドとプロパティ

|                                     |                                                                                                                                                                                                                                   |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .Contains ( OtherString )           | OtherString が入力文字列に含まれるかどうかを示すブール値を返します。                                                                                                                                                 |
| .EndsWith ( OtherString )           | 入力文字列が OtherString で終わるかどうかを示すブール値を返します。                                                                                                                                                |
| 長さ                              | 文字列の長さを返すプロパティ。                                                                                                                                                                                |
| .StartsWith ( OtherString )         | 入力文字列が OtherString で始まるかどうかを示すブール値を返します。                                                                                                                                              |
| .部分文字列 (StartPos、\[長さ\]) | 指定された開始位置から開始する入力文字列内の部分文字列を返します。 省略可能な長さは、指定した場合、返される部分文字列は、; 指定された長さになりますそれ以外の場合 – は、文字列の末尾に移動します。 |



その他のメソッド

|                              |                                                                                   |
|------------------------------|-----------------------------------------------------------------------------------|
| .IndexOf ( OtherString )     | 入力文字列内で最初に見つかった OtherString のインデックスを返します。 |
| .LastIndexOf ( OtherString ) | OtherString の最後に見つかった、入力文字列内のインデックスを返します。  |



書式指定メソッド

|                                          |                                                                                                                                                                                                                                                     |
|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .PadLeft ( TotalWidth )                  | 幅を指定する文字列の合計の長さを表示するために必要な文字列の左側にあるスペースを追加します。                                                                                                                    |
| .PadRight ( TotalWidth )                 | 幅を指定する文字列の合計の長さを表示するために必要な文字列の右側にあるスペースを追加します。                                                                                                                   |
| .削除 (StartPos、\[長さ\])         | 指定された開始位置として、入力文字列から文字を削除します。 省略可能な長さのパラメーターは、指定した数の文字が削除されます。それ以外の場合 – 文字列の末尾まですべての文字は削除されます。 |
| .Replace ( SearchString, ReplaceString ) | 指定された ReplaceString 出現するすべての入力文字列内で SearchString に置き換えます。                                                                                                                                                 |



文字列オブジェクトのプロジェクション

文字列オブジェクトを任意のオブジェクトに直接投影メソッド以外に、メソッドを利用できるようにに投影される次のメソッドがそれ自体が、文字列変換。

|                      |                                                                                                                                                                                                                  |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .ToDisplayString ( ) | オブジェクトの文字列の変換を返します。 これは、オブジェクトの dx 呼び出しで表示される文字列の変換です。 ToDisplayString の出力を書式設定の書式指定子を行うことができます。 |



次の例では、書式指定子の使用を示します。

```dbgcmd
kd> dx (10).ToDisplayString("d")
(10).ToDisplayString("d") : 10

kd> dx (10).ToDisplayString("x")
(10).ToDisplayString("x") : 0xa

kd> dx (10).ToDisplayString("o")
(10).ToDisplayString("o") : 012

kd> dx (10).ToDisplayString("b") 
(10).ToDisplayString("b")  : 0y1010
```

## <a name="span-iddebuggingplugandplayspanspan-iddebuggingplugandplayspanspan-iddebuggingplugandplayspandebugging-plug-and-play-example"></a><span id="Debugging_Plug_and_Play"></span><span id="debugging_plug_and_play"></span><span id="DEBUGGING_PLUG_AND_PLAY"></span>プラグ アンド プレイの例のデバッグ


このセクションでは説明する方法、プラグ アンド プレイのオブジェクトをデバッグする LINQ クエリを使用するデバッガー オブジェクトの構築されているを使用できます。

**すべてのデバイスを表示します。**

使用*Flatten*ですべてのデバイスを表示する、デバイス ツリー。 

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

他 dx コマンドを使用することができますが実行された後、コマンドを右クリックし、"グリッドとして表示 をクリックしてまたは追加して"-g"の結果のグリッド ビューを取得するコマンド。

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

**状態ごとのデバイスの表示**

使用*場所*特定のデバイスの状態を指定します。

```dbgcmd
dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.State <operator> <state number>)
```

たとえば DeviceNodeStarted の状態のデバイスを表示するには、このコマンドを使用します。

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

**ビューが開始されていないデバイス**

このコマンドを使用すると、状態 DeviceNodeStarted ではないデバイスを表示できます。

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

**問題のコードでデバイスの表示**

使用して、 *DeviceNodeObject.Problem*を特定の問題のコードを持つデバイスを表示するオブジェクト。

```dbgcmd
dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem <operator> <problemCode>)
```

たとえば、以外のあるデバイスを表示する 0 個の問題のコードはこのコマンドを使用します。 これにより、同様の情報を"[**! devnode** ](-devnode.md) 0 21"。

```dbgcmd
1: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem != 0)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem != 0)                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ACPI\PNP0700\4&215d0f95&0 (fdc)
```

**問題なくすべてのデバイスを表示します。**

このコマンドを使用して、問題なくすべてのデバイスを表示するには

```dbgcmd
1: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem == 0)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem == 0)                
    [0x0]            : ROOT\volmgr\0000 (volmgr)
    [0x1]            : ROOT\BasicDisplay\0000 (BasicDisplay)
    [0x2]            : ROOT\CompositeBus\0000 (CompositeBus)
    [0x3]            : ROOT\vdrvroot\0000 (vdrvroot)
...
```

**特定の問題を持つすべてのデバイスを表示します。**

0x16 の問題の状態のデバイスを表示するのにには、このコマンドを使用します。

```dbgcmd
1: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem == 0x16)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem == 0x16)                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ACPI\PNP0700\4&215d0f95&0 (fdc)
```

**関数のドライバーによってデバイスの表示**

このコマンドを使用すると、関数のドライバーによってデバイスを表示できます。

```dbgcmd
dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.ServiceName <operator> <service name>)
```

Atapi など、特定機能ドライバーを使用してデバイスを表示するには、このコマンドを使用します。

```dbgcmd
1: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.ServiceName == "atapi")
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.ServiceName == "atapi")                
    [0x0]            : PCIIDE\IDEChannel\4&10bf2f88&0&0 (atapi)
    [0x1]            : PCIIDE\IDEChannel\4&10bf2f88&0&1 (atapi)
```

**ブート開始ドライバーの一覧を表示します。**

どのような winload の一覧を表示するには、としてブート開始ドライバーを読み込む必要があります、LoaderBlock は今でも、LoaderBlock および初期の段階へのアクセスがあるコンテキストであります。 たとえば、nt 中!IopInitializeBootDrivers します。 このコンテキストで停止するブレークポイントを設定できます。

```dbgcmd
1: kd> g
Breakpoint 0 hit
nt!IopInitializeBootDrivers:
8225c634 8bff            mov     edi,edi
```

使用して、[概要] タブ ブート ドライバー構造を表示するコマンドです。

```dbgcmd
1: kd> ?? LoaderBlock->BootDriverListHead
struct _LIST_ENTRY
 [ 0x808c9960 - 0x808c8728 ]
   +0x000 Flink            : 0x808c9960 _LIST_ENTRY [ 0x808c93e8 - 0x808a2e18 ]
   +0x004 Blink            : 0x808c8728 _LIST_ENTRY [ 0x808a2e18 - 0x808c8de0 ]
```

Debugger.Utility.Collections.FromListEntry デバッガー オブジェクトを使用して、nt の開始アドレスを使用して、データの表示。\_一覧\_エントリの構造体。

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

-G オプションを使用して、データのグリッド ビューを作成します。

```dbgcmd
dx -r1 -g Debugger.Utility.Collections.FromListEntry(*(nt!_LIST_ENTRY *)0x808c9960, "nt!_BOOT_DRIVER_LIST_ENTRY", "Link")
```

**デバイスを表示する機能**

DeviceNodeObject.CapabilityFlags オブジェクトを使用して機能により、デバイスを表示します。

```dbgcmd
dx -r1 @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => (n.DeviceNodeObject.CapabilityFlags & <flag>) != 0)
```

このテーブルは、一般的なデバイス機能フラグで dx コマンドの使用をまとめたものです。

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
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x10) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x10) != 0)                
    [0x0]            : SWD\PRINTENUM\{2F8DBBB6-F246-4D84-BB1D-AA8761353885}
    [0x1]            : SWD\PRINTENUM\{F210BC77-55A1-4FCA-AA80-013E2B408378}
    [0x2]            : SWD\PRINTENUM\{07940A8E-11F4-46C3-B714-7FF9B87738F8}
    [0x3]            : DISPLAY\Default_Monitor\6&amp;1a097cd8&amp;0&amp;UID5527112 (monitor)</code>

</div></td>
</tr>
<tr class="even">
<td align="left">一意の Id</td>
<td align="left"><div class="code">

<code>dbgcmd
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x40) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x40) != 0)                
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
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x80) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x80) != 0)                
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
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x100) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x100) != 0)                
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
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x200) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x200) != 0)                
    [0x0]            : SWD\MMDEVAPI\MicrosoftGSWavetableSynth
    [0x1]            : SWD\IP_TUNNEL_VBUS\IP_TUNNEL_DEVICE_ROOT
    [0x2]            : SWD\PRINTENUM\PrintQueues
...</code>

</div></td>
</tr>
</tbody>
</table>


詳細については、CapabilityFlags を参照してください。 [**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)します。


## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。

[dx (表示デバッガー オブジェクト モデルの式)](dx--display-visualizer-variables-.md)

[NatVis でネイティブ デバッガー オブジェクト](native-debugger-objects-in-natvis.md)

[JavaScript の拡張機能のネイティブ デバッガー オブジェクト](native-objects-in-javascript-extensions.md) 

---







