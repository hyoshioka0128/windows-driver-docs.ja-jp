---
title: コマンド リストのサポート
description: コマンド リストのサポート
ms.assetid: 7bede247-680d-4fd3-a10b-6ef63f0a88ec
keywords:
- Direct3D バージョン 11 WDK Windows 7 display、コマンドリスト
- Direct3D バージョン 11 WDK Windows Server 2008 R2 display、コマンドリスト
- コマンド一覧は、WDK Windows 7 の表示をサポートしています
- コマンド一覧は、WDK Windows 7 display、Direct3D version 11 をサポートしています。
- コマンド一覧は、WDK Windows 2008 R2 の表示をサポートしています
- コマンド一覧は、WDK Windows 2008 R2 display、Direct3D version 11 をサポートしています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d8b6bd7aa77754b836f5f9f3bf5e1215736ad6e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825674"
---
# <a name="supporting-command-lists"></a>コマンド リストのサポート


このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows にのみ適用されます。

Direct3D ランタイムは、次の Direct3D 11 DDI for コマンドリストを使用します。

-   [**CalcPrivateCommandListSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatecommandlistsize)関数は、コマンドリストのメモリのユーザーモード表示ドライバーのプライベート領域のサイズを決定します。

-   [**CreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createcommandlist)関数は、コマンドリストを作成します。

-   [**RecycleCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecommandlist)関数は、コマンドリストをリサイクルします。

-   [**RecycleCreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatecommandlist)関数は、コマンドリストを作成し、以前に使用されていない DDI ハンドルを完全に再び有効にします。

-   [**Destroycommandlist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_destroycommandlist)関数は、コマンドリストを破棄します。

-   [**RecycleDestroyCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_destroycommandlist)関数は、コマンド一覧の軽量な破棄が必要であることをドライバーに通知します。

-   [**Commandlistexecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_commandlistexecute)関数は、コマンドリストを実行します。

ドライバーの[**Commandlistexecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_commandlistexecute)、 [**CalcPrivateCommandListSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatecommandlistsize)、 [**CreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createcommandlist)、および[**destroycommandlist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_destroycommandlist)関数のセマンティクスは、他の同様の DDI 関数や API に基づいて、ほとんどの場合、対応する DDI のドキュメント。

Direct3D ランタイムは、 *CreateCommandList*パラメーターが指す[**D3D11DDIARG\_pCreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createcommandlist)構造体の**hDeferredContext**メンバーに指定されている遅延コンテキストでドライバーの[**CreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createcommandlist)または[**RecycleCreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatecommandlist)関数を正常に呼び出した後、遅延コンテキストで次の破棄シーケンスを実行します。

1.  Direct3D ランタイムは、開いているすべての遅延オブジェクトハンドルを閉じます。 これらのハンドルは、遅延コンテキストにバインドされたままになっている可能性があります。

2.  ランタイムは、遅延コンテキストを破棄します。

[**CreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createcommandlist)または[**RecycleCreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatecommandlist)の呼び出し中に、ドライバーが[状態更新 DDI コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)に対して行うすべての呼び出しは、遅延コンテキストの現在の状態を引き続き公開します。 ただし、遅延コンテキストの "終了" と破棄中は、状態更新 DDI への呼び出しによって、何もバインドされていないことが反映されます (つまり、 *CreateCommandList*または*RecycleCreateCommandList*の呼び出しの直後になります)。暗黙的にバインド解除)。

遅延コンテキストは、アプリケーションによって明示的に破棄することも、API またはドライバーによるエラー状態によって破棄することもできます。 このような場合、Direct3D ランタイムは次のシーケンスを実行します。

1.  Direct3D ランタイムは、ドライバーの[**AbandonCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_abandoncommandlist)関数を呼び出します。

2.  ランタイムは、遅延コンテキストから1つずつハンドルをバインド解除します。

3.  ランタイムは、開いている遅延オブジェクトハンドルをすべて閉じます。

4.  ランタイムは、遅延コンテキストを破棄するか、破棄します。

