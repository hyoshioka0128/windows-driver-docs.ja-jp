---
title: JavaScript 拡張機能のネイティブ デバッガー オブジェクト
description: ネイティブ デバッガー オブジェクトは、さまざまな構成要素とデバッガー環境の動作を表します。 オブジェクトは、JavaScript の拡張機能に渡された (またはで取得した)。
ms.assetid: A8E12564-D083-43A7-920E-22C4D627FEE8
ms.date: 12/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: fddf5a08df7845bf1eecfdd24596a608a9d5cd2f
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464386"
---
# <a name="native-debugger-objects-in-javascript-extensions"></a>JavaScript 拡張機能のネイティブ デバッガー オブジェクト


ネイティブ デバッガー オブジェクトは、さまざまな構成要素とデバッガー環境の動作を表します。 オブジェクトは、デバッガーの状態を操作するに渡された (またはで取得した) の JavaScript 拡張機能。

デバッガー オブジェクトの例では、次に示します。

-   セッション
-   スレッド/スレッド
-   プロセス/処理
-   スタック フレームのスタック フレーム/
-   ローカル変数
-   モジュール/モジュール
-   ユーティリティ
-   状態
-   設定

たとえば host.namespace.Debugger.Utility.Control.ExecuteCommand オブジェクトは u コマンドを次の 2 行の JavaScript コードをデバッガーに送信するために使用できます。

```dbgcmd
var ctl = host.namespace.Debugger.Utility.Control;   
var outputLines = ctl.ExecuteCommand("u");
```

このトピックでは、一般的なオブジェクトを使用する方法について説明し、その属性とビヘイビアーの参照情報を提供します。

