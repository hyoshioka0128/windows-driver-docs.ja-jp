---
title: Debugger Data Model 関数のエイリアス
description: 関数のエイリアスは、デバッガーの拡張機能で定義されている機能をデバッガーのユーザーからアクセスできる、簡単な一意短い名前です。
keywords:
- Debugger Data Model 関数のエイリアス
ms.date: 03/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: c04dcac55ffd45c03742252a279d6f1ed3a7bc69
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368538"
---
# <a name="debugger-data-model-function-aliases"></a>Debugger Data Model 関数のエイリアス

関数のエイリアスは、一意の短い名前 (C++ または JavaScript などのいくつかのスクリプト環境で記述された) かどうかは、デバッガーの拡張機能で定義されている機能をデバッガーのユーザーからアクセスできます。 データ モデルの関数オブジェクト (IModelMethod を実装するオブジェクト) に関連付けられたこの短い名前を取得します。 その関数は、任意の数の引数を受け取り、1 つの値を返します。 関数のエイリアスとを呼び出すことの効果の値は、関数のエイリアスを呼び出す方法とどのようなホスト デバッガーによって異なります内で呼び出されます。 

このトピックでは、リーダーがデバッガー オブジェクト モデル ファイルと JavaScript に精通する前提としています。 JavaScript でデバッガー オブジェクトの使用方法の詳細については、次を参照してください。 [JavaScript 拡張機能のネイティブ デバッガー オブジェクト](native-objects-in-javascript-extensions.md)します。

