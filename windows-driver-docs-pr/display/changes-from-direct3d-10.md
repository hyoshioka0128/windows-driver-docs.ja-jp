---
title: Direct3D 10 からの変更点
description: Direct3D 10 からの変更点
ms.assetid: 014a5e44-f8c4-45c0-96e8-d82f37b8b28d
keywords:
- Direct3d version 11 WDK Windows 7 display、Direct3D version 10 からの変更
- Direct3D version 11 WDK Windows Server 2008 R2 display、Direct3D version 10 からの変更
- Direct3D version 10 WDK Windows 7 display
- Direct3d バージョン 10 WDK Windows 7 display、変更 (Direct3D バージョン 11)
- Direct3D バージョン 10 WDK Windows Server 2008 R2 ディスプレイ、変更 (Direct3D バージョン 11)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 532d5962412e654aa23a030271edea2e6f9d2dfe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839813"
---
# <a name="changes-from-direct3d-10"></a>Direct3D 10 からの変更点


このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

以下のセクションでは、Direct3D 11 が Direct3D 10 からどのように変更されたかについて説明します。

### <a name="driver-callback-functions-to-kernel-mode-services"></a>ドライバーコールバック関数からカーネルモードサービスへ

ランタイムがユーザーモードの display driver の[**CreateDevice (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数を呼び出したときに、Direct3D version 11 runtime によって[**D3DDDI\_DEVICECALLBACKS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicecallbacks)構造体に提供されるデバイス固有のコールバック関数は、ドライバーを分離します。カーネルハンドルおよびカーネル関数シグネチャから。 Direct3D version 11 ランタイムは、コールバックセマンティクスを変更します。したがって、フリースレッドモードの操作をサポートするためのコールバック関数の実装では、以前の Direct3D バージョンのランタイムは、のフリースレッドモードをサポートしていませんでした。運用. フリースレッドモード操作の規則は、ドライバーがフリースレッドモード (D3D11DDICAPS\_フリースレッド) をサポートしていることを示すと、適用されます。それ以外の場合は、以前に制限の厳しいルールが適用されます。 ドライバーがフリースレッドモードのサポートを示す方法の詳細については、「[スレッドとコマンドリスト](supporting-threading--command-lists--and-3-d-pipeline.md)」を参照してください。 Direct3D バージョン11では、次の制限があります。

-   HCONTEXT に対して一度に処理できるスレッドは1つだけです。 現在 HCONTEXT を使用している既存のコールバック関数は、 [**Pfnare cb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)、 [**pfnpresentcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)、 [*pfnEscapeCb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_escapecb)、 [**pfndestroycontextcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroycontextcb)、 [**pfnpresentcb objectcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_waitforsynchronizationobjectcb)、および[**Pfnsignal同期 Objectcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobjectcb)。 したがって、複数のスレッドがこれらのコールバック関数を呼び出し、同じ HCONTEXT を使用する場合、ドライバーはコールバック関数への呼び出しを同期する必要があります。 これらのコールバック関数は、直接コンテキストを操作するスレッドからのみ呼び出されることが多いため、この要件を満たすことは非常に自然です。

-   ドライバーは、これらのドライバー関数を呼び出したのと同じスレッドを使用して、次のドライバー関数の呼び出し中にのみ、次のコールバック関数を呼び出す必要があります。

    <span id="pfnAllocateCb"></span><span id="pfnallocatecb"></span><span id="PFNALLOCATECB"></span>[**pfnAllocateCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)  
    ドライバーは、共有リソースが作成されるときに、ドライバーの[**Createresource (D3D11)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)関数を呼び出したスレッドで[*Pfnallocatecb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)を呼び出す必要があります。 デバイスとの通常の非共有割り当ては完全にフリースレッドです。

    <span id="pfnPresentCb"></span><span id="pfnpresentcb"></span><span id="PFNPRESENTCB"></span>[**Pfnの持つ Cb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)  
    ドライバーは、ドライバーの実行中の[**dxgi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)関数の呼び出し中にのみ、 [**pfnを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)呼び出す必要があります。

    <span id="pfnSetDisplayModeCb"></span><span id="pfnsetdisplaymodecb"></span><span id="PFNSETDISPLAYMODECB"></span>[**pfnSetDisplayModeCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setdisplaymodecb)  
    ドライバーは、ドライバーの[**Setdisplaymodedxgi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_1_ddi_base_functions)関数の呼び出し中にのみ、 [**Pfnsetdisplaymodecb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setdisplaymodecb)を呼び出す必要があります。

    <span id="pfnRenderCb"></span><span id="pfnrendercb"></span><span id="PFNRENDERCB"></span>[**pfnRenderCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)  
    ドライバーは、ドライバーの[**Flush (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_flush)関数を呼び出したスレッドで[*Pfnrendercb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)を呼び出す必要があります。 この制限は、HCONTEXT の制限が原因で非常に自然です。

-   [*Pfndeallocatecb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocatecb)コールバック関数は、ドライバーがほとんどの種類のリソースに対して[**DESTROYRESOURCE (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyresource)関数から制御を返す前に*pfndeallocatecb*を呼び出す必要がないため、特別に記述されています。 DestroyResource (D3D10) はフリースレッド関数であるため、ドライバーは、既存の直接コンテキスト参照が残っていないことを効率的に確認できるようになるまで、オブジェクトの破棄を延期する必要があります (つまり、ドライバーは、前に[**Pfnrendercb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)を呼び出す必要があります。*Pfndeallocatecb*)。 この制限は、共有リソースまたは HRESOURCE を使用する他のコールバック関数にも適用され、 [**Pfnallocatecb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)での hresource の使用を補完します。 ただし、この制限は、プライマリには適用されません。 プライマリ例外の詳細については、「[プライマリ例外](#primary-exceptions)」を参照してください。 一部のアプリケーションは同期破棄のような外観を必要とする場合があるため、ドライバーは、[**フラッシュ (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_flush)関数の呼び出し中に、以前に破棄された共有リソースに対して、 *Pfndeallocatecb*を呼び出す必要があります。 また、フラッシュ (D3D10) 関数の呼び出し中に、ドライバーは、以前に破棄されたオブジェクト (パイプラインを停止しないオブジェクトのみ) をクリーンアップする必要があります。ドライバーは、このようなメカニズムを必要とする可能性のある少数のアプリケーションに対して、遅延破棄されたオブジェクトをクリーンアップするための公式メカニズムとして、ランタイムがフラッシュ (D3D10) を呼び出すようにする必要があります。 このメカニズムの詳細については、「[遅延破棄とフラッシュ」 (D3D10)](#deferred-destruction-and-flush-d3d10)を参照してください。 ドライバーは、ドライバーの[**Destroydevice (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroydevice)関数がクリーンアップ中に戻る前に、破棄が遅延されたオブジェクトが完全に破棄されていることを確認する必要もあります。

### <a name="deprecate-ability-to-allow-modification-of-free-threaded-ddis"></a>フリースレッド DDIs の変更を許可する機能を廃止する

Direct3D バージョン11では、ディスプレイデバイスの API レベルの概念と直接のコンテキストは、ディスプレイデバイスの従来の概念によって、引き続き DDI レベルでバンドルされます。 この表示デバイスとイミディエイトコンテキストのバンドルは、旧バージョンの DDIs ( [Direct3D バージョン 10 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)など) との互換性を最大化し、DDIs の複数のバージョンを通じて複数のバージョンの api をサポートするときにドライバーの変化を減らします。 ただし、このように表示デバイスとイミディエイトコンテキストをバンドルすると、スレッドドメインが非常に明示的ではないため、より複雑な DDI になります。 代わりに、複数のインターフェイスとそのインターフェイス内の関数のスレッド処理の要件を理解するために、ドライバー開発者はドキュメントを参照する必要があります。

Direct3D version 11 API の主な機能は、複数のスレッドが同時に create および destroy 関数に入ることができることです。 このような機能は、ドライバーが create および destroy の関数テーブルポインターをスワップアウトできるようにすることと互換性がありません。これは、 [**D3D10DDI\_devicefuncs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_devicefuncs)と D3D10 で指定されている関数の Direct3D バージョン 10 DDI セマンティクスです[ **\_1DDI\_DEVICEFUNCS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_1ddi_devicefuncs)が許可されています。 したがって、ドライバーが作成用の関数ポインター ([**CreateDevice (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)) を返した後、ドライバーが Direct3D VERSION 11 DDI で実行されている場合、ドライバーは、これらの特定の関数ポインターを変更することによって動作を変更しないようにする必要があります。ドライバーは、DDI スレッドをサポートしています。 この制限は、 *pfnCreate*、 *pfnopen*、 *pfnopen*、 *pfnCalcPrivate*、および*pfnCheck*で始まるすべてのデバイス関数に適用されます。 デバイス関数の残りの部分はすべて、イミディエイトコンテキストに厳密に関連付けられています。 1つのスレッドは一度に直接コンテキストを操作するので、ドライバーが直接コンテキスト関数テーブルのエントリをホットスワップできるように、適切に定義されています。

### <a name="pfnrendercb-versus-pfnperformamortizedprocessingcb"></a>pfnRenderCb と pfnPerformAmortizedProcessingCb

Direct3D version 10 API 関数は、Direct3D ランタイムの[**Pfnrendercb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)カーネルコールバック関数をフックして、償却処理を実行します (つまり、すべての API 関数呼び出しに対して特定の操作を実行するのではなく、償却を実行したドライバーさまざまな API 関数呼び出しに対する操作。 API は通常、この機会を使用して、高い透かしを除去し、遅延オブジェクトの破棄キューをフラッシュします。

カーネルコールバック関数をドライバーで可能な限りフリースレッドとして使用できるようにするため、ドライバーが Direct3D バージョン 11 DDI をサポートしている場合、Direct3D API は[**Pfnrendercb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)を使用しなくなりました。 そのため、Direct3D バージョン 11 DDI をサポートするドライバーでは、ドライバー DDI 関数を入力したスレッドから[**pfnPerformAmortizedProcessingCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_perform_amortized_processing_cb)カーネルコールバック関数を手動で呼び出す必要があります。イミディエイトコンテキスト (または同様の頻度)。 この操作では、ハイウォーターマークをトリミングする必要があるため、[状態更新 DDI コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を利用する場合、ドライバーがコマンドバッファー以降プリアンブルデータを生成する前に実行することをお勧めします。

さらに、ドライバーは API の償還に関する問題を認識し、 [**pfnPerformAmortizedProcessingCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_perform_amortized_processing_cb)カーネルコールバック関数を使用する頻度を調整します。 1つの極端な場合、ドライバーは過剰な処理を引き起こす可能性があります。 たとえば、複数のエンジンが使用されていることが原因で、ドライバーが常に*pfnPerformAmortizedProcessingCb*を2回 (バックツーバック) する場合、ドライバーは*pfnPerformAmortizedProcessingCb*を1回だけ呼び出す方が効率的です。 それ以外では、ドライバーが*pfnPerformAmortizedProcessingCb*を呼び出さない場合、たとえば、フレームレンダリングのデザインが交互に発生したことが原因で、Direct3D API がフレーム全体に対して作業を行うことを許可していない可能性があります。 ドライバーは、自然に*pfnPerformAmortizedProcessingCb*を呼び出す必要はありません (たとえば、ドライバーが1ミリ秒の期間に*pfnPerformAmortizedProcessingCb*を呼び出さなかった場合は、次のようにする必要があります。API のポンプ時間)。 このドライバーは、既存の[**Pfnrendercb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)呼び出しのうち**pfnPerformAmortizedProcessingCb**がどのものである必要があるかを判断するために必要です。これは、操作のスレッドセマンティクスに準拠している必要があります。

コマンドリストをサポートするドライバーの場合、これらのドライバーは、空き領域が不足している場合は常に遅延コンテキストから[**pfnPerformAmortizedProcessingCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_perform_amortized_processing_cb)を呼び出す必要があります (すべてのイミディエイトコンテキストフラッシュと同様の頻度です)。 Direct3D version 11 ランタイムは、少なくともこのような操作中にハイウォーターマークをトリミングすることを想定しています。 [**Pfnrendercb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)に関連するスレッドセマンティクスは、direct3d バージョン11では緩和されているため、direct3d バージョン11が制限なく**pfnrendercb**を引き続きフックできるようにするために、同時実行の問題を解決する必要があります。

### <a name="new-ddi-error-code"></a>新しい DDI エラーコード

D3DDDIERR\_APPLICATIONERROR エラーコードが作成されます。これにより、ドライバーは Direct3D version 11 API では検証に参加できませんでした。 以前は、ドライバーが E\_INVALIDARG エラーコードを返した場合、API によって例外が発生します。 デバッグレイヤーが存在すると、デバッグ出力が発生し、ドライバーが内部エラーを返したことを示します。 デバッグ出力では、ドライバーにバグがあったことが開発者に提示されます。 ドライバーが D3DDDIERR\_APPLICATIONERROR を返した場合、デバッグ層はアプリケーションがエラーになっていると判断します。

### <a name="retroactively-requiring-free-threaded-calcprivate-ddis"></a>無料スレッド CalcPrivate DDIs を必要とする遡及

Direct3D バージョン11以降では、Direct3D バージョン 10 DDI 関数の*pfnCalcPrivate*で始まるドライバー関数をフリースレッドにする必要があります。 この遡及的要件は、サポートされていないことがドライバーによって示されている場合でも、常に*pfnCalcPrivate\** および[**pfnCalcDeferredContextHandleSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcdeferredcontexthandlesize)関数をフリースレッドにする必要がある Direct3D バージョン 11 DDI の動作と一致します。DDI スレッド。 この遡及的要件の詳細については、「[フリースレッド CalcPrivate DDIs の要求](retroactively-requiring-free-threaded-calcprivate-ddis.md)」を参照してください。

### <a name="deferred-destruction-and-flush-d3d10"></a>破棄とフラッシュ D3D10 の遅延

すべての破棄関数がフリースレッドになったため、Direct3D ランタイムは破棄中にコマンドバッファーをフラッシュできません。 したがって、破棄関数は、直ちにコンテキストを操作するスレッドがそのオブジェクトに依存しないようにするために、ドライバーがオブジェクトの実際の破棄を遅延させる必要があります。 個々の個別の直接コンテキストメソッドでは、同期を効率的に使用して、この破棄の問題を解決することはできません。そのため、ドライバーはコマンドバッファーをフラッシュするときにのみ同期を使用する必要があります。 また、Direct3D ランタイムは同様の問題に対処する必要がある場合にも同じ設計を使用します。

遅延破棄の ratification のため、Direct3D ランタイムは、遅延破棄の回避策を許容できないアプリケーションが明示的なメカニズムを使用することを中心にしています。 そのため、ドライバーは、[**フラッシュ (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_flush)関数の呼び出し中に (コマンドバッファーが空の場合でも) 遅延破棄キューを処理して、これらのメカニズムが実際に動作することを確認する必要があります。

同期破棄の形式を必要とするアプリケーションでは、必要な破棄の負荷に応じて、次のいずれかのパターンを使用する必要があります。

-   アプリケーションによって、そのオブジェクトに対するすべての依存関係 (つまり、コマンドリスト、ビュー、中間ウェアなど) が解放された後、アプリケーションは次のパターンを使用します。
    ```cpp
    Object::Release(); // Final release
    ImmediateContext::ClearState(); // Remove all ImmediateContext references as well.
    ImmediateContext::Flush(); // Destroy all objects as quickly as possible.
    ```

-   次のパターンは、より heavywight な破棄です。
    ```cpp
    Object::Release(); // Final release
    ImmediateContext::ClearState(); // Remove all ImmediateContext references as well.
    ImmediateContext::Flush();
    ImmediateContext::End( EventQuery );
    while( S_FALSE == ImmediateContext::GetData( EventQuery ) ) ;
    ImmediateContext::Flush(); // Destroy all objects, completely.
    ```

### <a name="primary-exceptions"></a>プライマリ例外

プライマリは、ランタイムがドライバーの[**Createresource (D3D11)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)関数の呼び出しで作成するリソースです。 ランタイムは、 [**D3D11DDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)構造体の**pprimarydesc**メンバーを、 [**DXGI\_DDI\_プライマリ\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)構造体への有効なポインターに設定することによって、プライマリを作成します。 プライマリには、前の Direct3D 10 から Direct3D 11 への変更点に関して、次のような重要な例外があります。

-   プライマリのドライバーの[**Createresource (D3D11)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)関数と[**DESTROYRESOURCE (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyresource)関数はどちらもフリースレッドではなく、直接コンテキストスレッドドメインを共有します。 同時実行は、 *pfnCreate*および*pfndestroy*で始まる関数と共に使用できます。これには、createresource (D3D11) と destroyresource (D3D10) が含まれます。 ただし、プライマリに対して**Createresource (D3D11)** と**DESTROYRESOURCE (D3D10)** を同時実行することはできません。 たとえば、ドライバーは、CreateResource (D3D11) または DestroyResource (D3D10) 関数への呼び出しがプライマリに対するものであることを検出できます。これにより、関数呼び出しの間、直接コンテキストメモリを安全に使用またはタッチすることができます。

-   プライマリの破棄は、Direct3D ランタイムによって延期することはできません。ドライバーは、ドライバーの[**Destroyresource (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyresource)関数の呼び出し内で、 [*Pfndeallocatecb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocatecb)関数を適切に呼び出す必要があります。

 

 