前のシーケンスは、即時コンテキストの破棄シーケンスに似ています。 ドライバーの[**AbandonCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_abandoncommandlist)関数を呼び出すことにより、ドライバーが任意のドライバーに状態を適用する機会を得ることができます。

ドライバーの[**Commandlistexecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_commandlistexecute)関数の呼び出し中に、ドライバーは、デバイスが作成されたときの状態と同等になるように、遅延コンテキストの状態を遷移させる必要があります。 この操作は、クリア状態の操作とも呼ばれます。 ただし、ドライバーの**Commandlistexecute**関数を呼び出しているときに、ドライバーが[状態更新 DDI コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)に対して行う呼び出しは、ドライバー関数への最後の DDI 呼び出しの間にバインドされたものの状態を反映しています。 ドライバー関数への次の DDI 呼び出しでは、ドライバーが状態更新 DDI コールバック関数に対して行うすべての呼び出しについて、現在の状態が完全に空として表示されます。これは、 **Commandlistexecute**からの暗黙的な状態遷移を反映しています。 この事実は、状態更新 DDI コールバック関数の一般的なセマンティクスと動作とは若干異なります。 ドライバーの*Setshader*関数のいずれかの呼び出し中に、ドライバーが状態更新 ddi コールバック関数を呼び出した場合、状態更新 ddi のコールバック関数は、バインドされている新しいシェーダーが既にバインドされているものとして表示されます。 状態更新 DDI のコールバック動作のこのような違いにより、 **Commandlistexecute**時の古い状態を反映するために、ドライバーの柔軟性が向上します。

Direct3D version 11 API では、コマンド一覧によってクエリが操作されていない (つまり、 [**Querybegin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_querybegin)または[**querybegin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_queryend)が呼び出されている) こと、およびコマンドリストを実行しようとしたコンテキストによってのみ "開始" されていることを確認します。 また、API は、動的リソースのマップを記録するコマンドリストが、現在マップされている同じリソースを持つコンテキストで実行されないようにします。 アプリケーションが**Finish Commandlist**関数を呼び出す前に、Direct3D ランタイムは、開始されたクエリまたはマップされたリソースを開いたままになっている任意のクエリまたは動的リソースに対して、ドライバーの**Queryend**および[**resourceunmap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceunmap) DDI 関数を呼び出します。**Finish Commandlist**は、暗黙的にクエリ範囲を終了し、マップされたリソースを解除します。

### <a name="span-idoptimization_for_small_command_listsspanspan-idoptimization_for_small_command_listsspan-optimization-for-small-command-lists"></a><span id="optimization_for_small_command_lists"></span><span id="OPTIMIZATION_FOR_SMALL_COMMAND_LISTS"></span>小さいコマンドリストの最適化

