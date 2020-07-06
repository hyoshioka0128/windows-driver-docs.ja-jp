---
title: JavaScript 拡張機能のネイティブ デバッガー オブジェクト
description: ネイティブデバッガーオブジェクトは、デバッガー環境のさまざまな構造と動作を表します。 オブジェクトは、JavaScript 拡張に渡す (またはで取得) ことができます。
ms.assetid: A8E12564-D083-43A7-920E-22C4D627FEE8
ms.date: 09/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: cf0d7bc68691faba1f245ad597cc9be107004b57
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968425"
---
# <a name="native-debugger-objects-in-javascript-extensions"></a>JavaScript 拡張機能のネイティブ デバッガー オブジェクト


ネイティブデバッガーオブジェクトは、デバッガー環境のさまざまな構造と動作を表します。 オブジェクトは、デバッガーの状態を操作するために (またはで取得した) JavaScript 拡張機能に渡すことができます。

デバッガーオブジェクトの例を次に示します。

-   Session
-   スレッド/スレッド
-   プロセス/プロセス
-   スタックフレーム/スタックフレーム
-   ローカル変数
-   モジュール/モジュール
-   ユーティリティ
-   状態
-   設定

たとえば、次の2行の JavaScript コードを使用して、host.namespace.Debugger.Utility.Control.Exeのコマンドを実行して、u コマンドをデバッガーに送信することができます。

```dbgcmd
var ctl = host.namespace.Debugger.Utility.Control;   
var outputLines = ctl.ExecuteCommand("u");
```

このトピックでは、一般的なオブジェクトを使用する方法と、それらの属性と動作についてのリファレンス情報を提供します。

JavaScript の使用に関する一般的な情報については、「 [Javascript デバッガースクリプト](javascript-debugger-scripting.md)」を参照してください。 デバッガーオブジェクトを使用する JavaScript の例については、「 [Javascript デバッガーのサンプルスクリプト](javascript-debugger-example-scripts.md)」を参照してください。 設定オブジェクトの操作の詳細については、「」を参照してください[**。設定 (デバッグ設定の設定)**](-settings--set-debug-settings-.md)。

デバッガーセッションで使用可能なオブジェクトを調べるには、 [**dx (Display NatVis Expression)**](dx--display-visualizer-variables-.md)コマンドを使用します。 たとえば、この dx コマンドを使用して、最上位レベルのデバッガーオブジェクトの一部を表示できます。

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

上記のすべての項目はクリック可能な DML であり、さらに recursed してデバッガーのオブジェクト構造を表示できます。

## <a name="span-idextendingspanspan-idextendingspanspan-idextendingspanextending-the-debugger-via-the-data-model"></a><span id="Extending"></span><span id="extending"></span><span id="EXTENDING"></span>データモデルを使用したデバッガーの拡張


デバッガーデータモデルでは、次の属性を持つ Windows のアプリケーションとドライバーに関する情報へのインターフェイスを作成できます。

-   検出可能で整理済み-dx コマンドを使用して、論理的に構造化された名前空間を照会できます。
-   LINQ を使用してクエリを実行できます。これにより、標準クエリ言語を使用してデータの抽出と並べ替えを行うことができます。
-   このトピックで説明されている手法と、Natvis や JavaScript などのデバッガースクリプトプロバイダーを使用して、論理的かつ一貫した拡張が可能です。

## <a name="span-idextending-debugger-objectspanspan-idextending-debugger-objectspanspan-idextending-debugger-objectspanextending-a-debugger-object-in-javascript"></a><span id="Extending-Debugger-Object"></span><span id="extending-debugger-object"></span><span id="EXTENDING-DEBUGGER-OBJECT"></span>JavaScript でのデバッガーオブジェクトの拡張

スクリプト拡張機能では、JavaScript でビジュアライザーを作成できるだけでなく、デバッガーの主要な概念 (セッション、プロセス、スレッド、スタック、スタックフレーム、ローカル変数) を変更したり、他の拡張機能が使用できる拡張ポイントとして発行したりすることもできます。

このセクションでは、デバッガー内で中核となる概念を拡張する方法について説明します。 共有するように構築された拡張機能は、「 [JavaScript 拡張機能でのネイティブデバッガーオブジェクト](native-objects-in-javascript-extensions-design-considerations.md)」に示されているガイドラインに準拠している必要があります。設計およびテストに関する考慮事項。

**拡張機能の登録**

スクリプトでは、initializeScript メソッドから返された配列のエントリを通じて拡張機能を提供するという事実を登録できます。

```dbgcmd
function initializeScript()
{
    return [new host.namedModelParent(comProcessExtension, "Debugger.Models.Process")];
}
```