[データ モデルを使用してデバッガーを拡張します。](#extending)

[JavaScript でデバッガー オブジェクトを拡張します。](#extending-debugger-object)

[JavaScript の拡張機能でデバッガー オブジェクト](#debugger-objects)

[JavaScript の拡張機能のホスト Api](#host-apis)

[JavaScript でのデータ モデルの概念](#data-model)

[デバッガーのデータ モデルの設計に関する考慮事項](#design-considerations)

JavaScript の使用方法の概要については、[JavaScript デバッガー Scripting](javascript-debugger-scripting.md)を参照してください。 デバッガー オブジェクトを使用する JavaScript の例を参照してください。 [JavaScript デバッガーの使用例のスクリプト](javascript-debugger-example-scripts.md)します。 設定オブジェクトの操作については、[ **.settings (デバッグ設定の設定)**](-settings--set-debug-settings-.md)を参照してください。

デバッガー セッションで使用できるオブジェクトを調べるを使用して、 [ **dx (表示 NatVis 式)** ](dx--display-visualizer-variables-.md)コマンド。 たとえば、この dx コマンドを使用して最上位レベル デバッガー オブジェクトの一部を表示できます。

```dbgcmd
0: kd> dx -r2 Debugger
Debugger                
    Sessions         : [object Object]
        [0x0]            : Remote KD: KdSrv:Server=@{<Local>},Trans=@{NET:Port=50000,Key=1.2.3.4,Target}
    Settings        
        Debug           
        Display         
        EngineInitialization
        Extensions      
        Input           
        Sources         
        Symbols         
        AutoSaveSettings : false
    State           
        DebuggerVariables
        PseudoRegisters 
        Scripts         
        UserVariables   
    Utility         
        Collections     
        Control         
        Objects   
```

すべての上に示した項目はクリック可能な DML とさらに recursed ことができますデバッガー オブジェクトの構造の表示にします。

## <a name="span-idextendingspanspan-idextendingspanspan-idextendingspanextending-the-debugger-via-the-data-model"></a><span id="Extending"></span><span id="extending"></span><span id="EXTENDING"></span>データ モデルを使用してデバッガーを拡張します。


デバッガーのデータ モデルは、アプリケーションと、次の属性を持つ Windows でドライバーに関する情報へのインターフェイスを作成できます。

-   検出と分類-論理的に構造化された名前空間は、dx コマンドを使用して照会できます。
-   照会できます - これにより、抽出、標準クエリ言語を使用してデータの並べ替えと LINQ を使用します。
-   拡張 - デバッガーが Natvis や JavaScript などのプロバイダーをスクリプトで、このトピックで説明する手法を使用して拡張可能な論理的かつ一貫して使用できます。

## <a name="span-idextending-debugger-objectspanspan-idextending-debugger-objectspanspan-idextending-debugger-objectspanextending-a-debugger-object-in-javascript"></a><span id="Extending-Debugger-Object"></span><span id="extending-debugger-object"></span><span id="EXTENDING-DEBUGGER-OBJECT"></span>JavaScript でデバッガー オブジェクトを拡張します。


JavaScript でビジュアライザーを作成できるだけでなく、スクリプトの拡張子もコアを変更、セッション、プロセス、スレッド スタック、-、デバッガーの概念は、スタック フレームをローカル変数は、および拡張点を他にも発行自体拡張機能を使用できます。

このセクションでは、デバッガー内で最も重要な概念を拡張する方法について説明します。 共有に組み込まれている拡張機能が説明するガイドラインに従う必要があります[デバッガー データ モデルの設計に関する考慮事項](#design-considerations)します。

**拡張機能を登録します。**

スクリプトでは、initializeScript メソッドから返される配列内のエントリを使用して拡張機能を提供するという事実を登録できます。

```dbgcmd
function initializeScript()
{
    return [new host.namedModelParent(comProcessExtension, "Debugger.Models.Process")];
}
```

指定されたプロトタイプ オブジェクトまたは ES6 クラス (このケースで comProcessExtension) 名の下に登録されているモデルの親データ モデルになることデバッガーに、返される配列内の host.namedModelParent オブジェクトの存在を示しますDebugger.Models.Process します。

**デバッガー オブジェクトの拡張ポイント**

次のデバッガー拡張機能ポイントは、デバッガーに不可欠であり、JavaScript などのスクリプトのプロバイダーで使用される使用可能なは。

|                                |                                                                                              |
|--------------------------------|----------------------------------------------------------------------------------------------|
| Debugger.Models.Sessions       | デバッガーがアタッチされているセッション (ターゲット) の一覧                              |
| Debugger.Models.Session        | デバッガーがアタッチされている個別のセッション (ターゲット) (ライブ ユーザー モードでは、KD など..)。 |
| Debugger.Models.Processes      | セッション内でのプロセスの一覧                                                       |
| Debugger.Models.Threads        | プロセス内のスレッドの一覧                                                         |
| Debugger.Models.Thread         | プロセス内の個々 のスレッド (かどうかに関係なくユーザーまたはカーネル モード)            |
| Debugger.Models.Stack          | スレッドのスタック                                                                        |
| Debugger.Models.StackFrames    | スタックを構成するフレームのコレクション                                               |
| Debugger.Models.StackFrame     | スタック内の個々 のスタック フレーム                                                     |
| Debugger.Models.LocalVariables | スタック フレーム内のローカル変数                                                     |
| Debugger.Models.Parameters     | スタック フレーム内で呼び出しのパラメーター                                               |
| Debugger.Models.Module         | プロセスのアドレス空間内の個々 のモジュール                                   |

 

**その他のデータ モデル オブジェクト**

さらに、コア データ モデルで定義されているいくつか追加のデータ モデル オブジェクトがあります。

|                                             |                                                               |
|---------------------------------------------|---------------------------------------------------------------|
| DataModel.Models.Intrinsic                  | 固有の値を (序数、浮動小数点数など..)。                 |
| DataModel.Models.String                     | 文字列                                                      |
| DataModel.Models.Array                      | ネイティブの配列                                                |
| DataModel.Models.Guid                       | GUID                                                        |
| DataModel.Models.Error                      | Error オブジェクト                                               |
| DataModel.Models.Concepts.Iterable          | これは、反復可能なすべてのオブジェクトに適用                     |
| DataModel.Models.Concepts.StringDisplayable | 表示文字列の変換を持つすべてのオブジェクトに適用 |

 

**例 デバッガーの COM オブジェクトの拡張機能の概要**

例を考えてみましょう。 グローバル インターフェイス テーブル (GIT) など、COM に固有の情報を表示するデバッガー拡張機能を作成することを想像してください。

以前は、ある可能性があります COM. 点にアクセスするための手段を提供するコマンドの数が既存のデバッガー拡張機能 1 つのコマンドは、プロセスの中心とした情報を表示可能性があります (グローバル インターフェイス テーブルのインスタンス)。 別のコマンドには、内にどのようなアパートメント コードが実行されているなどのスレッドの中心とした情報を提供可能性があります。 について知っておくし、COM の他の面を紹介する 2 つ目のデバッガー拡張機能をロードする必要があります。

一連のコマンドを見つけにくいはなく、JavaScript の拡張機能は、デバッガーの概念、プロセスとスレッドは、自然な探索可能なおよびその他のデバッガーの拡張子を持つコンポーザブルである方法でこの情報を追加するを変更できます。

**ユーザーまたはカーネル モード デバッガーのオブジェクトの拡張機能**

デバッガーとデバッガー オブジェクトと、ユーザーとカーネル モードで動作の違いがあります。 デバッガーのモデル オブジェクトを作成するときに、環境で操作することを決定する必要があります。 ユーザー モードの COM で使用されるが、ため作成し、ユーザー モードでこの com 拡張機能をテストします。 その他の状況では、ユーザーとカーネル モードのデバッグの両方で動作する JavaScript デバッガーを作成することができます。

**Sub Namespace を作成します。**

この例に戻って、定義できますプロトタイプまたは ES6 クラス、 *comProcessExtension*プロセス オブジェクトを追加イベントのセットを含むです。

**重要な**  サブ空間の目的は、論理的に構造化データと自然に探索可能なパラダイムを作成します。 たとえば、同じサブ名前空間に関連付けられていない項目をダンプしないでください。 説明した情報を慎重に確認[デバッガー データ モデルの設計に関する考慮事項](#design-considerations)サブ名前空間を作成する前にします。

 

このコード スニペットで作成、既存のプロセス デバッガー オブジェクトに"COM"と呼ばれるサブ空間の追加。

```javascript
var comProcessExtension =
{
    //
    // Add a sub-namespace called 'COM' on process.
    //
    get COM()
    {
        //
        // What is 'this' below...?  It's the debugger's process object.  Yes -- this means that there is a cross-language
        // object hierarchy here.  A C++ object implemented in the debugger has a parent model (prototype) which is
        // implemented in JavaScript.
        //
        return new comNamespace(this);
    }
}
```

**Namespace の実装**

次に、プロセスの名前空間のサブ COM を実装しているオブジェクトを作成します。

**重要な**   (KD またはユーザー モードでは、そのようなアタッチされている) かどうか、複数のプロセスにすることができます。 この拡張機能が、デバッガーの現在の状態は、どのようなことを想定することはできません、ユーザーを対象としています。 だれかをキャプチャできます&lt;someProcess&gt;変数に .COM および変更不適切なプロセスのコンテキストから情報を表示する可能性があります。 ソリューションでは、各インスタンスはの追跡プロセスにアタッチされているように、拡張機能でコードを追加します。 このコード サンプルでは、この情報は、プロパティの 'this' ポインターを使用して渡されます。

`this.__process = process;`

 

```javascript
class comNamespace
{
    constructor(process)
    {
        //
        // This is an entirely JavaScript object.  Each instantiation of a comNamespace will keep track
        // of what process it is attached to (passed via the ''this'' pointer of the property getter
        // we authored above.
        //
        this.__process = process;
    }
    
    get GlobalObjects()
    {
        return new globalObjects(this.__process);
    }
}
```

**COM のグローバル インターフェイス テーブルの実装ロジック**

COM のグローバル インターフェイス テーブルの実装ロジックにこれをより明確に分離には、1 つの ES6 クラスを定義します*gipTable* COM GIP テーブルと切り離されている*globalObjects*、前に示した Namespace 実装コードの領域切り取りで定義されている GlobalObjects() ゲッターからは何が返されますを取得します。 これらを内部の詳細のいずれかのデバッガーの名前空間に公開を避ける initializeScript のクロージャ内では、これらすべての詳細を非表示にできます。

```javascript
// gipTable:
//
// Internal class which abstracts away the GIP Table.  It iterates objects of the form
// {entry : GIPEntry, cookie : GIT cookie}
//
class gipTable
{
    constructor(gipProcess)
    {
        //
        // Windows 8 through certain builds of Windows 10, it's in CGIPTable::_palloc.  In certain builds
        // of Windows 10 and later, this has been moved to GIPEntry::_palloc.  We need to check which.
        //
        var gipAllocator = undefined;
        try
        {
            gipAllocator = host.getModuleSymbol("combase.dll", "CGIPTable::_palloc", "CPageAllocator", gipProcess)._pgalloc;
        }
        catch(err)
        {
        }

        if (gipAllocator == undefined)
        {
            gipAllocator = host.getModuleSymbol("combase.dll", "GIPEntry::_palloc", "CPageAllocator", gipProcess)._pgalloc;
        }

        this.__data = {
            process : gipProcess,
            allocator : gipAllocator,
            pageList : gipAllocator._pPageListStart,
            pageCount : gipAllocator._cPages,
            entriesPerPage : gipAllocator._cEntriesPerPage,
            bytesPerEntry : gipAllocator._cbPerEntry,
            PAGESHIFT : 16,
            PAGEMASK : 0x0000FFFF,
            SEQNOMASK : 0xFF00
        };
    }

    *[Symbol.iterator]()
    {
        for (var pageNum = 0; pageNum < this.__data.pageCount; ++pageNum)
        {
            var page = this.__data.pageList[pageNum];
            for (var entryNum = 0; entryNum < this.__data.entriesPerPage; ++entryNum)
            {
                var entryAddress = page.address.add(this.__data.bytesPerEntry * entryNum);
                var gipEntry = host.createPointerObject(entryAddress, "combase.dll", "GIPEntry *", this.__data.process);
                if (gipEntry.cUsage != -1 && gipEntry.dwType != 0)
                {
                    yield {entry : gipEntry, cookie : (gipEntry.dwSeqNo | (pageNum << this.__data.PAGESHIFT) | entryNum)};
                }
            }
        }
    }

    entryFromCookie(cookie)
    {
        var sequenceNo = (cookie & this.__data.SEQNOMASK);
        cookie = cookie & ~sequenceNo;
        var pageNum = (cookie >> this.__data.PAGESHIFT);
        if (pageNum < this.__data.pageCount)
        {
            var page = this.__data.pageList[pageNum];
            var entryNum = (cookie & this.__data.PAGEMASK);
            if (entryNum < this.__data.entriesPerPage)
            {
                var entryAddress = page.address.add(this.__data.bytesPerEntry * entryNum);
                var gipEntry = host.createPointerObject(entryAddress, "combase.dll", "GIPEntry *", this.__data.process);
                if (gipEntry.cUsage != -1 && gipEntry.dwType != 0 && gipEntry.dwSeqNo == sequenceNo)
                {
                    return {entry : gipEntry, cookie : (gipEntry.dwSeqNo | (pageNum << this.__data.PAGESHIFT) | entryNum)};
                }
            }
        }

        //
        // If this exception flows back to C/C++, it will be a failed HRESULT (according to the type of error -- here E_BOUNDS)
        // with the message being encapsulated by an error object.
        //
        throw new RangeError("Unable to find specified value");
    }
}





// globalObjects:
//
// The class which presents how we want the GIP table to look to the data model.  It iterates the actual objects
// in the GIP table indexed by their cookie.
//
class globalObjects
{
    constructor(process)
    {
        this.__gipTable = new gipTable(process);
    }

    *[Symbol.iterator]()
    {
        for (var gipCombo of this.__gipTable)
        {
            yield new host.indexedValue(gipCombo.entry.pUnk, [gipCombo.cookie]);
        }
    }

    getDimensionality()
    {
        return 1;
    }

    getValueAt(cookie)
    {
        return this.__gipTable.entryFromCookie(cookie).entry.pUnk;
    }
}
```

最後に、host.namedModelRegistration を使用して、新しい COM 機能を登録します。

```javascript
function initializeScript()
{
    return [new host.namedModelParent(comProcessExtension, "Debugger.Models.Process"),
            new host.namedModelRegistration(comNamespace, "Debugger.Models.ComProcess")];
}
```

コードをメモ帳などのアプリケーションを使用して GipTableAbstractor.js に保存します。

ここで、プロセス情報がユーザー モードでこの拡張機能を読み込む前に。

```dbgcmd
0:000:x86> dx @$curprocess
@$curprocess                 : DataBinding.exe
    Name             : DataBinding.exe
    Id               : 0x1b9c
    Threads         
    Modules  
```

JavaScript のプロバイダーと拡張機能をスクリプトを読み込みます。

```dbgcmd
0:000:x86> !load jsprovider.dll
0:000:x86> .scriptload C:\JSExtensions\GipTableAbstractor.js
JavaScript script successfully loaded from 'C:\JSExtensions\GipTableAbstractor.js'
```

Dx コマンドを使用して、定義済みの @$ curprocess を使用して、プロセスに関する情報を表示します。

```dbgcmd
0:000:x86> dx @$curprocess
@$curprocess                 : DataBinding.exe
    Name             : DataBinding.exe
    Id               : 0x1b9c
    Threads         
    Modules         
    COM              : [object Object]
```

```dbgcmd
0:000:x86> dx @$curprocess.COM
@$curprocess.COM                 : [object Object]
    GlobalObjects    : [object Object]
0:000:x86> dx @$curprocess.COM.GlobalObjects
@$curprocess.COM.GlobalObjects                 : [object Object]
    [0x100]          : 0x12f4fb0 [Type: IUnknown *]
    [0x201]          : 0x37cfc50 [Type: IUnknown *]
    [0x302]          : 0x37ea910 [Type: IUnknown *]
    [0x403]          : 0x37fcfe0 [Type: IUnknown *]
    [0x504]          : 0x12fe1d0 [Type: IUnknown *]
    [0x605]          : 0x59f04e8 [Type: IUnknown *]
    [0x706]          : 0x59f0eb8 [Type: IUnknown *]
    [0x807]          : 0x59f5550 [Type: IUnknown *]
    [0x908]          : 0x12fe340 [Type: IUnknown *]
    [0xa09]          : 0x5afcb58 [Type: IUnknown *]
```

このテーブルは、GIT の cookie を使用してプログラムでアクセスできるもあります。

```dbgcmd
0:000:x86> dx @$curprocess.COM.GlobalObjects[0xa09]
@$curprocess.COM.GlobalObjects[0xa09]                 : 0x5afcb58 [Type: IUnknown *]
    [+0x00c] __abi_reference_count [Type: __abi_FTMWeakRefData]
    [+0x014] __capture        [Type: Platform::Details::__abi_CapturePtr]
```

**LINQ でのデバッガー オブジェクトの概念を拡張します。**

プロセスやスレッドなどのオブジェクトを拡張できるほか、JavaScript と、データ モデルに関連付けられている概念を拡張できます。 たとえば、新しい LINQ メソッドを追加することはすべてを反復可能な。 すべてのエントリが反復可能な N 回重複データの例を拡張機能、"DuplicateDataModel"を検討してください。 次のコードでは、この実装方法を示します。

```javascript
function initializeScript()
{
    var newLinqMethod =
    {
        Duplicate : function *(n)
        {
            for (var val of this)
            {
                for (var i = 0; i < n; ++i)
                {
                    yield val;
                }
            };
        }
    };

    return [new host.namedModelParent(newLinqMethod, "DataModel.Models.Concepts.Iterable")];
}
```

コードをメモ帳などのアプリケーションを使用して DuplicateDataModel.js に保存します。

必要な場合の JavaScript スクリプト プロバイダーを読み込み、DuplicateDataModel.js 拡張機能を読み込みます。

```dbgcmd
0:000:x86> !load jsprovider.dll
0:000:x86> .scriptload C:\JSExtensions\DuplicateDataModel.js
JavaScript script successfully loaded from 'C:\JSExtensions\DuplicateDataModel.js'
```

新しい複製関数をテストするのにには、dx コマンドを使用します。

```dbgcmd
0: kd> dx -r1 Debugger.Sessions.First().Processes.First().Threads.Duplicate(2),d
Debugger.Sessions.First().Processes.First().Threads.Duplicate(2),d                 : [object Generator]
    [0]              : nt!DbgBreakPointWithStatus (fffff800`9696ca60) 
    [1]              : nt!DbgBreakPointWithStatus (fffff800`9696ca60) 
    [2]              : intelppm!MWaitIdle+0x18 (fffff805`0e351348) 
    [3]              : intelppm!MWaitIdle+0x18 (fffff805`0e351348) 
…
```

## <a name="span-iddebugger-objectsspanspan-iddebugger-objectsspanspan-iddebugger-objectsspandebugger-objects-in-javascript-extensions"></a><span id="Debugger-Objects"></span><span id="debugger-objects"></span><span id="DEBUGGER-OBJECTS"></span>JavaScript の拡張機能でデバッガー オブジェクト


**ネイティブ オブジェクトを渡す**

デバッガー オブジェクトに渡されるまたは JavaScript の拡張機能のさまざまな方法で取得できます。

-   これらは、JavaScript 関数またはメソッドに渡すことができます。
-   JavaScript のプロトタイプのインスタンスのオブジェクトがあることができます (として、ビジュアライザーのインスタンス)
-   ネイティブ デバッガー オブジェクトを作成するためのホスト メソッドから返されます
-   デバッガーのネイティブ オブジェクトを作成するためのホスト メソッドから返されます

JavaScript の拡張機能に渡されるオブジェクトをデバッガーには、このセクションで説明されている機能のセットがあります。

-   プロパティへのアクセス
-   射影された名前
-   ネイティブ デバッガー オブジェクトに関連する特殊な種類
-   追加の属性

**プロパティへのアクセス**

JavaScript プロバイダー自体によって配置されたオブジェクトでは、いくつかのプロパティがありますが、JavaScript を入力するネイティブ オブジェクトのプロパティの大部分は、データ モデルによって提供されます。 プロパティ アクセス---object.propertyName またはオブジェクトのつまり\[propertyName\]次が発生します。

-   場合*propertyName*プロパティの名前、オブジェクトの上に JavaScript プロバイダー自体によって投影、これを解決するこれまずそれ以外の場合。
-   場合*propertyName*キーの名前、オブジェクトの上に、データ モデル (別のビジュアライザー) によって投影、これを解決するこの名前それ以外の 2 つ目
-   場合*propertyName*名前のネイティブ オブジェクトのフィールド、それを解決するこの名前それ以外の 3 つ目
-   オブジェクトが、ポインターの場合、ポインターを逆参照すると上記のサイクルは (ネイティブのフィールドの後に、キーの後に逆参照されたオブジェクトの射影されたプロパティ) を引き続き

JavaScript--object.propertyName とオブジェクト プロパティへのアクセスの通常の方法\[propertyName\] --'dx' のコマンドは、デバッガー内と同様に、オブジェクトの基になるネイティブ フィールドにアクセスします。

**射影された名前**

次のプロパティ (とメソッド) は、JavaScript を入力するネイティブ オブジェクトに投影されます。

| メソッド             | 署名                  | 説明                                                                                                                                |
|--------------------|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| hostContext        | プロパティ                   | 内のオブジェクトがコンテキストを表すオブジェクトを返します (アドレス空間、デバッグ ターゲットなど..)。                              |
| TargetLocation     | プロパティ                   | 抽象化であるオブジェクトを返しますのオブジェクトが、アドレス空間内 (仮想アドレス、レジスタ、サブレジスタなど..)。 |
| targetSize         | プロパティ                   | オブジェクトのサイズを返します (実質的に: sizeof (&lt;型のオブジェクト&gt;)                                                                |
| addParentModel     | .addParentModel(object)    | オブジェクトを新しい親モデル (データ mdoel 側の JavaScript プロトタイプかが) を追加します。                                          |
| RemoveParentModel  | .removeParentModel(object) | オブジェクトから指定した親モデルを削除します。                                                                                               |
| runtimeTypedObject | プロパティ                   | オブジェクトに対して分析を実行し、(最も派生) ランタイムの型に変換しようとしています。                                                 |

 

オブジェクトが、ポインターの場合、次のプロパティ (とメソッド) が、ポインターが JavaScript の入力に投影されます。

| プロパティ名 | 署名      | 説明                                                                    |
|---------------|----------------|--------------------------------------------------------------------------------|
| 追加           | .add(value)    | ポインターと、指定した値の間のポインターの加算を実行します     |
| address       | プロパティ       | 64 ビットの序数に基づくオブジェクト (ライブラリの種類) としてポインターのアドレスを返します |
| 逆参照します。   | .dereference() | ポインターを逆参照し、基になるオブジェクトを返します                     |
| IsNull        | プロパティ       | ポインター値が nullptr (0) であるかどうかを返します。                        |

 

**ネイティブ デバッガー オブジェクトに関連する特殊な種類**

**オブジェクトの場所**

ネイティブ オブジェクトの targetLocation プロパティから返される location オブジェクトには、次のプロパティ (とメソッド) が含まれています。

| プロパティ名 | 署名        | 説明                                          |
|---------------|------------------|------------------------------------------------------|
| 追加           | .add(value)      | 場所に、絶対のバイト オフセットを追加します。        |
| 減算 (subtract)      | .subtract(value) | 場所から絶対のバイト オフセットを減算します。 |

 

**追加の属性**

**Iterability**

データ モデルによって、反復可能なが認識している任意のオブジェクト (ネイティブの配列またはビジュアライザーがある (NatVis またはそれ以外の場合) これにより、反復可能な)、iterator 関数 (ES6 標準 Symbol.iterator 経由でインデックス付き) にする必要があります。 これは、JavaScript でネイティブ オブジェクトが次のように反復処理できることを意味します。

```javascript
function iterateNative(nativeObject)
{
    for (var val of nativeObject)
    {
        // 
        // val will contain each element iterated from the native object.  This would be each element of an array,
        // each element of an STL structure which is made iterable through NatVis, each element of a data structure
        // which has a JavaScript iterator accessible via [Symbol.iterator], or each element of something
        // which is made iterable via support of IIterableConcept in C/C++.
        //
    }
}
```

**満たさなくなりました。 この**

序数を使用して 1 つのディメンションのインデックスとして認識されているオブジェクト (例:: ネイティブ配列) は、標準的なプロパティ アクセス演算子を使用して JavaScript でインデックス可能--オブジェクト\[インデックス\]します。 オブジェクトは名前によってインデックス付けまたは indexable 1 つ以上のディメンションで場合、JavaScript コードは、インデクサーを利用できるように、getValueAt および setValueAt メソッドは、オブジェクトに投影されます。

```javascript
function indexNative(nativeArray)
{
    var first = nativeArray[0];
}
```

**文字列変換**

IStringDisplayableConcept または NatVis DisplayString 要素のサポートを使用して、表示文字列変換のある任意のネイティブ オブジェクトは、その文字列の変換の標準の JavaScript の toString メソッドを使用してアクセスできる必要があります。

```javascript
function stringifyNative(nativeObject)
{
    var myString = nativeObject.toString();
}
```

## <a name="span-idcreatingnativedebuggerobjectsspanspan-idcreatingnativedebuggerobjectsspanspan-idcreatingnativedebuggerobjectsspancreating-native-debugger-objects"></a><span id="Creating_Native_Debugger_Objects"></span><span id="creating_native_debugger_objects"></span><span id="CREATING_NATIVE_DEBUGGER_OBJECTS"></span>ネイティブ デバッガー オブジェクトを作成します。


JavaScript スクリプトがネイティブのオブジェクトへのアクセスを取得するいくつかの方法のいずれかで JavaScript に渡されることによって前述のように、または、ホスト、ライブラリの呼び出しを通じてそれらを作成できます。 ネイティブ デバッガー オブジェクトを作成するのにには、次の関数を使用します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メソッド</th>
<th align="left">署名</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>host.getModuleSymbol</p></td>
<td align="left"><p>getModuleSymbol (moduleName、シンボル、[contextInheritor])</p>
<p>getModuleSymbol (moduleName、シンボル、[typeName]、[contextInheritor])</p></td>
<td align="left"><p>特定のモジュール内でグローバル シンボルのオブジェクトを返します。 シンボル名とモジュールの名前は、文字列です。</p>
<p>場合、省略可能な<em>contextInheritor</em>引数を指定すると、モジュールとシンボルは、渡されたオブジェクトと同じコンテキスト (アドレス空間、デバッグ対象) 内で探されます。 引数が指定されていない場合、モジュールと記号を検索する、デバッガーの現在のコンテキストでします。 1 回限りのテスト スクリプトではない JavaScript 拡張機能では、コンテキストの明示的なを必ず指定する必要があります。</p>
<p>場合、省略可能な<em>typeName</em>引数が指定されて、シンボルは、渡された型であると想定されます、およびシンボルで示される型は無視されます。 モジュールのパブリック シンボルを操作するを待ち受けている呼び出し元が、明示的な型名を指定する必要があります常に注意してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>host.createPointerObject</p></td>
<td align="left"><p>createPointerObject (アドレス、moduleName、typeName [contextInheritor])</p></td>
<td align="left"><p>指定したアドレスまたは場所には、ポインター オブジェクトを作成します。 モジュール名と型名は、文字列です。</p>
<p>場合、省略可能な<em>contextInheritor</em>引数を指定すると、モジュールとシンボルは、渡されたオブジェクトと同じコンテキスト (アドレス空間、デバッグ対象) 内で探されます。 引数が指定されていない場合、モジュールと記号を検索する、デバッガーの現在のコンテキストでします。 1 回限りのテスト スクリプトではない JavaScript 拡張機能では、コンテキストの明示的なを必ず指定する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>host.createTypedObject</p></td>
<td align="left"><p>createTypedObject(location, moduleName, typeName, [contextInheritor])</p></td>
<td align="left"><p>指定した位置にデバッグ対象のアドレス空間内のネイティブな型指定されたオブジェクトを表すオブジェクトを作成します。 モジュール名と型名は、文字列です。</p>
<p>場合、省略可能な<em>contextInheritor</em>引数を指定すると、モジュールとシンボルは、渡されたオブジェクトと同じコンテキスト (アドレス空間、デバッグ対象) 内で探されます。 引数が指定されていない場合、モジュールと記号を検索する、デバッガーの現在のコンテキストでします。 1 回限りのテスト スクリプトではない JavaScript 拡張機能では、コンテキストの明示的なを必ず指定する必要があります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idhost-apisspanspan-idhost-apisspanspan-idhost-apisspanhost-apis-for-javascript-extensions"></a><span id="Host-APIs"></span><span id="host-apis"></span><span id="HOST-APIS"></span>JavaScript の拡張機能のホスト Api


JavaScript のプロバイダーを読み込むすべてのスクリプトのグローバル名前空間にホストと呼ばれるオブジェクトを挿入します。 このオブジェクトは、デバッガーの名前空間へのアクセスに加えて、スクリプトの重要な機能へのアクセスを提供します。 2 つのフェーズに設定されます。

-   **フェーズ 1**:任意のスクリプトが実行される前に、ホスト オブジェクトには、スクリプト自体を初期化し、その拡張ポイント (両方のプロデューサーとコンシューマーとして) の登録に必要な機能の最小限のセットにはのみが含まれます。 ルートおよび初期化コードをデバッグ対象の状態を操作したり、複雑な操作を実行する必要はありませんし、そのため、ホストが完全に設定されていないまで initializeScript メソッドが返された後にします。

-   **フェーズ 2**:InitializeScript を返した後、デバッグ ターゲットの状態を操作するために必要なすべてのものが、そのホスト オブジェクトが設定されます。

**ホスト オブジェクトのレベル**

いくつかの重要な機能では、ホスト オブジェクトの直下です。 残りの部分は、サブ名前です。 名前空間は、次に示します。

| Namespace   | 説明                                                              |
|-------------|--------------------------------------------------------------------------|
| 診断 | 診断とスクリプトのコードのデバッグを支援する機能    |
| memory      | 読み取りと書き込みデバッグ ターゲット内のメモリを有効にする機能 |

 

**ルート レベル**

直接、ホスト オブジェクト内で次のプロパティ、メソッド、およびコンス トラクターはあります。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">名前</th>
<th align="left">署名</th>
<th align="left">現在のフェーズ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">createPointerObject</td>
<td align="left"><p>createPointerObject (アドレス、moduleName、typeName [contextInheritor])</p></td>
<td align="left">2</td>
<td align="left">指定したアドレスまたは場所には、ポインター オブジェクトを作成します。 モジュール名と型名は、文字列です。 省略可能な<strong>contextInheritor</strong>引数が getModuleSymbol と同様に動作します。</td>
</tr>
<tr class="even">
<td align="left">createTypedObject</td>
<td align="left"><p>createTypedObject(location, moduleName, typeName, [contextInheritor])</p></td>
<td align="left">2</td>
<td align="left">指定した位置にデバッグ対象のアドレス空間内のネイティブな型指定されたオブジェクトを表すオブジェクトを作成します。 モジュール名と型名は、文字列です。 省略可能な contextInheritor 引数は、getModuleSymbol とは動作します。</td>
</tr>
<tr class="odd">
<td align="left">現在</td>
<td align="left"><p>プロパティ</p></td>
<td align="left">2</td>
<td align="left">デバッガーの現在のプロセスを表すオブジェクトを返します</td>
</tr>
<tr class="even">
<td align="left">CurrentSession</td>
<td align="left"><p>プロパティ</p></td>
<td align="left">2</td>
<td align="left">デバッガーの現在のセッションを表すオブジェクトを返します (どのターゲット、ダンプなど) は、デバッグ中</td>
</tr>
<tr class="odd">
<td align="left">呼び出せるようになって</td>
<td align="left"><p>プロパティ</p></td>
<td align="left">2</td>
<td align="left">デバッガーの現在のスレッドを表すオブジェクトを返します</td>
</tr>
<tr class="even">
<td align="left">式の評価</td>
<td align="left"><p>式の評価 (expression, [contextInheritor])</p></td>
<td align="left">2</td>
<td align="left">これは、デバッグ ターゲットのみの言語を使用して式を評価するデバッグ ホストを呼び出します。 場合、省略可能な<em>contextInheritor</em>引数を指定すると、式は、コンテキストで評価されます (例:: アドレス空間とデバッグのターゲット) の引数それ以外の場合、評価されます、デバッガーの現在のコンテキストで。</td>
</tr>
<tr class="odd">
<td align="left">evaluateExpressionInContext</td>
<td align="left"><p>evaluateExpressionInContext (コンテキスト、式)</p></td>
<td align="left">2</td>
<td align="left">これは、デバッグ ターゲットのみの言語を使用して式を評価するデバッグ ホストを呼び出します。 コンテキスト引数は、評価版を利用するには、このポインター、暗黙の型を示します。 式は、コンテキストで評価されます (例:: アドレス空間とデバッグ対象) で示される、<em>コンテキスト</em>引数。</td>
</tr>
<tr class="even">
<td align="left">getModuleSymbol</td>
<td align="left"><p>getModuleSymbol (moduleName、シンボル、[contextInheritor])</p></td>
<td align="left">2</td>
<td align="left">特定のモジュール内でグローバル シンボルのオブジェクトを返します。 シンボル名とモジュールの名前は、文字列です。 場合、省略可能な<em>contextInheritor</em>引数を指定すると、モジュールとシンボルは、渡されたオブジェクトと同じコンテキスト (アドレス空間、デバッグ対象) 内で探されます。 引数が指定されていない場合、モジュールと記号を検索する、デバッガーの現在のコンテキストでします。 1 回限りのスクリプトではない JavaScript 拡張機能はコンテキストの明示的なを必ず指定する必要があります。</td>
</tr>
<tr class="odd">
<td align="left">getNamedModel</td>
<td align="left"><p>getNamedModel(modelName)</p></td>
<td align="left">2</td>
<td align="left">指定された名前に対して登録されたデータ モデルを返します。 これをまだ登録されていない名前に対して呼び出す区切ればことに注意してください。 そうとその名前のスタブが作成され、スタブの操作が登録時に実際のオブジェクトになります</td>
</tr>
<tr class="even">
<td align="left">indexedValue</td>
<td align="left"><p>new indexedValue(value, indicies)</p></td>
<td align="left">2</td>
<td align="left">インデックスの既定のセットを繰り返し行う一連の値に割り当てるには JavaScript 反復子から返されるオブジェクトのコンス トラクターです。 インデックスのセットは、JavaScript 配列として表現する必要があります。</td>
</tr>
<tr class="odd">
<td align="left">Int64</td>
<td align="left"><p>新しい Int64 (value, [highValue])</p></td>
<td align="left">1</td>
<td align="left">これは、ライブラリ Int64 型を作成します。 1 つの引数 (なしの変換) Int64 にパックしてなどに配置できる任意の値になります。 省略可能な 2 番目の引数が指定されている場合は、最初の引数の変換が下位の 32 ビットにパックされているし、2 番目の引数の変換が上位の 32 ビットにまとめられます。</td>
</tr>
<tr class="even">
<td align="left">namedModelParent</td>
<td align="left"><p>new namedModelParent(object, name)</p></td>
<td align="left">1</td>
<td align="left">返される配列に配置するためのもので、オブジェクトのコンス トラクター <strong>initializeScript</strong>、このデータとして、JavaScript プロトタイプまたは ES6 クラスを使用して表す、指定した名前のデータ モデルの親拡張機能をモデル化</td>
</tr>
<tr class="odd">
<td align="left">namedModelRegistration</td>
<td align="left"><p>new namedModelRegistration(object, name)</p></td>
<td align="left">1</td>
<td align="left">返される配列に配置するためのもので、オブジェクトのコンス トラクター <strong>initializeScript</strong>、これは、JavaScript プロトタイプの登録を表しますまたは、データと ES6 クラスは、他の拡張機能を検索できるように既知の名前を使用してモデルと。拡張</td>
</tr>
<tr class="even">
<td align="left">名前空間</td>
<td align="left"><p>プロパティ</p></td>
<td align="left">2</td>
<td align="left">により、デバッガーのルート名前空間へのアクセスを直接します。 Host.namespace.Debugger.Sessions.First() を使用して最初のデバッグ対象のプロセス一覧にアクセスいずれかなど。このプロパティを使用してプロセス</td>
</tr>
<tr class="odd">
<td align="left">RegisterNamedModel</td>
<td align="left"><p>registerNamedModel(object, modelName)</p></td>
<td align="left">2</td>
<td align="left">これにより、指定した名前でデータ モデルとして、JavaScript プロトタイプまたは ES6 クラスが登録されます。 このような登録には、プロトタイプや検索と他のスクリプトまたはその他のデバッガー拡張によって拡張されたクラスができます。 返すスクリプトを優先する必要がありますに注意してください、 <strong>namedModelRegistration</strong>オブジェクトからその<strong>initializeScript</strong>これを強制的に行うのではなく、メソッド。 変更を強制的に、任意のスクリプトが必要ですが、 <strong>initializeScript</strong>クリーンアップするためにメソッド。</td>
</tr>
<tr class="even">
<td align="left">RegisterExtensionForTypeSignature</td>
<td align="left"><p>registerExtensionForTypeSignature (object, typeSignature)</p></td>
<td align="left">2</td>
<td align="left">これにより、JavaScript プロトタイプまたは ES6 クラスが、拡張機能のデータ モデルの指定された型のシグネチャで指定されたネイティブ型として登録されます。 返すスクリプトを優先する必要がありますに注意してください、 <strong>typeSignatureExtension</strong>オブジェクトからその<strong>initializeScript</strong>これを強制的に行うのではなく、メソッド。 変更を強制的に、任意のスクリプトが必要ですが、 <strong>initializeScript</strong>クリーンアップするためにメソッド。</td>
</tr>
<tr class="odd">
<td align="left">registerPrototypeForTypeSignature</td>
<td align="left"><p>registerPrototypeForTypeSignature (object, typeSignature)</p></td>
<td align="left">2</td>
<td align="left">正規のデータ モデルとしては、JavaScript プロトタイプまたは ES6 クラスを登録しますこの (例:: ビジュアライザー) のネイティブ型として指定された型のシグネチャで指定します。 返すスクリプトを優先する必要がありますに注意してください、 <strong>typeSignatureExtension</strong>オブジェクトからその<strong>initializeScript</strong>これを強制的に行うのではなく、メソッド。 変更を強制的に、任意のスクリプトが必要ですが、 <strong>uninitializeScript</strong>クリーンアップするためにメソッド。</td>
</tr>
<tr class="even">
<td align="left">parseInt64</td>
<td align="left"><p>parseInt64(string, [radix])</p></td>
<td align="left">1</td>
<td align="left">このメソッドは、代わりにライブラリ Int64 型を返す点が標準の JavaScript parseInt メソッドに同様に機能します。 基数を指定すると、ベース 2、8、10、または 16 のように、解析が発生します。</td>
</tr>
<tr class="odd">
<td align="left">typeSignatureExtension</td>
<td align="left"><p>新しい typeSignatureExtension (オブジェクト、typeSignature、[moduleName]、[minVersion]、[maxVersion])</p></td>
<td align="left">1</td>
<td align="left">返される配列に配置するためのもので、オブジェクトのコンス トラクター <strong>initializeScript</strong>、これは、JavaScript プロトタイプまたは ES6 クラスによって型署名を使用して説明されているネイティブ型の拡張機能を表します。 完全引き継ぐのではなく、シグネチャに一致する任意の型のような登録「フィールドを追加」デバッガーの視覚化。 省略可能なモジュールの名前およびバージョンを登録を制限できます。 バージョンは「1.2.3.4」として指定されたスタイルの文字列。</td>
</tr>
<tr class="even">
<td align="left">typeSignatureRegistration</td>
<td align="left"><p>新しい typeSignatureRegistration (オブジェクト、typeSignature、[moduleName]、[minVersion]、[maxVersion])</p></td>
<td align="left">1</td>
<td align="left">返される配列に配置するためのもので、オブジェクトのコンス トラクター <strong>initializeScript</strong>、これは、JavaScript プロトタイプまたはネイティブ型署名に対する ES6 クラスでの正規の登録を表します。 このような登録「は」シグネチャに一致する任意の型ではなく拡張することよりも単に、デバッガーの視覚化。 省略可能なモジュールの名前およびバージョンを登録を制限できます。 バージョンは「1.2.3.4」として指定されたスタイルの文字列。</td>
</tr>
<tr class="odd">
<td align="left">unregisterNamedModel</td>
<td align="left"><p>unregisterNamedModel(modelName)</p></td>
<td align="left">2</td>
<td align="left">によって実行された操作を元に戻す指定した名前で参照からのデータ モデルの登録を解除この<strong>registerNamedModel</strong></td>
</tr>
<tr class="even">
<td align="left">UnregisterExtensionForTypeSignature</td>
<td align="left"><p>unregisterExtensionForTypeSignature (オブジェクト、typeSignature、[moduleName]、[minVersion]、[maxVersion])</p></td>
<td align="left">2</td>
<td align="left">これは、JavaScript プロトタイプまたは ES6 クラスの指定された型のシグネチャで指定されたネイティブ型の拡張データ モデルの中から登録解除します。 論理的に元に戻して registerExtensionForTypeSignature になります。 返すスクリプトを優先する必要がありますに注意してください、 <strong>typeSignatureExtension</strong>オブジェクトからその<strong>initializeScript</strong>これを強制的に行うのではなく、メソッド。 変更を強制的に、任意のスクリプトが必要ですが、 <strong>initializeScript</strong>クリーンアップするためにメソッド。 省略可能なモジュールの名前およびバージョンを登録を制限できます。 バージョンは「1.2.3.4」として指定されたスタイルの文字列。</td>
</tr>
<tr class="odd">
<td align="left">unregisterPrototypeForTypeSignature</td>
<td align="left"><p>unregisterPrototypeForTypeSignature (オブジェクト、typeSignature、[moduleName]、[minVersion]、[maxVersion])</p></td>
<td align="left">2</td>
<td align="left">これは、JavaScript プロトタイプまたは正規のデータ モデルからの ES6 クラス登録解除します。 (例:: ビジュアライザー) のネイティブ型として指定された型のシグネチャで指定します。 論理的に元に戻して registerPrototypeForTypeSignature になります。 返すスクリプトを優先する必要がありますに注意してください、 <strong>typeSignatureRegistration</strong>オブジェクトからその<strong>initializeScript</strong>これを強制的に行うのではなく、メソッド。 変更を強制的に、任意のスクリプトが必要ですが、 <strong>uninitializeScript</strong>クリーンアップするためにメソッド。 省略可能なモジュールの名前およびバージョンを登録を制限できます。 バージョンは「1.2.3.4」として指定されたスタイルの文字列。</td>
</tr>
</tbody>
</table>

 

**診断機能**

次に、診断サブ名前空間ホスト オブジェクトにはが含まれます。

| 名前     | 署名           | 現在のフェーズ | 説明                                                                                                                                                                                                                                                                                                                                                   |
|----------|---------------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| debugLog | debugLog(object...) | 1             | これは、printf スタイルのデバッグ スクリプト拡張機能を提供します。 現在のところ、debugLog からの出力は、デバッガーのコンソール出力にルーティングされます。 時間の後で、この出力のルーティングに柔軟性を提供する計画があります。 注: これは、コンソールに、ユーザーの印刷出力の手段としていない使用する必要があります。 可能性がありますはルーティングされませんが、今後。 |

 

**メモリの機能**

メモリ サブの名前空間ホスト オブジェクトにはには、次のものが含まれています。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">名前</th>
<th align="left">署名</th>
<th align="left">現在のフェーズ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">readMemoryValues</td>
<td align="left"><p>readMemoryValues (場所、numElements、[elementSize]、[isSigned]、[contextInheritor])</p></td>
<td align="left">2</td>
<td align="left">これにより、デバッグ対象のアドレス空間からされた生の配列の値を読み取るし、このメモリのビューの上部に型指定された配列を配置します。 指定された場所には、アドレス (64 ビット値)、場所オブジェクト、またはネイティブ ポインターを指定できます。 配列のサイズが付いて、 <em>numElements</em>引数。 配列の各要素のサイズ (よぶ型) は、オプションで指定されます<em>elementSize</em>と<em>isSigned</em>引数。 このような引数が指定されていない、既定値はバイト (符号なし/1 バイト)。 場合、省略可能な<em>contextInheritor</em>引数を指定すると、コンテキストには、メモリを読み込み、(例:: アドレス空間とデバッグのターゲット) の引数で指定された; それ以外の場合、デバッガーの現在のコンテキストから読み取られます。 このメソッドを使用して、8、16、32 ビット値に、読み取りのメモリ上に配置されている高速な型指定されたビューに注意してください。 64 ビット値でこのメソッドを使用して結果が大幅にコストが高く構築される 64 ビット ライブラリ型の配列。</td>
</tr>
<tr class="even">
<td align="left">readString</td>
<td align="left"><p>readString(location, [contextInheritor])</p>
<p>readString (場所、[長さ]、[contextInheritor])</p></td>
<td align="left">2</td>
<td align="left">これにより、utf-16 に変換します、デバッグ対象のアドレス空間から (現在のコード ページ) のナロー文字列を読み取り、JavaScript 文字列として結果を返します。 メモリを読み取ることができませんでした例外をスロー、可能性があります。 指定された場所 (64 ビット値) のアドレス、または指定できます場所オブジェクトでは、ネイティブの char<em>します。 場合、省略可能な<em>contextInheritor</em>引数を指定すると、コンテキストには、メモリを読み込み、(例:: アドレス空間とデバッグのターゲット) の引数で指定された; それ以外の場合、デバッガーの現在のコンテキストから読み取られます。 場合、省略可能な<em>長さ</em>引数を指定すると、指定した長さの読み取り文字列になります。</td>
</tr>
<tr class="odd">
<td align="left">readWideString</td>
<td align="left"><p>readWideString (場所や [contextInheritor])</p>
<p>readWideString (場所、[長さ]、[contextInheritor])</p></td>
<td align="left">2</td>
<td align="left">これにより、デバッグ対象のアドレス空間から wide(UTF-16) 文字列を読み取り、JavaScript 文字列として結果を返します。 メモリを読み取ることができませんでした例外をスロー、可能性があります。 指定された場所は、アドレス (64 ビット値)、場所オブジェクト、またはネイティブの wchar_t にできる</em>します。 場合、省略可能な<em>contextInheritor</em>引数を指定すると、コンテキストには、メモリを読み込み、(例:: アドレス空間とデバッグのターゲット) の引数で指定された; それ以外の場合、デバッガーの現在のコンテキストから読み取られます。 場合、省略可能な<em>長さ</em>引数を指定すると、指定した長さの読み取り文字列になります。</td>
</tr>
</tbody>
</table>

 

## <a name="span-iddata-modelspanspan-iddata-modelspanspan-iddata-modelspandata-model-concepts-in-javascript"></a><span id="Data-Model"></span><span id="data-model"></span><span id="DATA-MODEL"></span>JavaScript でのデータ モデルの概念


**データ モデルのマッピング**

次のデータ モデルの概念は、JavaScript にマップします。

| 概念                 | ネイティブ インターフェイス             | JavaScript と同等                                                |
|-------------------------|------------------------------|----------------------------------------------------------------------|
| 文字列変換       | IStringDisplayableConcept    | standard: toString(...){...}                                         |
| Iterability             | IIterableConcept             | standard:\[Symbol.iterator\](){...}                                 |
| 満たさなくなりました。 この            | IIndexableConcept            | プロトコル: getDimensionality(...)/getValueAt(...)/setValueAt(...) |
| ランタイム型の変換 | IPreferredRuntimeTypeConcept | protocol: getPreferredRuntimeTypedObject(...)                        |

 

**文字列変換**

文字列変換の概念 (IStringDisplayableConcept) は、標準の JavaScript に直接つながる**toString**メソッド。 すべての JavaScript オブジェクトには、文字列の変換 (Object.prototype によって提供される場合は指定されていない別の場所) がある、データ モデルに返されるすべての JavaScript オブジェクトは、表示文字列に変換できます。 独自の toString を実装する必要が単に文字列の変換をオーバーライドします。

```javascript
class myObject
{
    //
    // This method will be called whenever any native code calls IStringDisplayableConcept::ToDisplayString(...)
    //
    toString()
    { 
        return "This is my own string conversion!";
    }
}
```

**Iterability**

オブジェクトが反復可能なまたはオブジェクトが反復可能なかどうかの ES6 プロトコルに直接マップされないかどうかのデータ モデルの概念です。 任意のオブジェクトを持つ、 \[Symbol.iterator\]メソッドが反復可能なと見なされます。 このような実装には、オブジェクトが反復可能なこと。

反復可能なオブジェクトには、次のようになど実装をことができます。

```javascript
class myObject
{
    //
    // This method will be called whenever any native code calls IIterableConcept::GetIterator
    //
    *[Symbol.iterator]()
    {
        yield "First Value";
        yield "Second Value";
        yield "Third Value";
    }
}
```

特別な考慮事項は、オブジェクトは反復可能なと、インデックス可能な反復子から返されるオブジェクトは、特別な戻り値の型を使用する値と同様に、インデックスを含める必要がありますがで指定する必要があります。

**反復可能なインデックス可能**

反復可能なインデックス可能であるオブジェクトには、反復子からの特別な戻り値が必要です。 値を生成するには、代わりには、反復子は、indexedValue のインスタンスを生成します。 インデックスは、2 番目の引数の配列として indexedValue コンス トラクターに渡されます。 これらは、多次元にすることができますが、インデクサーのプロトコルで返される次元に一致する必要があります。

このコードは、例、implementaion を示しています。

```javascript
class myObject
{
    //
    // This method will be called whenever any native code calls IIterableConcept::GetIterator
    //
    *[Symbol.iterator]()
    {
        //
        // Consider this a map which mapped 42->"First Value", 99->"Second Value", and 107->"Third Value"
        //
        yield new host.indexedValue("First Value", [42]);
        yield new host.indexedValue("Second Value", [99]);
        yield new host.indexedValue("Third Value", [107]);
    }
}
```

**満たさなくなりました。 この**

JavaScript とは異なり、データ モデルはプロパティ アクセスとインデックス作成の非常に明示的な区別によりします。 データ モデルのインデックスとして自体を提示することを希望する任意の JavaScript オブジェクトは、インデクサーと getValueAt および setValueAt メソッドの省略可能なペアの次元を返す getDimensionality メソッドで構成されるプロトコルを実装する必要がありますが指定したインデックス位置にあるオブジェクトの読み取りや書き込みを実行します。 オブジェクトが読み取り専用または書き込み専用の場合は、getValueAt または setValueAt のいずれかのメソッドを省略することができます。

```javascript
class myObject
{
    //
    // This method will be called whenever any native code calls IIndexableConcept::GetDimensionality or IIterableConcept::GetDefaultIndexDimensionality
    //
    getDimensionality()
    {
        //
        // Pretend we are a two dimensional array.
        //
        return 2;
    } 

    //
    // This method will be called whenever any native code calls IIndexableConcept::GetAt
    //
    getValueAt(row, column)
    {
        return this.__values[row * this.__columnCount + column];
    }

    //
    // This method will be called whenever any native code calls IIndexableConcept::SetAt
    //
    setValueAt(value, row, column)
    {
        this.__values[row * this.__columnCount + column] = value;
    }
}
```

**ランタイム型の変換**

これは、JavaScript プロトタイプ/クラスの型システム (ネイティブ) の型に対して登録されている関連するだけです。 デバッガーが分析を実行できる多くの場合 (例: 実行時型情報 (RTTI)/v テーブル分析) コードで表される静的な型のオブジェクトの場合は true。 ランタイムの種類を判断します。 ネイティブ型に対して登録されているデータ モデルには、IPreferredRuntimeTypeConcept の実装を使用してこの動作をオーバーライドできます。 同様に、JavaScript クラスまたはネイティブのオブジェクトに対して登録されているプロトタイプは、getPreferredRuntimeTypedObject メソッドで構成されるプロトコルの実装を使用して、独自の実装を提供できます。

中に、このメソッドでは、何も返すことが技術的と見なされるランタイム型または派生型をあまり問題のあるフォームの何かを返すことに注意してください。 デバッガーのユーザーの重要な混乱などがあります。 このメソッドをオーバーライドすることができます、ただし、する C スタイル ヘッダー + 実装などのオブジェクトのスタイルなどの役に立つ.

```javascript
class myNativeModel
{
    //
    // This method will be called whenever the data model calls IPreferredRuntimeTypeConcept::CastToPreferredRuntimeType
    //
    getPreferredRuntimeTypedObject()
    {
        var loc = this.targetLocation;

        //
        // Perform analysis...
        //
        var runtimeLoc = loc.Add(runtimeObjectOffset);
  
        return host.createTypedObject(runtimeLoc, runtimeModule, runtimeTypeName);
    }
}
```

## <a name="span-iddesign-considerationsspanspan-iddesign-considerationsspanspan-iddesign-considerationsspandebugger-data-model-design-considerations"></a><span id="Design-Considerations"></span><span id="design-considerations"></span><span id="DESIGN-CONSIDERATIONS"></span>デバッガーのデータ モデルの設計に関する考慮事項


**設計の原則**

次の原則を探索可能なクエリ可能なおよびスクリプト可能な情報を提供する、デバッガーの拡張機能を検討してください。

-   情報は、必要な場所に近いです。 たとえば、レジストリ キー ハンドルを格納するローカル変数の一部としてレジストリ キーの情報を表示する必要があります。
-   情報が構成されています。 たとえば、キーの種類、キーの ACL、キー名、および値などの別のフィールドに、レジストリ キーの情報が表示されます。 これは、個々 のフィールドにテキストを解析することがなくアクセスできることを意味します。
-   情報は、一貫性のあります。 レジストリ キー ハンドルに関する情報は表示するファイル ハンドルに関する情報と同様、できるだけ方法。

これらの原則をサポートしていないこれらのアプローチを回避します。

-   単一フラット「キッチン シンク」に、項目な構造の操作を行います。 階層化したものでは、探しているものとサポートの見つけやすさの知識なし探している情報を参照することができます。
-   未加工のテキストの画面を引き続き出力中に、モデルに移行するだけでは、クラシック dbgeng 拡張機能を変換できません。 これが他の拡張機能でコンポーザブルでないと、LINQ 式でクエリを実行することはできません。 代わりに、データを個別のクエリ可能なフィールドに分割します。

**名前付けのガイドライン**

-   フィールドの大文字と小文字は PascalCase にあります。 名が別の文字種、jQuery などのあまり知られているは、例外が考えられます。
-   C++ 識別子で通常使用いない特殊文字を使用しないでください。 たとえば、「合計の長さ」(スペースを含む) などの名前を使用してを回避または"\[サイズ\]"(角かっこを含む)。 この規則はスクリプト言語のこれらの文字は、識別子の一部として使用できない場所から利用しやすいように、コマンド ウィンドウから利用しやすいようにことができます。

**組織と階層のガイドライン**

-   デバッガーの名前空間の最上位レベルは拡張されません。 代わりに、最も関係がある情報が表示されるようデバッガーでの既存のノードを拡張する必要があります。
-   概念と重複しません。 デバッガーに既に存在する概念に関する追加情報を一覧表示するデータ モデルの拡張機能を作成する場合、既存の情報を拡張するより新しい情報に置き換えます。 つまり、モジュールに関する詳細が表示される拡張機能が、既存を拡張する必要があります*モジュール*モジュールの新しいリストを作成するのではなく、オブジェクト。
-   無料ユーティリティのコマンドを浮動小数点の一部にする必要があります、 *Debugger.Utility*名前空間。 サブの名前空間内を適切になる必要がありますも (例: *Debugger.Utility.Collections.FromListEntry*)

**下位互換性と重大な変更します。**

パブリッシュされているスクリプトでは、それに依存する他のスクリプトとの互換性は中断されませんする必要があります。 たとえば、モデルに関数が発行されると、可能な場合は、同じパラメーターと同じ場所に残る必要があります。

**外部のリソースを使用しません。**

-   拡張機能は、外部プロセスを起動する必要があります。 外部プロセスが、デバッガーの動作に干渉することができ、リモート デバッガーのさまざまなシナリオ (例: dbgsrv リモコン、ntsd リモート、および「ntsd-d リモコン」) では不適切な動作
-   拡張機能は、すべてのユーザー インターフェイスを表示しないでください。 表示するユーザー インターフェイス要素では、リモートのデバッグ シナリオで正しく動作して、コンソールのシナリオのデバッグを中断することができます。
-   拡張機能では、デバッガー エンジンまたは文書化されていない方法では、デバッガー UI は操作する必要があります。 これによって、互換性の問題、さまざまな UI を使用したデバッガー クライアントで正しく動作します。
-   拡張機能は、文書化されているデバッガー Api を介してのみ対象の情報にアクセスする必要があります。 Win32 Api は、セキュリティの境界を越えて、リモート多くのシナリオとローカルのデバッグ シナリオでも失敗を通じてターゲットに関する情報にアクセスしようとしています。

**Dbgeng 固有の機能を使用しません。**

拡張機能として使用することを意図したスクリプトは、(「クラシック」デバッガー拡張機能を実行して) などが可能であれば dbgeng 固有の機能に依存する必要があります。 スクリプトは、データ モデルをホストするすべてのデバッガーの上に使用できるようにします。

## <a name="span-idtesting-debugger-extensionsspanspan-idtesting-debugger-extensionsspanspan-idtesting-debugger-extensionsspantesting-debugger-extensions"></a><span id="Testing-Debugger-Extensions"></span><span id="testing-debugger-extensions"></span><span id="TESTING-DEBUGGER-EXTENSIONS"></span>デバッガーの拡張機能のテスト


さまざまなシナリオで作業するには、拡張機能が予想されます。 一部の拡張機能 (カーネルのデバッグ シナリオ) などのシナリオに固有のものが、中には、ほとんどの拡張機能は必要がありますすべてのシナリオでは機能またはサポートされるシナリオを示すメタデータが必要です。

カーネル モード

-   実際のカーネル デバッグ
-   カーネル ダンプのデバッグ

ユーザー モード

-   ライブ ユーザー モードのデバッグ
-   ユーザー モード ダンプのデバッグ

さらに、ようなデバッガーの使用シナリオを検討してください。

-   マルチ プロセス デバッグ
-   複数のセッション (ダンプ + 1 つのセッション内のライブ ユーザーなど) のデバッグ

**リモート デバッガーの使用状況**

リモート デバッガーの使用シナリオで適切な操作をテストします。

-   dbgsrv remotes
-   ntsd リモコン
-   ntsd-d リモコン

詳細については、[デバッグを使用して CDB、NTSD](debugging-using-cdb-and-ntsd.md)と[**プロセス サーバーをアクティブ化する**](activating-a-process-server.md)を参照してください。

**回帰テスト**

デバッガーの新しいバージョンがリリースされた、拡張機能では、機能を確認できますテスト自動化の使用を調査します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[JavaScript デバッガー スクリプト](javascript-debugger-scripting.md)

[JavaScript デバッガーの スクリプトの例](javascript-debugger-example-scripts.md)

 

 