小さなメモリ量のコマンド一覧に対するメモリリサイクルの最適化は、コマンドリストの DDI 関数呼び出し間の競合を軽減し、コマンドリストに必要な呼び出し処理のオーバーヘッドを減らすために重要です。 各コマンド一覧で inherant されている処理のオーバーヘッドは重要です。 この最適化は、コマンド一覧に必要な処理オーバーヘッドが、コマンド一覧に必要な CPU 時間とメモリ領域をより大きくするコマンドリストを対象としています。 小さいメモリ量のコマンド一覧は、たとえば、CopyResource のような1つのグラフィックスコマンドです。 CopyResource に必要なメモリの量は2つのポインターです。 ただし、CopyResource では、大量のメモリを持つコマンドリストと同じ量のコマンド一覧呼び出し処理が必要になります。 小メモリ量のコマンドリストが高頻度で生成される場合、ランタイムがドライバーの[**CreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createcommandlist)、 [**destroycommandlist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_destroycommandlist)、 [**CreateDeferredContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext)、およびを[**呼び出すために必要な処理オーバーヘッド。破棄デバイス (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroydevice)関数 (遅延コンテキスト) はますます重要になります。 ここで参照されるメモリは、DDI ハンドルのメモリを含むドライバーデータ構造を保持するシステムメモリです。

ドライバーの[**RecycleCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecommandlist)関数は、ドライバーハンドルが使用されなくなった (ただし、まだ削除されていない) 場合、および以前に未使用のドライバーハンドルが再利用された場合に、ドライバーに通知する必要があります。 この通知は、コマンドリストと遅延コンテキストの両方のハンドルに適用されます。 ドライバーがリサイクルする必要があるメモリは、DDI ハンドルが指すメモリだけです。 **RecycleCommandList**の目的は、ハンドルに関連付けられているメモリをリサイクルすることですが、効率を上げるために、ドライバーは、リサイクルするメモリを選択して選択するための柔軟な柔軟性を備えています。 ドライバーは、直接コンテキストのコマンドリストハンドルがポイントするメモリ領域のサイズを変更できません。 このサイズは、 [**CalcPrivateCommandListSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatecommandlistsize)の戻り値です。 また、このドライバーは、コンテキストコマンドリストのローカルハンドルが指すメモリ領域のサイズを変更することもできません。このサイズは、 [**CalcDeferredContextHandleSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcdeferredcontexthandlesize)の戻り値です。

ドライバーの[**RecycleCreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatecommandlist)および[**RecycleCreateDeferredContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatedeferredcontext) DDI 関数は、OUTOFMEMORY HRESULT 値 E\_としてメモリ不足エラーコードを返す必要があります。 これらの関数は、 [**pfnSetErrorCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb)関数の呼び出しによって、このようなエラーコードを提供しません。 このドライバーの要件により、ランタイムは、デバイス全体の同期を使用して、これらの作成タイプドライバー関数からのコンテキストエラーを即座に監視する必要がなくなります。 これらのエラーを監視することは、小規模メモリのコマンド一覧の致命的な競合の原因になります。

ドライバーの[**RecycleDestroyCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_destroycommandlist)、 [**RecycleCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecommandlist)、 [**RecycleCreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatecommandlist)の各関数の違いは重要です。 これらの機能には、次のものがあります。

<span id="RecycleDestroyCommandList"></span><span id="recycledestroycommandlist"></span><span id="RECYCLEDESTROYCOMMANDLIST"></span>[**RecycleDestroyCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_destroycommandlist)  
ランタイムは、ドライバーの[**RecycleDestroyCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_destroycommandlist)関数を呼び出して、軽量の破棄が必要であることをドライバーに通知します。 つまり、ドライバーは、DDI コマンドリストハンドルのメモリの割り当てを解除しないようにする必要があります。 ドライバーの*RecycleDestroyCommandList*関数は、ドライバーの**destroycommandlist**関数と同様にフリースレッドです。

<span id="RecycleCommandList"></span><span id="recyclecommandlist"></span><span id="RECYCLECOMMANDLIST"></span>[**RecycleCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecommandlist)  
ドライバーの[**RecycleCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecommandlist)関数は、コマンドリストを処理するランタイムが遅延コンテキストキャッシュに戻されたことをドライバーに通知します。 次に、関数は、コマンドリストに関連付けられているメモリを遅延コンテキストキャッシュに戻す機会をドライバーに提供します。 ランタイムは、遅延コンテキストスレッドからドライバーの**RecycleCommandList**関数を呼び出します。 **RecycleCommandList** DDI 関数を使用すると、ドライバーが自身の同期を実行する必要性が軽減されます。

<span id="RecycleCreateCommandList"></span><span id="recyclecreatecommandlist"></span><span id="RECYCLECREATECOMMANDLIST"></span>[**RecycleCreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatecommandlist)  
ランタイムは、ドライバーの[**RecycleCreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatecommandlist)関数を呼び出して、以前に使用されていない DDI ハンドルを再び完全に有効にします。

これらのリサイクル DDI 関数は、小規模メモリのコマンド一覧のリソースをリサイクルするための最適化の機会を提供します。 次の擬似コードは、API から DDI への関数呼び出しのフローを通じてランタイムを実装する方法を示しています。

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

次の状態の図は、即時コンテキストの DDI コマンドリストハンドルの有効性を示しています。 緑の状態は、 [**Commandlistexecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_commandlistexecute)で使用できるハンドルを表します。

![コマンドリストハンドルの有効性の状態を示す図](images/d3d11ddi2.png)

 

 





