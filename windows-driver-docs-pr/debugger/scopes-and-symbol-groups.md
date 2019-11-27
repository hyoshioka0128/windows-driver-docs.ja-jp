---
title: スコープとシンボルのグループ
description: スコープとシンボルのグループ
ms.assetid: f14b6361-9962-4fa3-bb1a-dfde066754b9
keywords:
- デバッガーエンジン API、シンボル、シンボルグループ
- シンボルグループ、スコープ
- デバッガーエンジン API、シンボル、スコープ
- スコープ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f1f96f9a37d258c9ded57e205d320dc186dc5bb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838815"
---
# <a name="scopes-and-symbol-groups"></a>スコープとシンボルのグループ


## <span id="ddk_scopes_and_symbol_groups_dbx"></span><span id="DDK_SCOPES_AND_SYMBOL_GROUPS_DBX"></span>


*シンボルグループ*には、グループとして効率的に操作するためのシンボルのセットが含まれています。 シンボルグループは、手動で作成して設定することも、ローカル変数や関数の引数など、構文のスコープ内のシンボルに基づいて自動的に生成および更新することもできます。 インターフェイス[IDebugSymbolGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsymbolgroup)は、シンボルグループを表すために使用されます。

シンボルグループを作成するには、次の2つの方法があります。 空のシンボルグループが "GetScopeSymbolGroup"[**グループ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-createsymbolgroup)によって返され、現在の構文のスコープのシンボルグループが[](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getscopesymbolgroup)によって返されます。

現在のスコープから生成されたシンボルグループがローカル変数のスナップショットである   に**注意**してください。 ターゲットで実行が行われると、シンボルが正確ではなくなる可能性があります。 また、現在のスコープが変更された場合、シンボルグループは*現在*のスコープを表すものではなくなります (これは、作成されたスコープを引き続き表すためです)。

 

シンボルは、 [**Addsymbol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-addsymbol)を使用してシンボルグループに追加したり、 [**RemoveSymbolByIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-removesymbolbyindex)または[**RemoveSymbolByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-removesymbolbyname)を使用して削除したりできます。 [**OutputAsType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-outputastype)メソッドは、シンボルのデータを処理するときに、別のシンボルの種類を使用するようにデバッガーに指示します。

スコープが指定されたシンボルの値が正確ではない   に**注意**してください。 特に、コンピューターのアーキテクチャとコンパイラの最適化により、デバッガーがシンボルの値を正確に判断できなくなる場合があります。

 

*シンボルエントリ情報*は、シンボルの場所とその型を含むシンボルの説明です。 モジュール内のシンボルに関するこの情報を検索するには、 [**IDebugSymbols3:: Getsymbol Entryinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolentryinformation)を使用します。 シンボルグループ内のシンボルに関するこの情報を検索するには、 [**IDebugSymbolGroup2:: Getsymbol Entryinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolentryinformation)を使用します。 シンボルエントリ情報の詳細については、「 [**DEBUG\_symbol\_ENTRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_symbol_entry) 」を参照してください。

次のメソッドは、シンボルグループ内のシンボルに関する情報を返します。

-   [**GetSymbolName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolname)は、シンボルの名前を返します。

-   シンボルに絶対アドレスが指定されている場合、 [**GetSymbolOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymboloffset)はシンボルのターゲットの仮想アドレス空間にある絶対アドレスを返します。

-   シンボルがレジスタに含まれている場合、 [**Getsymbol register**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolregister)はシンボルを含むレジスタを返します。

-   [**Getsymbol size**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolsize)は、シンボルのデータのサイズを返します。

-   [**Getsymbol typename**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymboltypename)は、シンボルの型の名前を返します。

-   [**GetSymbolValueText**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolvaluetext)は、記号の値を文字列として返します。

シンボルがレジスタまたはデバッガーエンジンによって認識されるメモリ位置に格納されている場合、その値は[**WriteSymbol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-writesymbol)を使用して変更できます。

記号は、他の記号が含まれている場合は*親シンボル*です。 たとえば、構造体にメンバーが含まれているとします。 シンボルは、別のシンボルに含まれている場合は、*子シンボル*です。 記号は、親と子の両方のシンボルにすることができます。 各シンボルグループにはフラット構造があり、親シンボルとその子が含まれています。 各シンボルの*深さ*は、記号グループの親を持たない深さが0で、各子シンボルの深さが親の深さよりも1大きくなっています。 親シンボルの子は、シンボルグループに含まれている場合と存在しない場合があります。 子がシンボルグループに存在する場合、親シンボルは "*展開*済み" と呼ばれます。 シンボルグループ内の記号の子を追加または削除するには、 [**Expandsymbol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-expandsymbol)を使用します。

シンボルグループ内の記号の数は、 [**Getnumber シンボル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-getnumbersymbols)によって返されます。 シンボルグループ内のシンボルの*インデックス*は識別番号です。インデックスの範囲は0から、記号から1を引いた数です。 シンボルを追加したり、シンボルグループから削除したりするたびに (たとえば、シンボルを展開するなど)、シンボルグループ内のすべてのシンボルのインデックスが変更されることがあります。

親子関係に関する情報を含むシンボルパラメーターは、 [**Getsymbol parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolparameters)を使用して見つけることができます。 このメソッドは、[**デバッグ\_シンボル\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_symbol_parameters)構造体を返します。

シンボルグループ内のシンボルは、 [**outputsymbols**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-outputsymbols)メソッドを使用して、デバッガーの出力ストリームに出力できます。

### <a name="span-idscopesspanspan-idscopesspanscopes"></a><span id="scopes"></span><span id="SCOPES"></span>スコープ

*現在のスコープ*または*現在のローカルコンテキスト*によって、デバッガーエンジンによって公開されるローカル変数が決まります。 スコープには、次の3つのコンポーネントがあります。

1.  スタックフレーム。

2.  現在の命令。

3.  レジスタコンテキスト。

スタックフレームが呼び出し履歴の一番上にある場合、現在の命令は最後のイベントが発生した命令になります。 それ以外の場合、現在の命令は、次に大きいスタックフレームが生成された関数呼び出しになります。

[**GetScope**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getscope)メソッドと[**setscope**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-setscope)メソッドを使用して、現在のスコープを取得して設定できます。 イベントが発生すると、現在のスコープがイベントのスコープに設定されます。 現在のスコープは、 [**Resetscope**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-resetscope)を使用して、最後のイベントのスコープにリセットできます。

### <a name="span-idthread-contextspanspan-idthread_contextspanthread-context"></a><span id="thread-context"></span><span id="THREAD_CONTEXT"></span>スレッドコンテキスト

*スレッドコンテキスト*は、スレッドを切り替えるときに Windows によって保持される状態です。 これはレジスタコンテキストに似ていますが、レジスタコンテキストの一部であるものの、スレッドコンテキストの一部ではないカーネル専用プロセッサ状態がある点が異なります。 この追加の状態は、カーネルモードのデバッグ中にレジスタとして使用できます。

スレッドコンテキストは、ntddk で定義されているコンテキスト構造によって表されます。 この構造体はプラットフォームに依存し、その解釈は、有効なプロセッサの種類によって異なります。 [**Getthreadcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-getthreadcontext)メソッドと[**setthreadcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-setthreadcontext)メソッドを使用して、スレッドコンテキストを取得および設定できます。

 

 