返された配列内にホストの namedModelParent オブジェクトが存在する場合、指定されたプロトタイプオブジェクトまたは ES6 クラス (この場合は comProcessExtension) が、デバッガーに登録されているモデルの親データモデルであることを示します。

**デバッガーオブジェクト拡張ポイント**

次のデバッガー拡張ポイントはデバッガーに不可欠であり、JavaScript などのスクリプトプロバイダーが使用できます。

**Debugger. sessions**: デバッガーがアタッチされているセッション (ターゲット) の一覧

**Debugger. session**: デバッガーがアタッチされている個々のセッション (ターゲット) (ライブユーザーモード、KD など)

**Debugger. processes. プロセス**: セッション内のプロセスの一覧

**Debugger. threads**: プロセス内のスレッドの一覧

**Debugger. Thread**: プロセス内の個々のスレッド (ユーザーモードまたはカーネルモードかどうかに関係なく)

**Debugger. stack. stack**: スレッドのスタック

**Debugger. stackframes**: スタックを構成するフレームのコレクション

**スタックフレーム**: スタック内の個々のスタックフレーム

**LocalVariables**: スタックフレーム内のローカル変数

**Debugger. parameters**: スタックフレーム内の呼び出しのパラメーター

**Debugger. モジュール**: プロセスのアドレス空間内の個々のモジュール


 

**追加 Data Model オブジェクト**

さらに、コアデータモデルによって定義される追加のデータモデルオブジェクトもあります。

**DataModel**: 組み込みの値 (序数、浮動小数点以下など)

**DataModel**: 文字列。

**DataModel**: ネイティブ配列。

**DataModel**: guid。

**DataModel**: error オブジェクト。

**DataModel 反復可能な**: 反復可能なであるすべてのオブジェクトに適用されます。

**DataModel**: 表示文字列変換を含むすべてのオブジェクトに適用されます。


 

**COM デバッガーオブジェクト拡張機能の概要の例**

具体的な例を考えてみましょう。 たとえば、グローバルインターフェイステーブル (GIT) など、COM 固有の情報を表示するデバッガー拡張機能を作成するとします。

以前は、COM に関する情報にアクセスする手段を提供する多数のコマンドを含む既存のデバッガー拡張機能がある可能性があります。 1つのコマンドで、プロセス中心の情報 (インスタンスのグローバルインターフェイステーブル) が表示される場合があります。 別のコマンドは、内部で実行されているアパートメントコードなどのスレッド中心の情報を提供する場合があります。 COM のその他の側面を調べるために、2つ目のデバッガー拡張機能について理解し、読み込む必要がある場合があります。

JavaScript 拡張機能を使用すると、コマンドを検出するための一連の作業を行うのではなく、デバッガーのプロセスとスレッドの概念を変更できます。この情報は、他のデバッガー拡張機能と同様に、自然で探索可能な、コンポーザブルな方法で追加できます。

**ユーザーモードまたはカーネルモードのデバッガーオブジェクト拡張機能**

デバッガーとデバッガーオブジェクトの動作は、ユーザーモードとカーネルモードで異なります。 デバッガーモデルオブジェクトを作成するときは、使用する環境を決定する必要があります。 ここでは、ユーザーモードで COM を操作するため、この com 拡張機能をユーザーモードで作成し、テストします。 他の状況では、ユーザーモードとカーネルモードの両方のデバッグで動作するデバッガー JavaScript を作成できる場合があります。

**サブ名前空間の作成**

この例に戻り、プロトタイプまたは ES6 クラスを定義できます。このクラスに*は、プロセス*オブジェクトに追加する一連の項目が含まれています。

**重要**   サブ名前空間の目的は、論理的に構造化された自然な探索可能なパラダイムを作成することです。 たとえば、関連性のない項目を同じサブ名前空間にダンプしないようにします。 「JavaScript の拡張機能」の「ネイティブデバッガーオブジェクト」で説明されている情報を慎重に確認してください。サブ名前空間を作成する前に、[設計とテストに関する考慮事項](native-objects-in-javascript-extensions-design-considerations.md)を参照

このコードスニペットでは、"COM" と呼ばれるサブ名前空間を既存のプロセスデバッガーオブジェクトに追加します。

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

**名前空間の実装**

次に、プロセスでサブ名前空間 COM を実装するオブジェクトを作成します。