いくつかの例を使用して次のとおり、dx コマンドの使用に関する詳細については、dx コマンドを参照してください[dx (表示デバッガー オブジェクト モデルの式)](dx--display-visualizer-variables-.md)します。 さらに、LINQ を使用して説明されている[デバッガー オブジェクトで LINQ を使用して](https://docs.microsoft.com/windows-hardware/drivers/debugger/using-linq-with-the-debugger-objects)します。



## <a name="using-function-alias-as-extension-commands"></a>拡張機能のコマンドとして関数を使用してエイリアス

場合デバッグ拡張機能と同様、WinDbg プレビューで作成されたすべての関数のエイリアスを呼び出すことができる **!** 「書きあがりました」コマンド。 関数に引数がない場合を呼び出すだけです。 aliasName と、関数を呼び出すと、結果の値を表示します。 たとえば (JavaScript の機能拡張で作成された)

たとえば、この関数は 2 つの定数値を提供します*pi*と*e*します。

```cpp
function __constants()
{
    return { math_constants : { pi :  3.1415926535 , e :  2.7182818284}, description : "Archimedes' pi and Euler's number e" };
}

function initializeScript()
{
    return [new host.functionAlias(__constants, "constants")];
}
```

ここでは、関数のエイリアスの呼び出しの結果。 

```dbgcmd
0:000> !constants
@$constants()                 : [object Object]
    math_constants   : [object Object]
    description      : Archimedes' pi and Euler's number e
```

DML へのリンクを複雑なオブジェクトが自動的に生成されます。 前に示した math_constants をクリックすると、次の出力が発生します。 

```dbgcmd
0:000> dx -r1 @$constants().math_constants
@$constants().math_constants                 : [object Object]
    pi               : 3.141593
    e                : 2.718282
```


関数の引数の場合は、関数のエイリアス コマンド自体の後に指定できます。 関数のエイリアス コマンドの後に来る式と見なされが評価されるように注意してください。 テキスト文字列は、関数に直接渡されません。 1 つの引数式の後、関数のエイリアス コマンド自体に付属することができます。 複数の引数の必要があるかっこで囲まれた次の例に示すように関数呼び出しをした場合と同じです。


```cpp
function __oneArgument(x)
{
    return -x;
}

function __twoArguments(x, y)
{
    return x + y;
}

function initializeScript()
{
    return [new host.functionAlias(__oneArgument, "neg"),
            new host.functionAlias(__twoArguments, "add")];
}
```

次のように、これら 2 つの関数を呼び出すことができます。

```dbgcmd
0:000> !neg 42
@$neg(42)        : -42

0:000> !add (5, 7)
@$add(5, 7)      : 0xc
```


## <a name="function-alias-use-with-the-dx-expression-evaluator"></a>Dx 式エバリュエーターでの関数の別名の使用

デバッグ拡張機能だけでなく **!** 「書きあがりました」コマンド、エイリアス化された関数を呼び出すための構文、すべての関数のエイリアスに関連付けられている名前が付いている場合、dx 式エバリュエーターで直接利用*@$* 次のようにします。  

```dbgcmd
0:000> dx @$neg(42)
@$neg(42)        : -42

0:000> dx @$add(99, 77)
@$add(99, 77)    : 0xb0
```


## <a name="function-alias-design-considerations"></a>関数のエイリアスの設計に関する考慮事項

関数のエイリアスは、データの大部分の機能がどのモデルの拡張機能が公開されている唯一の方法はなりません。 (C++ または JavaScript である) データ モデルの拡張機能は、型またはその他のデバッガーの概念に関連付けられたデータが公開することをほとんど常に含める必要があります。 Debugger.Models.Process またはそのオブジェクトのサブの名前空間の下のプロセスに関連付けられていることがあります。 関数のエイリアスは、の便利な方法が大幅に長くクエリが必要となるデータを取得する (または変換)。 

カーネル モードの例としては、次のクエリは PnP デバイス ツリーを受け取りし、デバイスの場合は、単純なフラット リストに平坦化します。 

```dbgcmd
0: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children),5
@$cursession.Devices.DeviceTree.Flatten(n => n.Children),5                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ROOT\volmgr\0000 (volmgr)
    [0x2]            : ROOT\BasicDisplay\0000 (BasicDisplay)
    [0x3]            : ROOT\CompositeBus\0000 (CompositeBus)
    [0x4]            : ROOT\vdrvroot\0000 (vdrvroot)
    [...]     
```

この JavaScript コードでは、これを関数のエイリアスとして実装する方法を示しています。 

```dbgcmd
function __flatDevices()
{
    return host.currentSession.Devices.DeviceTree.Flatten(n => n.Children);
}

function initializeScript()
{
    return [new host.functionAlias(__flatDevices, "devices")];
}
```

関数のエイリアスは、デバッグ拡張機能のコマンドとして呼び出すことができます。 

```dbgcmd
0: kd> !devices
@$devices()                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ROOT\volmgr\0000 (volmgr)
    [0x2]            : ROOT\BasicDisplay\0000 (BasicDisplay)
    [0x3]            : ROOT\CompositeBus\0000 (CompositeBus)
    [0x4]            : ROOT\vdrvroot\0000 (vdrvroot)
    [0x5]            : ROOT\spaceport\0000 (spaceport)

    ...
```

関数のエイリアスを使用する利点の 1 つは、さらに絞り込んだ dx の構文を使用することができます。 この例では、where 句は「ハード」を含むデバイス ノードの検索に追加されます。

```dbgcmd
0: kd> dx @$devices().Where(n => n.InstancePath.Contains("Harddisk"))
@$devices().Where(n => n.InstancePath.Contains("Harddisk"))                
    [0x0]            : STORAGE\VolumeSnapshot\HarddiskVolumeSnapshot1
    [0x1]            : STORAGE\VolumeSnapshot\HarddiskVolumeSnapshot2
    [0x2]            : STORAGE\VolumeSnapshot\HarddiskVolumeSnapshot3
    [0x3]            : STORAGE\VolumeSnapshot\HarddiskVolumeSnapshot4
    [0x4]            : STORAGE\VolumeSnapshot\HarddiskVolumeSnapshot5
    [0x5]            : STORAGE\VolumeSnapshot\HarddiskVolumeSnapshot6
```


次のように LINQ コマンドは、関数型エイリアス - で使用できます。すべての。存在する。カウントします。まずは。、フラット化します。GroupBy、します。前の。OrderBy、します。OrderByDescending、します。選択するとします。どこ。 これらのメソッドが (可能な限り) に従って、 C# LINQ メソッド フォーム。 詳細については、次を参照してください。[デバッガー オブジェクトで LINQ を使用して](https://docs.microsoft.com/windows-hardware/drivers/debugger/using-linq-with-the-debugger-objects)します。



**グリッドの表示**

他 dx コマンドを使用することができますが実行された後、コマンドを右クリックし、"グリッドとして表示 をクリックしてまたは追加して"-g"の結果のグリッド ビューを取得するコマンド。 並べ替え、たとえば InstancePath に使用する任意の列をクリックすることができます。

```dbgcmd
0: kd> dx -g @$devices().OrderBy(obj => obj.@"InstancePath")
```

![debugger objects function alias grid output showing sorted rows](images/debugger-objects-function-alias.png) 



## <a name="process-threads-example"></a>プロセス スレッドの例

デバッガー オブジェクトは、「デバッガーの」ルート名前空間に射影されます。 プロセス、モジュール、スレッド、スタック、スタック フレーム、およびローカル変数は、LINQ クエリで使用するために利用します。

この例の JavaScript では、現在のセッションのプロセスのスレッド数を表示する方法を示します。

```dbgcmd
function __Processes()
{
    return host.currentSession.Processes.Select(p => ({Name: p.Name, ThreadCount: p.Threads.Count()}));
}

function initializeScript()
{
    return [new host.functionAlias(__Processes, "Processes")];
}
```
例の出力を表示します。プロセスの関数のエイリアスです。


```dbgcmd
0: kd> !Processes
@$Processes()                
    [0x0]            : [object Object]
    [0x4]            : [object Object]
    [0x1b4]          : [object Object]
    [0x248]          : [object Object]
    [0x2c4]          : [object Object]
    [0x340]          : [object Object]
    [0x350]          : [object Object]
    [0x3d4]          : [object Object]
    [0x3e8]          : [object Object]
    [0x4c]           : [object Object]
    [0x214]          : [object Object]
    [0x41c]          : [object Object]
    [0x494]          : [object Object]

...    
```
この例で、最大スレッド数の上位 5 プロセスが表示されます。

```dbgcmd
0: kd> dx -r1 @$Processes().OrderByDescending(p =>p.ThreadCount),5
@$Processes().OrderByDescending(p =>p.ThreadCount),5                
    [0x4]            : [object Object]
    [0x180]          : [object Object]
    [0x978]          : [object Object]
    [0xda4]          : [object Object]
    [0x3e8]          : [object Object]
    [...]   
```



## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。

[dx (表示デバッガー オブジェクト モデルの式)](dx--display-visualizer-variables-.md)

[デバッガー オブジェクトを LINQ で使用します。](using-linq-with-the-debugger-objects.md)

[NatVis でネイティブ デバッガー オブジェクト](native-debugger-objects-in-natvis.md)

[JavaScript の拡張機能のネイティブ デバッガー オブジェクト](native-objects-in-javascript-extensions.md) 

---






