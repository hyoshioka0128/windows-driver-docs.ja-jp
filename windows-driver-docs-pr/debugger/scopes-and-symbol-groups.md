---
title: スコープとシンボルのグループ
description: スコープとシンボルのグループ
ms.assetid: f14b6361-9962-4fa3-bb1a-dfde066754b9
keywords:
- デバッガーのエンジンの API、記号、シンボルのグループ
- シンボルのグループ、スコープ
- デバッガーのエンジンの API、記号、スコープ
- スコープ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f56ed9cb78424c87378336925439d4eda8a5168
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366400"
---
# <a name="scopes-and-symbol-groups"></a>スコープとシンボルのグループ


## <span id="ddk_scopes_and_symbol_groups_dbx"></span><span id="DDK_SCOPES_AND_SYMBOL_GROUPS_DBX"></span>


A*シンボル グループ*効率的な操作をグループとしての記号のセットが含まれています。 シンボル グループは、作成できる、手動で設定されますと自動的に生成することができますまたはおよびに基づいてシンボルなど、ローカル変数と関数の引数の構文のスコープでの更新をします。 インターフェイス[IDebugSymbolGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugsymbolgroup)シンボルのグループを表すために使用します。

シンボルのグループを作成する 2 つの方法はあります。 によって、空のシンボルのグループが返される[ **CreateSymbolGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-createsymbolgroup)、現在の構文のスコープのシンボルのグループがによって返されると[ **GetScopeSymbolGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getscopesymbolgroup).

**注**  現在のスコープから生成されたシンボルのグループはローカル変数のスナップショットです。 ターゲットのいずれかの実行が発生した場合、シンボルが正しく不要になった可能性があります。 また、現在のスコープが変更された場合、シンボルのグループを表さなく、*現在*スコープ (ため、作成対象のスコープを表すし続けます)。

 

シンボルを使用してシンボルのグループに追加できる[ **AddSymbol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-addsymbol)を使用して削除と[ **RemoveSymbolByIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-removesymbolbyindex)または[ **RemoveSymbolByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-removesymbolbyname)します。 メソッド[ **OutputAsType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-outputastype)シンボルのデータを処理するときに、別の記号の種類を使用するデバッガーに指示します。

**注**  スコープを持つシンボルの値が正しくない可能性があります。 具体的には、コンピューターのアーキテクチャおよびコンパイラの最適化では、シンボルの値を正確に判断するからデバッガーをできない可能性があります。

 

*シンボル エントリ情報*の場所とその型を含む、シンボルの説明を示します。 モジュールのシンボルには、この情報を検索するには使用、 [ **IDebugSymbols3::GetSymbolEntryInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolentryinformation)します。 シンボルのグループ内のシンボルには、この情報を検索するには使用[ **IDebugSymbolGroup2::GetSymbolEntryInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolentryinformation)します。 参照してください[**デバッグ\_シンボル\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_symbol_entry)シンボル エントリの情報の詳細についてはします。

次の方法では、シンボルのグループでシンボルに関する情報が返されます。

-   [**GetSymbolName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolname)シンボルの名前を返します。

-   [**GetSymbolOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymboloffset)シンボルが絶対アドレスを持つ場合は、シンボルのターゲットの仮想アドレス空間で絶対アドレスを返します。

-   [**GetSymbolRegister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolregister)レジスタにシンボルが含まれている場合、シンボルを格納しているレジスタを返します。

-   [**GetSymbolSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolsize)のシンボル データのサイズを返します。

-   [**GetSymbolTypeName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymboltypename)シンボルの型の名前を返します。

-   [**GetSymbolValueText** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolvaluetext)文字列としての記号の値を返します。

使用して、その値を変更できるレジスタ内、またはデバッガー エンジンに既知のメモリ位置には、シンボルが格納されている場合[ **WriteSymbol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-writesymbol)します。

シンボルは、*親シンボル*その他の記号が含まれている場合。 たとえば、構造体には、そのメンバーが含まれています。 シンボルは、*子シンボル*別のシンボルに含まれている場合。 親と子の両方のシンボル、シンボルがあります。 各シンボルのグループは、フラットな構造を持ち、親のシンボルとその子を含みます。 各シンボルを*深さ*--シンボルのグループ内の親がないシンボルがある深さ 0、および各子シンボルの深さは 1 つの親の深さを超えています。 親のシンボルの子は、シンボルのグループに存在することができない可能性があります。 子は、シンボルのグループに存在するが、親のシンボルと呼びます*展開*します。 を追加またはシンボルのグループ内のシンボルの子を削除するには使用[ **ExpandSymbol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-expandsymbol)します。

シンボルのグループ内のシンボルの数がによって返される[ **GetNumberSymbols**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-getnumbersymbols)します。 *インデックス*シンボルとしてシンボルのグループには、id 番号は、インデックスの範囲は 0 から 1 を引いたのシンボルの数をします。 シンボルを追加または - たとえば、シンボルを展開するには--してシンボルのグループから削除するたびに、シンボルのグループ内のすべてのシンボルのインデックスを変更できます。

使用して、親子のリレーションシップに関する情報など、シンボルのパラメーターを検出できます[ **GetSymbolParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolparameters)します。 このメソッドが戻る、 [**デバッグ\_シンボル\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_symbol_parameters)構造体。

シンボルのグループ内のシンボルは、メソッドを使用して、デバッガーの出力ストリームに印刷できる[ **OutputSymbols**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-outputsymbols)します。

### <a name="span-idscopesspanspan-idscopesspanscopes"></a><span id="scopes"></span><span id="SCOPES"></span>スコープ

*現在のスコープ*、または*現在ローカル コンテキスト*、デバッガー エンジンによって公開されているローカル変数を決定します。 スコープでは、次の 3 つのコンポーネントがあります。

1.  スタック フレーム。

2.  現在の命令。

3.  レジスタのコンテキスト。

スタック フレームが呼び出し履歴の上部にある場合は、現在の手順の最後のイベントを発生させた命令です。 それ以外の場合、現在の命令は、関数呼び出しでは、[次へ] の上のスタック フレームです。

メソッド[ **GetScope** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getscope)と[ **SetScope** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-setscope)を取得し、現在のスコープを設定するために使用できます。 イベントの発生時に、現在のスコープは、イベントのスコープに設定されます。 使用して最終イベントのスコープには、現在のスコープをリセットできます[ **ResetScope**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-resetscope)します。

### <a name="span-idthread-contextspanspan-idthreadcontextspanthread-context"></a><span id="thread-context"></span><span id="THREAD_CONTEXT"></span>スレッド コンテキスト

*スレッド コンテキスト*はスレッドを切り替えるときに、Windows によって保持状態です。 レジスタのコンテキストがスレッド コンテキストではなくの一部であるいくつかのカーネル専用のプロセッサの状態があることを除き、レジスタのコンテキストに似ています。 この余分な状態は、カーネル モードのデバッグ中にレジスタとして使用できます。

スレッド コンテキストは ntddk.h で定義されているコンテキストの構造体によって表されます。 この構造体はプラットフォームに依存して、その解釈は、有効なプロセッサの種類によって異なります。 メソッド[ **GetThreadContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugadvanced3-getthreadcontext)と[ **SetThreadContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugadvanced3-setthreadcontext)を取得し、スレッド コンテキストを設定するために使用できます。

 

 





