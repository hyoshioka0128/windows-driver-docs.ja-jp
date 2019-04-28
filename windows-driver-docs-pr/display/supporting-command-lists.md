---
title: コマンド リストのサポート
description: コマンド リストのサポート
ms.assetid: 7bede247-680d-4fd3-a10b-6ef63f0a88ec
keywords:
- Direct3D のバージョン 11 WDK Windows 7 の表示、コマンドを一覧表示します。
- Direct3D のバージョン 11 WDK Windows Server 2008 R2 の表示、コマンドを一覧表示します。
- コマンド一覧 WDK Windows 7 のサポートを表示をします
- コマンドには、WDK の Windows 7 のサポートの表示、Direct3D のバージョン 11 が一覧表示します
- コマンド一覧は、WDK Windows 2008 R2 の表示をサポートします。
- コマンド一覧は、WDK Windows 2008 R2 の表示、Direct3D のバージョン 11 をサポートします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9f5af08f8007d15b2dfe477def41abcf4864fc5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375900"
---
# <a name="supporting-command-lists"></a>コマンド リストのサポート


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows にのみ適用されます。

Direct3D のランタイムは、コマンド一覧の次の Direct3D 11 DDI を使用します。

-   [ **CalcPrivateCommandListSize** ](https://msdn.microsoft.com/library/windows/hardware/ff538278)関数は、コマンドの一覧については、メモリのユーザー モードのディスプレイ ドライバーのプライベート領域のサイズを決定します。

-   [ **CreateCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff540602)関数は、コマンドの一覧を作成します。

-   [ **RecycleCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff569237)関数は、コマンドの一覧をリサイクルします。

-   [ **RecycleCreateCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff569238)関数は、コマンドの一覧を作成し、により、以前使用されていない DDI ハンドルをもう一度完全に有効です。

-   [ **DestroyCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff552748)関数は、コマンドの一覧を破棄します。

-   [ **RecycleDestroyCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff552748)関数は、コマンドの一覧の軽量の破棄が必要である、ドライバーに通知します。

-   [ **CommandListExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff539476)関数は、コマンドの一覧を実行します。

ドライバーのためのセマンティクス[ **CommandListExecute**](https://msdn.microsoft.com/library/windows/hardware/ff539476)、 [ **CalcPrivateCommandListSize**](https://msdn.microsoft.com/library/windows/hardware/ff538278)、 [ **CreateCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff540602)、および[ **DestroyCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff552748)関数はほとんどの場合、その他の同様の DDI 機能と API に基づく、一目瞭然対応する DDI のドキュメントです。

Direct3D の後にランタイムが正常に呼び出す、ドライバーの[ **CreateCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff540602)または[ **RecycleCreateCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff569238)関数遅延のコンテキストで指定されている、 **hDeferredContext**のメンバー、 [ **D3D11DDIARG\_CREATECOMMANDLIST** ](https://msdn.microsoft.com/library/windows/hardware/ff542040)構造体*pCreateCommandList*パラメーターが指す、Direct3D ランタイムは、遅延のコンテキストで次の破棄の順序を実行します。

1.  Direct3D ランタイムは、遅延オブジェクトのすべての開いているハンドルを「閉じる」。 これらのハンドルが遅延のコンテキストにバインドされている表示も可能性がありますに注意してください。

2.  ランタイムは、遅延のコンテキストを破棄します。

呼び出し中に[ **CreateCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff540602)または[ **RecycleCreateCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff569238)ドライバーが、に呼び出し[DDI コールバック関数の状態の更新](https://msdn.microsoft.com/library/windows/hardware/ff552885)遅延コンテキストの現在の状態を引き出したりする続行します。 ただし、"closing"と遅延のコンテキストの破棄、中に状態更新 DDI への呼び出しを反映 nothing がバインドされている (つまり、呼び出しの後すぐに*CreateCommandList*または*RecycleCreateCommandList*、暗黙的にバインドされているすべてのものが)。

API またはドライバーによって、アプリケーションによって明示的にまたはエラー状態が原因のいずれか遅延コンテキストを破棄もできます。 このような場合は、Direct3D のランタイムは、次のシーケンスを実行します。

1.  Direct3D ランタイムが呼び出す、ドライバーの[ **AbandonCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff538199)関数。

2.  ランタイムは、1 つずつの遅延のコンテキストからのハンドルをバインド解除します。

3.  ランタイムは、遅延オブジェクトのすべての開いているハンドルを「閉じる」。

4.  ランタイムか recyles または遅延のコンテキストを破棄します。

上記の順序は、イミディ エイト コンテキストの破棄の順序に似ています。 ドライバーへの呼び出し[ **AbandonCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff538199)関数は、どのようなドライバーを希望に状態を適用するドライバーの機会を提供します。

呼び出し中に、ドライバーの[ **CommandListExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff539476)関数の場合、ドライバーは、デバイスが作成されたときの状態にするようにする遅延のコンテキストの状態を変更する必要があります。 この操作は、状態のクリア操作でとも呼ばれます。 呼び出し中に、ドライバーの**CommandListExecute**関数、ただし、すべての呼び出しを発行するドライバー、 [DDI コールバック関数の状態の更新](https://msdn.microsoft.com/library/windows/hardware/ff552885)も中にバインドされた内容の状態を反映、最後の DDI ドライバー関数の呼び出しです。 ドライバー関数に次の DDI 呼び出し中に状態更新 DDI コールバック関数に、ドライバーは、すべての呼び出しを表示する現在の状態と完全に空から暗黙的に状態遷移を反映する**CommandListExecute**. このファクトは、一般的なセマンティクスの状態更新 DDI のコールバック関数の動作と若干異なります。 ドライバーでの呼び出し中に、ドライバーのいずれかの状態更新 DDI のコールバック関数が呼び出されてかどうか*SetShader*関数、状態更新 DDI のコールバック関数が表示に既にバインドされている新しいシェーダーにバインドされています。 この食い違い DDI コールバック動作の状態更新の中に以前の状態を反映するようにドライバーに柔軟性を提供する**CommandListExecute**します。

Direct3D のバージョン 11 API により、クエリが操作されているどちらもありません (つまり、必要がある[ **QueryBegin** ](https://msdn.microsoft.com/library/windows/hardware/ff569214)または[ **QueryEnd** ](https://msdn.microsoft.com/library/windows/hardware/ff569217)の呼び出し) コマンドの一覧でされてのみ「が開始した」コマンド リストを実行しようとするコンテキストとします。 API は、同じリソースが現在割り当てられているコンテキストで動的リソースのマップを記録するコマンドの一覧が実行されていないことも確認します。 アプリケーションを呼び出す前に、 **FinishCommandList**関数、Direct3D ランタイムは、ドライバーの**QueryEnd**と[ **ResourceUnmap** ](https://msdn.microsoft.com/library/windows/hardware/ff569495)DDI 関数クエリまたはまだ開始されてクエリを保持する動的リソースまたはマッピングされたリソースのため、開く**FinishCommandList**暗黙的にクエリの範囲を終了し、マッピングされたリソースの割り当てを解除します。

### <a name="span-idoptimizationforsmallcommandlistsspanspan-idoptimizationforsmallcommandlistsspan-optimization-for-small-command-lists"></a><span id="optimization_for_small_command_lists"></span><span id="OPTIMIZATION_FOR_SMALL_COMMAND_LISTS"></span> 小規模なコマンド一覧の最適化

小規模メモリの量のコマンド一覧のメモリのリサイクルの最適化が重要なは、コマンド一覧 DDI 関数呼び出しの間で競合を減らすと、コマンド一覧の必要な呼び出しの処理のオーバーヘッドを削減できます。 各コマンドの一覧で inherant は処理のオーバーヘッドは重要です。 この最適化は、コマンドの一覧に必要な処理オーバーヘッドがコマンドの一覧に必要な CPU 時間とメモリ容量よりも優位コマンドの一覧。 小規模メモリの量のコマンドの一覧はたとえば、CopyResource などの単一のグラフィックス コマンドです。 CopyResource に必要なメモリの量は、2 つのポインターです。 ただし、CopyResource 同量のメモリ量では大規模なコマンドのリストとして処理コマンド一覧の呼び出しも必要です。 ドライバーの呼び出しに、その処理のオーバーヘッドが、ランタイムの必要な高頻度で小さなメモリサイズ コマンド一覧が生成されると、 [ **CreateCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff540602)、 [ **DestroyCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff552748)、 [ **CreateDeferredContext**](https://msdn.microsoft.com/library/windows/hardware/ff540622)、および[ **DestroyDevice(D3D10)**](https://msdn.microsoft.com/library/windows/hardware/ff552768) (コンテキストの遅延) の機能がますます重要になります。 ここでは、メモリは、DDI ハンドルのメモリを含むデータ構造では、ドライバーを保持するシステム メモリです。

ドライバーの[ **RecycleCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff569237)関数する必要がありますドライバーとドライバーのハンドルはアウト規約を参照してください (ただし、まだ削除されていない)、および通知と以前使用されていないドライバーのハンドルが再利用されます。 この通知は、コマンド一覧と遅延コンテキストの両方のハンドルに適用されます。 ドライバーをリサイクルする必要がありますのみメモリは、DDI へのポインターを処理するメモリです。 目的を while **RecycleCommandList**効率、ドライバーが完全な柔軟性をリサイクルするには、どのメモリを選択して、ハンドルに関連付けられているメモリを再利用します。 ドライバーは、イミディ エイト コンテキスト コマンドの一覧がポイントを処理するメモリの領域のサイズを変更できません。 このサイズの戻り値は、 [ **CalcPrivateCommandListSize**](https://msdn.microsoft.com/library/windows/hardware/ff538278)します。 また、ドライバーは、コンテキストのコマンド一覧のローカル ポイントの処理をメモリの領域のサイズを変更できません。このサイズの戻り値は、 [ **CalcDeferredContextHandleSize**](https://msdn.microsoft.com/library/windows/hardware/ff538272)します。

ドライバーの[ **RecycleCreateCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff569238)と[ **RecycleCreateDeferredContext** ](https://msdn.microsoft.com/library/windows/hardware/ff569239) DDI 関数は、メモリ不足を返す必要がありますエラー コードとして E\_OUTOFMEMORY HRESULT 値。 これらの関数の呼び出しを通じてこのようなエラー コードを指定しない、 [ **pfnSetErrorCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568929)関数。 このドライバーの要件は、ランタイムをデバイス全体の同期を使用して、これらの型が作成ドライバー関数からイミディ エイト コンテキスト エラーを監視することを防ぎます。 これらの監視のエラーは、小規模メモリの量のコマンド一覧の壊滅的な競合の原因になります。

ドライバーの間の違い[ **RecycleDestroyCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff552748)、 [ **RecycleCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff569237)、および[ **RecycleCreateCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff569238)関数は重要です。 その機能を以下に示します。

<span id="RecycleDestroyCommandList"></span><span id="recycledestroycommandlist"></span><span id="RECYCLEDESTROYCOMMANDLIST"></span>[**RecycleDestroyCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff552748)  
ランタイムが呼び出す、ドライバーの[ **RecycleDestroyCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff552748)軽量の破棄が必要である、ドライバーに通知します。 つまり、ドライバーする必要がありますいないまだ割り当てを解除 DDI コマンド一覧ハンドルのメモリ。 ドライバーの*RecycleDestroyCommandList*関数は、ドライバーのと同じようにフリー スレッド**DestroyCommandList**関数。

<span id="RecycleCommandList"></span><span id="recyclecommandlist"></span><span id="RECYCLECOMMANDLIST"></span>[**RecycleCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff569237)  
ドライバーの[ **RecycleCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff569237)関数は、ランタイムが遅延コンテキスト キャッシュに再度コマンド一覧のハンドルを統合することをドライバーに通知します。 関数には、ドライバーを遅延コンテキスト キャッシュには、コマンドの一覧に関連付けられているメモリを統合する機会を提供します。 ランタイムが呼び出す、ドライバーの**RecycleCommandList**遅延コンテキストのスレッドからの関数。 **RecycleCommandList** DDI 関数は、ドライバーが、独自の同期を実行するための必要性を軽減します。

<span id="RecycleCreateCommandList"></span><span id="recyclecreatecommandlist"></span><span id="RECYCLECREATECOMMANDLIST"></span>[**RecycleCreateCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff569238)  
ランタイムが呼び出す、ドライバーの[ **RecycleCreateCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff569238)関数をもう一度完全に有効にするには、以前使用されていない DDI ハンドルにします。

DDI 関数をリサイクルこれらは、小規模メモリの量のコマンド一覧のリソースをリサイクルする最適化の機会を提供します。 次の疑似コードは、フロー DDI API から関数呼び出しのランタイムの実装を示しています。

```cpp
::FinishCommandList()
{
  // Empty InterlockedSList, integrating into the cache
  Loop { DC::pfnRecycleCommandList }

  If (Previously Destroyed CommandList Available)
 { IC::pfnRecycleCreateCommandList }
 else
  {
    IC::pfnCalcPrivateCommandListSize
    IC::pfnCreateCommandList
    IC::pfnCalcDeferredContextHandleSize(D3D11DDI_HT_COMMANDLIST)
  }

  Loop { DC::pfnDestroy* (context-local handle destroy) }

  IC::pfnRecycleCreateDeferredContext
}
...
Sporadic: DC::pfnCreate* (context-local open during first-bind per CommandList)

CommandList::Destroy()
{
  // If DC still alive, almost always recycle:
  If (DC still alive)
 { IC::pfnRecycleDestroyCommandList }
  Else
 { IC::pfnDestroyCommandList }
  // Add to InterlockedSList
}
```

次の状態図は、イミディ エイト コンテキスト DDI コマンド一覧ハンドルの有効性を示します。 緑色の状態で使用できるハンドルを表す[ **CommandListExecute**](https://msdn.microsoft.com/library/windows/hardware/ff539476)します。

![コマンド リストのハンドルの有効性の状態を示す図](images/d3d11ddi2.png)

 

 





