---
title: 遅延コンテキストの概要
description: 遅延コンテキストの概要
ms.assetid: a417bcc7-ca86-4853-baa3-415214da348f
keywords:
- Direct3D のバージョン 11 WDK Windows 7 の表示、遅延のコンテキストの概要
- Direct3D のバージョン 11 WDK Windows Server 2008 R2 の表示、遅延のコンテキストの概要
- 遅延コンテキストの WDK Windows 7 の表示, 概要
- WDK の Windows Server 2008 R2 のコンテキストを遅延表示, 概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d02f3300f2fe51e36e87532f3f83e49efc9b96aa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379879"
---
# <a name="introduction-to-deferred-contexts"></a>遅延コンテキストの概要


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

遅延コンテキストは、コマンドのリストを作成するアプリケーションによって使用されます。 ユーザー モードのディスプレイ ドライバーは、D3D11DDICAPS によってコマンド リストをサポートしていることを示す場合\_COMMANDLISTS\_ビルド\_の 2 つのフラグ、 [ **D3D11DDI\_スレッド処理\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11ddi_threading_caps)構造を作成し、遅延のコンテキストを操作する機能もサポートする必要があります。 ドライバーがスレッド処理の機能を示す方法の詳細については、次を参照してください。[スレッド処理をサポートしている、コマンドを一覧表示、および 3-D パイプライン](supporting-threading--command-lists--and-3-d-pipeline.md)します。 遅延コンテキストは、生成されたコマンドの一覧を実行することによって、コマンドを実行するアプリケーションが明示的に要求されるまで、遅延のコンテキストを記録するコマンドを実行することはできません、イミディ エイト コンテキストとは異なります。 作成して、遅延のコンテキストを使用して、Direct3D のバージョン 11 は、次の新しい DDI 関数を提供します。 これらの関数は、デバイス/イミディ エイト コンテキストの組み合わせを作成するために必要な情報のサブセットです。

-   [**AbandonCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_abandoncommandlist)

-   [**CalcPrivateDeferredContextSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatedeferredcontextsize)

-   [**CreateDeferredContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext)

-   [**RecycleCreateDeferredContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatedeferredcontext)

セマンティクス、 [ **CalcPrivateDeferredContextSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatedeferredcontextsize)と[ **CreateDeferredContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext)関数は他のと同様に似ていますDDI 関数。

Direct3D のランタイムが呼び出しごとに、ドライバーのドライバーの新しいハンドルとコア層ハンドルで渡します[ **CreateDeferredContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext)各遅延コンテキストを作成する関数。 遅延コンテキストごとのパイプラインの状態は、パイプラインに相当する必要がありますイミディ エイト コンテキストではあるが、状態のクリア操作が実行された後の状態します。 ドライバーがのメンバーを入力する必要があります、 [ **D3D11DDI\_DEVICEFUNCS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11ddi_devicefuncs)構造体、 **p11ContextFuncs**のメンバー [ **D3D11DDIARG\_CREATEDEFERREDCONTEXT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createdeferredcontext)構造体を指す、関数のサブセットを; 関数テーブルからランタイムを使用してそれぞれの対応する遅延コンテキスト D3D10DDI\_HDEVICE ハンドル値を**hDrvContext** D3D11DDIARG のメンバー\_CREATEDEFERREDCONTEXT は、この関数のテーブルを指定します。

ドライバーが始まる関数の提供を続行する必要があります*pfnCreate*、 *pfnOpen*、および*pfnDestroy*遅延コンテキスト。 これらの関数の遅延のコンテキストでは、残りの部分と同じスレッド処理セマンティクスを共有して、その使用を開いたり閉じたりコンテキスト ローカル DDI ハンドル」の説明に従って[を使用してローカル コンテキスト DDI ハンドル](using-context-local-ddi-handles.md)します。 始まる関数*pfnCalcPrivate*または*pfnCheck* ; 遅延のコンテキストの活用がいない、ドライバーがのメンバーを設定するため、 [ **D3D11DDI\_DEVICEFUNCS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11ddi_devicefuncs)にこれらの関数の**NULL**遅延コンテキストが作成されたとき。 遅延コンテキストのサポートの残りのデバイス機能の大半が活用されます。 ドライバーを活用していないその[ **QueryGetData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_querygetdata)関数は、ただしします。 ただし、ドライバーを活用してその[ **ResourceMap** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap)と[ **ResourceUnmap** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceunmap)関数。 ドライバーのみをサポート、 [ **ResourceIsStagingBusy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceisstagingbusy)関数と Direct3D のイミディ エイト コンテキスト ハンドルを使用して、イミディ エイト コンテキストをクランプします。 バージョン 11 リソースの新しい DDI 関数。 遅延コンテキストの活用がいない関数の完全な一覧を参照してください。[遅延コンテキスト DDI 関数を除く](excluding-ddi-functions-for-deferred-contexts.md)します。

コア、メモリに用意されているコールバック関数のレイヤー ドライバーの活用をブロックする、 **p11UMCallbacks**のメンバー [ **D3D11DDIARG\_CREATEDEFERREDCONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createdeferredcontext)を指します。 これら core レイヤーのコールバック関数では、各遅延コンテキストの状態の更新 DDI を提供します。 ただしの追加は、最も重要な[ **pfnPerformAmortizedProcessingCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_perform_amortized_processing_cb)で説明されているコールバック関数[direct3d10 から変更](changes-from-direct3d-10.md)します。

ドライバーは期待できません、 [ **pfnDisableDeferredStagingResourceDestruction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_disable_deferred_staging_resource_destruction_cb)するコールバック関数、 **pfnDisableDeferredStagingResourceDestruction**のメンバー [ **D3D11DDI\_CORELAYER\_DEVICECALLBACKS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11ddi_corelayer_devicecallbacks)を有効にするポイント。 ドライバーを呼び出す必要がある**pfnDisableDeferredStagingResourceDestruction**内、 [ **CreateDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)デバイス/イミディ エイト コンテキスト; 関数その後、ドライバーは呼び出す必要がありますしない**pfnDisableDeferredStagingResourceDestruction**新しい Direct3D のバージョン 11 DDI セマンティクスを持つ。

ドライバーの[ **RecycleCreateDeferredContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatedeferredcontext)関数する必要がありますクリア遅延のコンテキストでは、パイプラインの状態にする方法と同様のドライバーの[ **CreateDeferredContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext)遅延コンテキストのパイプラインの状態をクリアします。 ランタイムが呼び出す、ドライバーの後に[ **AbandonCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_abandoncommandlist)、 [ **CreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createcommandlist)、または[ **RecycleCreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatecommandlist)、ランタイムは、遅延のコンテキスト ハンドルを使用して、ドライバーの[ **DestroyDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroydevice)または**RecycleCreateDeferredContext**関数。 詳細については**RecycleCreateDeferredContext**を参照してください[小さなコマンドを一覧表示の最適化](supporting-command-lists.md)します。

 

 





