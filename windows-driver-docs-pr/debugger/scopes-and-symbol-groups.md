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
ms.openlocfilehash: 9937d4ccbf7a6472c935d116e1a94f255c0cc134
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550458"
---
# <a name="scopes-and-symbol-groups"></a>スコープとシンボルのグループ


## <span id="ddk_scopes_and_symbol_groups_dbx"></span><span id="DDK_SCOPES_AND_SYMBOL_GROUPS_DBX"></span>


A*シンボル グループ*効率的な操作をグループとしての記号のセットが含まれています。 シンボル グループは、作成できる、手動で設定されますと自動的に生成することができますまたはおよびに基づいてシンボルなど、ローカル変数と関数の引数の構文のスコープでの更新をします。 インターフェイス[IDebugSymbolGroup](https://msdn.microsoft.com/library/windows/hardware/ff550838)シンボルのグループを表すために使用します。

シンボルのグループを作成する 2 つの方法はあります。 によって、空のシンボルのグループが返される[ **CreateSymbolGroup**](https://msdn.microsoft.com/library/windows/hardware/ff540093)、現在の構文のスコープのシンボルのグループがによって返されると[ **GetScopeSymbolGroup**](https://msdn.microsoft.com/library/windows/hardware/ff548280).

**注**  現在のスコープから生成されたシンボルのグループはローカル変数のスナップショットです。 ターゲットのいずれかの実行が発生した場合、シンボルが正しく不要になった可能性があります。 また、現在のスコープが変更された場合、シンボルのグループを表さなく、*現在*スコープ (ため、作成対象のスコープを表すし続けます)。

 

シンボルを使用してシンボルのグループに追加できる[ **AddSymbol**](https://msdn.microsoft.com/library/windows/hardware/ff537925)を使用して削除と[ **RemoveSymbolByIndex** ](https://msdn.microsoft.com/library/windows/hardware/ff554510)または[ **RemoveSymbolByName**](https://msdn.microsoft.com/library/windows/hardware/ff554518)します。 メソッド[ **OutputAsType** ](https://msdn.microsoft.com/library/windows/hardware/ff553191)シンボルのデータを処理するときに、別の記号の種類を使用するデバッガーに指示します。

**注**  スコープを持つシンボルの値が正しくない可能性があります。 具体的には、コンピューターのアーキテクチャおよびコンパイラの最適化では、シンボルの値を正確に判断するからデバッガーをできない可能性があります。

 

*シンボル エントリ情報*の場所とその型を含む、シンボルの説明を示します。 モジュールのシンボルには、この情報を検索するには使用、 [ **IDebugSymbols3::GetSymbolEntryInformation**](https://msdn.microsoft.com/library/windows/hardware/ff548484)します。 シンボルのグループ内のシンボルには、この情報を検索するには使用[ **IDebugSymbolGroup2::GetSymbolEntryInformation**](https://msdn.microsoft.com/library/windows/hardware/ff548487)します。 参照してください[**デバッグ\_シンボル\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff541662)シンボル エントリの情報の詳細についてはします。

次の方法では、シンボルのグループでシンボルに関する情報が返されます。

-   [**GetSymbolName** ](https://msdn.microsoft.com/library/windows/hardware/ff549121)シンボルの名前を返します。

-   [**GetSymbolOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff549135)シンボルが絶対アドレスを持つ場合は、シンボルのターゲットの仮想アドレス空間で絶対アドレスを返します。

-   [**GetSymbolRegister** ](https://msdn.microsoft.com/library/windows/hardware/ff549165)レジスタにシンボルが含まれている場合、シンボルを格納しているレジスタを返します。

-   [**GetSymbolSize** ](https://msdn.microsoft.com/library/windows/hardware/ff549169)のシンボル データのサイズを返します。

-   [**GetSymbolTypeName** ](https://msdn.microsoft.com/library/windows/hardware/ff549188)シンボルの型の名前を返します。

-   [**GetSymbolValueText** ](https://msdn.microsoft.com/library/windows/hardware/ff549201)文字列としての記号の値を返します。

使用して、その値を変更できるレジスタ内、またはデバッガー エンジンに既知のメモリ位置には、シンボルが格納されている場合[ **WriteSymbol**](https://msdn.microsoft.com/library/windows/hardware/ff561457)します。

シンボルは、*親シンボル*その他の記号が含まれている場合。 たとえば、構造体には、そのメンバーが含まれています。 シンボルは、*子シンボル*別のシンボルに含まれている場合。 親と子の両方のシンボル、シンボルがあります。 各シンボルのグループは、フラットな構造を持ち、親のシンボルとその子を含みます。 各シンボルを*深さ*--シンボルのグループ内の親がないシンボルがある深さ 0、および各子シンボルの深さは 1 つの親の深さを超えています。 親のシンボルの子は、シンボルのグループに存在することができない可能性があります。 子は、シンボルのグループに存在するが、親のシンボルと呼びます*展開*します。 を追加またはシンボルのグループ内のシンボルの子を削除するには使用[ **ExpandSymbol**](https://msdn.microsoft.com/library/windows/hardware/ff543271)します。

シンボルのグループ内のシンボルの数がによって返される[ **GetNumberSymbols**](https://msdn.microsoft.com/library/windows/hardware/ff547975)します。 *インデックス*シンボルとしてシンボルのグループには、id 番号は、インデックスの範囲は 0 から 1 を引いたのシンボルの数をします。 シンボルを追加または - たとえば、シンボルを展開するには--してシンボルのグループから削除するたびに、シンボルのグループ内のすべてのシンボルのインデックスを変更できます。

使用して、親子のリレーションシップに関する情報など、シンボルのパラメーターを検出できます[ **GetSymbolParameters**](https://msdn.microsoft.com/library/windows/hardware/ff549146)します。 このメソッドが戻る、 [**デバッグ\_シンボル\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff541673)構造体。

シンボルのグループ内のシンボルは、メソッドを使用して、デバッガーの出力ストリームに印刷できる[ **OutputSymbols**](https://msdn.microsoft.com/library/windows/hardware/ff553264)します。

### <a name="span-idscopesspanspan-idscopesspanscopes"></a><span id="scopes"></span><span id="SCOPES"></span>スコープ

*現在のスコープ*、または*現在ローカル コンテキスト*、デバッガー エンジンによって公開されているローカル変数を決定します。 スコープでは、次の 3 つのコンポーネントがあります。

1.  スタック フレーム。

2.  現在の命令。

3.  レジスタのコンテキスト。

スタック フレームが呼び出し履歴の上部にある場合は、現在の手順の最後のイベントを発生させた命令です。 それ以外の場合、現在の命令は、関数呼び出しでは、[次へ] の上のスタック フレームです。

メソッド[ **GetScope** ](https://msdn.microsoft.com/library/windows/hardware/ff548270)と[ **SetScope** ](https://msdn.microsoft.com/library/windows/hardware/ff556773)を取得し、現在のスコープを設定するために使用できます。 イベントの発生時に、現在のスコープは、イベントのスコープに設定されます。 使用して最終イベントのスコープには、現在のスコープをリセットできます[ **ResetScope**](https://msdn.microsoft.com/library/windows/hardware/ff554577)します。

### <a name="span-idthread-contextspanspan-idthreadcontextspanthread-context"></a><span id="thread-context"></span><span id="THREAD_CONTEXT"></span>スレッド コンテキスト

*スレッド コンテキスト*はスレッドを切り替えるときに、Windows によって保持状態です。 レジスタのコンテキストがスレッド コンテキストではなくの一部であるいくつかのカーネル専用のプロセッサの状態があることを除き、レジスタのコンテキストに似ています。 この余分な状態は、カーネル モードのデバッグ中にレジスタとして使用できます。

スレッド コンテキストは ntddk.h で定義されているコンテキストの構造体によって表されます。 この構造体はプラットフォームに依存して、その解釈は、有効なプロセッサの種類によって異なります。 メソッド[ **GetThreadContext** ](https://msdn.microsoft.com/library/windows/hardware/ff549291)と[ **SetThreadContext** ](https://msdn.microsoft.com/library/windows/hardware/ff556829)を取得し、スレッド コンテキストを設定するために使用できます。

 

 





