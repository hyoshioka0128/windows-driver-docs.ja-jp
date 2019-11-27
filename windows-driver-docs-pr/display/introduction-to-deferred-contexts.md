---
title: 遅延コンテキストの概要
description: 遅延コンテキストの概要
ms.assetid: a417bcc7-ca86-4853-baa3-415214da348f
keywords:
- Direct3D バージョン 11 WDK Windows 7 の表示、遅延コンテキスト、概要
- Direct3D バージョン 11 WDK Windows Server 2008 R2 の表示、遅延コンテキスト、概要
- 遅延コンテキスト WDK Windows 7 ディスプレイ、概要
- 遅延コンテキスト WDK Windows Server 2008 R2 ディスプレイ、概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6769a5c0f1d57664365be1e5cf5fcd6ddf9cb28
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840349"
---
# <a name="introduction-to-deferred-contexts"></a>遅延コンテキストの概要


このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

遅延コンテキストは、コマンドリストを作成するためにアプリケーションによって使用されます。 ユーザーモードの表示ドライバーによって、D3D11DDICAPS\_COMMANDLISTS\_のコマンドリストがサポートされていることが示された場合、 [**D3D11DDI\_スレッド処理\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_threading_caps)構造体の\_2 フラグを作成します。遅延コンテキストを作成および操作します。 ドライバーがスレッド処理機能を示す方法の詳細については、「[スレッド処理、コマンドリスト、および3-D パイプラインのサポート](supporting-threading--command-lists--and-3-d-pipeline.md)」を参照してください。 遅延コンテキストは、アプリケーションが生成されたコマンドリストを実行してコマンドの実行を明示的に要求するまで、遅延コンテキストレコードのコマンドを実行できないという点で、イミディエイトコンテキストとは異なります。 遅延コンテキストを作成して使用するために、Direct3D バージョン11には次の新しい DDI 関数が用意されています。 これらの関数は、デバイス/イミディエイトコンテキストの組み合わせを作成するために必要な情報のサブセットです。

-   [**AbandonCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_abandoncommandlist)

-   [**CalcPrivateDeferredContextSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatedeferredcontextsize)

-   [**CreateDeferredContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext)

-   [**RecycleCreateDeferredContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatedeferredcontext)

[**CalcPrivateDeferredContextSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatedeferredcontextsize)関数と[**CreateDeferredContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext)関数のセマンティクスは、他の同様の DDI 関数と似ています。

Direct3D ランタイムは、ドライバーの[**CreateDeferredContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext)関数を呼び出すたびに、新しいドライバーハンドルとコア層ハンドルを渡して、各遅延コンテキストを作成します。 遅延コンテキストごとのパイプラインの状態は、クリア状態の操作が実行された後に、イミディエイトコンテキストが持つパイプラインの状態と同等である必要があります。 ドライバーは、 [**D3D11DDIARG\_CREATEDEFERREDCONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createdeferredcontext)構造体の**p11ContextFuncs**メンバーが関数のサブセットを指す[**D3D11DDI\_devicefuncs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_devicefuncs)構造体のメンバーになる必要があります。一覧ランタイムは、対応する遅延コンテキスト D3D10DDI\_HDEVICE ハンドル値を使用します。この値は、D3D11DDIARG\_CREATEDEFERREDCONTEXT の**hDrvContext**メンバーがこの関数テーブルを使用して指定します。

ドライバーは、遅延コンテキストの*pfnCreate*、 *pfnopen*、および*pfnopen*で始まる関数を引き続き提供する必要があります。 これらの関数は、遅延コンテキストの残りの部分と同じスレッド処理セマンティクスを共有し、「[コンテキストローカルの Ddi ハンドルの使用](using-context-local-ddi-handles.md)」で説明されているように、コンテキストローカルの ddi ハンドルを開いたり閉じたりするために使用されます。 *PfnCalcPrivate*または*pfnCheck*で始まる関数は、遅延コンテキストでは利用されません。そのため、遅延コンテキストが作成されると、ドライバーはこれらの関数の[**D3D11DDI\_devicefuncs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_devicefuncs)のメンバーを**NULL**に設定できます。 残りのデバイス関数の大部分は、遅延コンテキストのサポートのために活用されています。 ただし、ドライバーはその[**Querygetdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_querygetdata)関数を利用しません。 ただし、ドライバーでは、 [**resourcemap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap)関数と[**resourceunmap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceunmap)関数を利用しています。 ドライバーがサポートしているのは、即時コンテキストハンドルを使用することによって、Direct3D バージョン11リソースの[**ResourceIsStagingBusy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceisstagingbusy)関数と新しい DDI 関数だけです。 遅延コンテキストで使用されない関数の完全な一覧については、「[遅延コンテキストのための DDI 関数の除外](excluding-ddi-functions-for-deferred-contexts.md)」を参照してください。

ドライバーは、メモリブロックに用意されているコア層のコールバック関数を利用します。この関数は、 [**D3D11DDIARG\_CREATEDEFERREDCONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createdeferredcontext)の**p11UMCallbacks**メンバーが指しているメモリブロックに含まれています。 これらのコアレイヤーコールバック関数は、遅延コンテキストごとに更新状態の DDI を提供します。 ただし、最も重要な点は、「 [Direct3D 10 からの変更](changes-from-direct3d-10.md)」で説明されている[**pfnPerformAmortizedProcessingCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_perform_amortized_processing_cb) callback 関数を追加することです。

ドライバーは、 [**D3D11DDI\_CORELAYER\_DEVICECALLBACKS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_corelayer_devicecallbacks)の**pfnDisableDeferredStagingResourceDestruction**メンバーが有効であることを予期していません。 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_disable_deferred_staging_resource_destruction_cb) ドライバーは、デバイス/イミディエイトコンテキストの[**CreateDevice (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数内で**pfnDisableDeferredStagingResourceDestruction**を呼び出す必要があります。その後、ドライバーは、新しい Direct3D バージョン 11 DDI セマンティクスで**pfnDisableDeferredStagingResourceDestruction**を呼び出すことはできません。

ドライバーの[**RecycleCreateDeferredContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatedeferredcontext)関数は、遅延コンテキストのパイプラインの状態をクリアする必要があります。これは、ドライバーの[**CreateDeferredContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext)が遅延コンテキストのパイプラインの状態をクリアする方法と似ています。 ランタイムは、ドライバーの[**AbandonCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_abandoncommandlist)、 [**CreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createcommandlist)、または[**RecycleCreateCommandList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatecommandlist)を呼び出した後、ドライバーの破棄[**デバイス (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroydevice)または**のいずれかを使用して遅延コンテキストハンドルを使用できます。RecycleCreateDeferredContext**関数。 **RecycleCreateDeferredContext**の詳細については、「[小さいコマンドリストの最適化](supporting-command-lists.md)」を参照してください。

 

 