**重要**   複数のプロセスが存在する場合があります (ユーザーモードまたは KD 下でにアタッチされている場合)。 この拡張機能では、デバッガーの現在の状態がユーザーの意図したものであると想定することはできません。 他のユーザーが &lt; &gt; 変数にあるプロセス .com をキャプチャして変更すると、間違ったプロセスコンテキストから情報が表示される可能性があります。 これを解決するには、拡張機能にコードを追加して、各インスタンス化が、アタッチされているプロセスを追跡できるようにします。 このコードサンプルでは、この情報はプロパティの ' this ' ポインターを介して渡されます。

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

**COM グローバルインターフェイステーブルの実装ロジック**

COM グローバルインターフェイステーブルの実装ロジックをより明確に分離するには、ES6*クラスを 1*つ定義します。このクラスは、COM gip テーブルとその他の*globalobjects*を抽象化します。これは、上記の名前空間の実装コード領域で定義されている globalobjects () getter から返されます。 これらの詳細はすべて、initializeScript のクロージャ内で非表示にすることができます。これにより、これらの内部の詳細情報がデバッガーの名前空間に発行されるのを回避できます。

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

最後に、ホストの namedModelRegistration を使用して、新しい COM 機能を登録します。

```javascript
function initializeScript()
{
    return [new host.namedModelParent(comProcessExtension, "Debugger.Models.Process"),
            new host.namedModelRegistration(comNamespace, "Debugger.Models.ComProcess")];
}
```

メモ帳などのアプリケーションを使用して GipTableAbstractor.js にコードを保存します。

この拡張機能を読み込む前に、ユーザーモードで使用可能なプロセス情報を次に示します。

```dbgcmd
0:000:x86> dx @$curprocess
@$curprocess                 : DataBinding.exe
    Name             : DataBinding.exe
    Id               : 0x1b9c
    Threads         
    Modules  
```

JavaScript スクリプトプロバイダーと拡張機能を読み込みます。

```dbgcmd
0:000:x86> !load jsprovider.dll
0:000:x86> .scriptload C:\JSExtensions\GipTableAbstractor.js
JavaScript script successfully loaded from 'C:\JSExtensions\GipTableAbstractor.js'
```

次に、dx コマンドを使用して、定義済みの @ $curprocess を使用してプロセスに関する情報を表示します。

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

このテーブルには、GIT cookie を介してプログラムからアクセスすることもできます。

```dbgcmd
0:000:x86> dx @$curprocess.COM.GlobalObjects[0xa09]
@$curprocess.COM.GlobalObjects[0xa09]                 : 0x5afcb58 [Type: IUnknown *]
    [+0x00c] __abi_reference_count [Type: __abi_FTMWeakRefData]
    [+0x014] __capture        [Type: Platform::Details::__abi_CapturePtr]
```

**LINQ を使用したデバッガーオブジェクトの概念の拡張**

JavaScript では、プロセスやスレッドなどのオブジェクトを拡張できるだけでなく、データモデルに関連付けられた概念を拡張することもできます。 たとえば、新しい LINQ メソッドをすべての反復可能なに追加することができます。 例として、"DuplicateDataModel" という拡張子を使用します。これは、反復可能な N 回のすべてのエントリを複製します。 次のコードは、この実装方法を示しています。

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

メモ帳などのアプリケーションを使用して DuplicateDataModel.js にコードを保存します。

必要に応じて JavaScript スクリプトプロバイダーを読み込み、DuplicateDataModel.js 拡張機能を読み込みます。

```dbgcmd
0:000:x86> !load jsprovider.dll
0:000:x86> .scriptload C:\JSExtensions\DuplicateDataModel.js
JavaScript script successfully loaded from 'C:\JSExtensions\DuplicateDataModel.js'
```

Dx コマンドを使用して、新しい重複関数をテストします。

```dbgcmd
0: kd> dx -r1 Debugger.Sessions.First().Processes.First().Threads.Duplicate(2),d
Debugger.Sessions.First().Processes.First().Threads.Duplicate(2),d                 : [object Generator]
    [0]              : nt!DbgBreakPointWithStatus (fffff800`9696ca60) 
    [1]              : nt!DbgBreakPointWithStatus (fffff800`9696ca60) 
    [2]              : intelppm!MWaitIdle+0x18 (fffff805`0e351348) 
    [3]              : intelppm!MWaitIdle+0x18 (fffff805`0e351348) 
…
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[JavaScript 拡張機能のネイティブ デバッガー オブジェクト - デバッガー オブジェクトの詳細](native-objects-in-javascript-extensions-debugger-objects.md)

[JavaScript 拡張機能のネイティブデバッガーオブジェクト-設計とテストに関する考慮事項](native-objects-in-javascript-extensions-design-considerations.md)

[JavaScript デバッガー スクリプト](javascript-debugger-scripting.md)

[JavaScript デバッガーのスクリプト例](javascript-debugger-example-scripts.md)
