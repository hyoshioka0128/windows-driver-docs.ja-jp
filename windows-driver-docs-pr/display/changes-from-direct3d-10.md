---
title: Direct3D 10 からの変更点
description: Direct3D 10 からの変更点
ms.assetid: 014a5e44-f8c4-45c0-96e8-d82f37b8b28d
keywords:
- Direct3D のバージョン 11 WDK Windows 7 の表示、Direct3D のバージョン 10 から変更します。
- Direct3D のバージョン 11 WDK Windows Server 2008 R2 の表示、Direct3D のバージョン 10 から変更します。
- Direct3D のバージョン 10 WDK Windows 7 の表示
- Direct3D バージョン 10 WDK Windows 7 の表示、Direct3D のバージョン 11 での変更
- Direct3D バージョン 10 WDK Windows Server 2008 R2 の表示、Direct3D のバージョン 11 での変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6ce864c55b0f0267f3e8cdacb1889428098d943
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384594"
---
# <a name="changes-from-direct3d-10"></a>Direct3D 10 からの変更点


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

次のセクションでは、direct3d11、direct3d10 からどのように変更されたかについて説明します。

### <a name="driver-callback-functions-to-kernel-mode-services"></a>サービスのカーネル モード ドライバーのコールバック関数

デバイス固有のコールバック関数で、Direct3D のバージョン 11 ランタイムを提供する、 [ **D3DDDI\_DEVICECALLBACKS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_devicecallbacks)ランタイムが呼び出すユーザー モードのディスプレイ ドライバーのと構造体[ **CreateDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数がカーネル ハンドルとカーネル関数のシグネチャからドライバーを分離します。 前の Direct3D のバージョンのランタイムでのシングル スレッド モードがサポートされていませんでしたが、コールバックのセマンティクスとフリー スレッド モードの操作をサポートするために、コールバック関数の実装を Direct3D のバージョン 11 ランタイムが変更します。操作です。 シングル スレッド モードの操作の規則の適用後、ドライバーは、シングル スレッド モードをサポートしていることを示します (D3D11DDICAPS\_FREETHREADED)。 そうしないと、以前の制限された頻度の高いルールが適用されます。 ドライバーがシングル スレッド モードのサポートを指定する方法については、次を参照してください。[スレッド処理とコマンドを一覧表示](supporting-threading--command-lists--and-3-d-pipeline.md)します。 Direct3D のバージョン 11 状態は次の制限であります。

-   1 つのスレッドは、一度に、HCONTEXT に対して作業できます。 現在、HCONTEXT を使用している既存のコールバック関数は[ **pfnPresentCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)、 [ **pfnRenderCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)、 [ *pfnEscapeCb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_escapecb)、 [ **pfnDestroyContextCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroycontextcb)、 [ **pfnWaitForSynchronizationObjectCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_waitforsynchronizationobjectcb)、および[ **pfnSignalSynchronizationObjectCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobjectcb)します。 したがって場合は、複数のスレッドでは、これらのコールバック関数を呼び出すし、同じ HCONTEXT を使用して、ドライバーはコールバック関数への呼び出しを同期する必要があります。 この要件を満たすことは非常に自然なは、これらのコールバック関数は、イミディ エイト コンテキストを操作するスレッドからのみ呼び出されるためです。

-   ドライバーは、それらのドライバー関数を呼び出した同じスレッドを使用して、次のドライバー関数への呼び出し中にのみ、次のコールバック関数を呼び出す必要があります。

    <span id="pfnAllocateCb"></span><span id="pfnallocatecb"></span><span id="PFNALLOCATECB"></span>[**pfnAllocateCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)  
    ドライバーを呼び出す必要があります[ *pfnAllocateCb* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)ドライバーを呼び出したスレッドで[ **CreateResource(D3D11)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)共有するときに関数リソースが作成されます。 デバイスと非共有の割り当てが通常は完全にフリー スレッドです。

    <span id="pfnPresentCb"></span><span id="pfnpresentcb"></span><span id="PFNPRESENTCB"></span>[**pfnPresentCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)  
    ドライバーを呼び出す必要があります[ **pfnPresentCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)ドライバーへの呼び出し中にのみ[ **PresentDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)関数。

    <span id="pfnSetDisplayModeCb"></span><span id="pfnsetdisplaymodecb"></span><span id="PFNSETDISPLAYMODECB"></span>[**pfnSetDisplayModeCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setdisplaymodecb)  
    ドライバーを呼び出す必要があります[ **pfnSetDisplayModeCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setdisplaymodecb)ドライバーへの呼び出し中にのみ[ **SetDisplayModeDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_1_ddi_base_functions)関数。

    <span id="pfnRenderCb"></span><span id="pfnrendercb"></span><span id="PFNRENDERCB"></span>[**pfnRenderCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)  
    ドライバーを呼び出す必要があります[ *pfnRenderCb* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)ドライバーを呼び出したスレッドで[ **Flush(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_flush)関数。 この制限は、HCONTEXT 制限のため非常に自然です。

-   [ *PfnDeallocateCb* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocatecb)コールバック関数併せて特別なドライバーを呼び出す必要はないため*pfnDeallocateCb*からドライバーが返される前に、[ **DestroyResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyresource)関数のほとんどのリソースの種類。 ドライバーをドライバーの既存のイミディ エイト コンテキストの参照が残っていないことが効率的に確保されるまでオブジェクトの破棄を延期する必要があります DestroyResource(D3D10) は、フリー スレッドの関数であるため (つまり、ドライバーを呼び出す必要があります[ **pfnRenderCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)する前に*pfnDeallocateCb*)。 共有リソースまたは HRESOURCE 使用率を補完する HRESOURCE を使用するその他のコールバック関数も、この制限が適用されます[ **pfnAllocateCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)します。 ただし、この制限は、プライマリには適用されません。 プライマリの例外の詳細については、次を参照してください。[プライマリ例外](#primary-exceptions)します。 一部のアプリケーションには、同期の破棄の外観が必要とする可能性があります、ため、ドライバーを呼び出していることを確認する必要があります*pfnDeallocateCb*以前の呼び出し中に共有リソースを破棄いずれかの[ **Flush(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_flush)関数。 ドライバーもクリーンアップする必要があります、Flush(D3D10) 関数の呼び出し中に (のみですが、パイプラインを停止していないもの) のオブジェクトが破棄以前ドライバーは、ため、ランタイムが、クリーンアップするには、公式のメカニズムとして Flush(D3D10) を呼び出すことを確認するようなメカニズムが必要となるようないくつかのアプリケーション用の破棄されたオブジェクトを延期を行う必要があります。 このメカニズムの詳細については、次を参照してください。[遅延破棄および Flush(D3D10)](#deferred-destruction-and-flush-d3d10)します。 ドライバーが破棄が延期されたすべてのオブジェクトが、ドライバーの前に完全に破棄ことを確認する必要がありますも[ **DestroyDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroydevice)クリーンアップ中に関数を返します。

### <a name="deprecate-ability-to-allow-modification-of-free-threaded-ddis"></a>Ddi のフリー スレッドの変更を許可する機能を廃止します。

Direct3D のバージョン 11、ディスプレイの API レベルの概念のデバイスと、イミディ エイト コンテキストは引き続きバンドル DDI レベルでレガシ ディスプレイ デバイスの概念。 このバンドルをディスプレイ デバイスのイミディ エイト コンテキスト Ddi の前のバージョンとの互換性を最大化 (など、 [Direct3D のバージョン 10 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)) を通じて複数の Api の複数のバージョンをサポートするときに、ドライバーのチャーンを削減し、Ddi のバージョン。 ただし、このバンドルをディスプレイ デバイスのイミディ エイト コンテキスト結果混乱 DDI スレッドのドメインが非常に明示的なためです。 代わりに、複数のインターフェイスとそれらのインターフェイス内の関数のスレッド要件を理解するドライバー開発者が、ドキュメントを参照する必要があります。

Direct3D のバージョン 11 API は、複数のスレッドを入力できることの主な機能の作成し、同時に関数を破棄します。 許可の作成時に関数のテーブルのポインターを入れ替えるし、破棄で指定されている関数のセマンティクスは Direct3D バージョン 10 DDI としてにドライバーと互換性がないこのような機能は[ **D3D10DDI\_DEVICEFUNCS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddi_devicefuncs)と[ **D3D10\_1DDI\_DEVICEFUNCS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10_1ddi_devicefuncs)許可します。 そのため、ドライバーが関数ポインター後を作成します ([**CreateDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice))、ドライバーはこれらの特定の関数ポインターを変更することによって動作を変更しようとはしないでください11 DDI Direct3D のバージョンで実行される、ドライバーとドライバー DDI スレッド処理をサポートしています。 この制限が適用されるすべてのデバイス機能で始まる*pfnCreate*、 *pfnOpen*、 *pfnDestroy*、 *pfnCalcPrivate*と*pfnCheck*します。 デバイスの機能のすべての残りの部分は、イミディ エイト コンテキストに強く関連付けられます。 1 つのスレッドは、一度にイミディ エイト コンテキストを操作する、ために、ドライバーはホット スワップ イミディ エイト コンテキスト関数のテーブルのエントリを引き続き適切に定義されたです。

### <a name="pfnrendercb-versus-pfnperformamortizedprocessingcb"></a>pfnRenderCb Versus pfnPerformAmortizedProcessingCb

Direct3D のバージョン 10 API 関数のフック、Direct3D ランタイムの[ **pfnRenderCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)償却の処理を実行するカーネル コールバック関数 (つまり、特定の操作を実行するのではなくすべての API 関数呼び出し、ドライバー償却の操作を実行のすべてのように多数の API 関数呼び出し)。 通常、API は、ハイ ウォーターマークをトリミングし、特にその遅延オブジェクトの破棄キューをフラッシュするこの機会を使用します。

Direct3D API カーネルとフリー スレッド ドライバーできるだけするコールバック関数を許可するのには不要になった[ **pfnRenderCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)ドライバーが Direct3D のバージョン 11 をサポートしているときに DDI します。 そのため、Direct3D のバージョン 11 をサポートするドライバー DDI 呼び出す必要があります手動で、 [ **pfnPerformAmortizedProcessingCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_perform_amortized_processing_cb) DDI ドライバーを入力したのと同じスレッドからカーネル コールバック関数ドライバーは、イミディ エイト コンテキスト (または同様の頻度) をコマンド バッファーを送信した後の関数。 利用する場合、ドライバーはコマンド バッファー以降、プリアンブル データを生成する前に行う利点がありますが、操作は、ハイ ウォーターマークをトリミングする必要があります、ため、 [DDI コールバック関数の状態の更新](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

さらに、ドライバーが API の償却問題に注意してくださいし、使用頻度のバランスが取れる必要があります、 [ **pfnPerformAmortizedProcessingCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_perform_amortized_processing_cb)カーネル コールバック関数。 1 つの極端には、過剰な処理が、ドライバーにあります。 たとえば、ドライバーは常に呼び出されます*pfnPerformAmortizedProcessingCb* 2 回 (連続)、マルチ エンジンの使用状況、原因として考えられますことを呼び出してドライバーの効率を高める*pfnPerformAmortizedProcessingCb* 1 回だけです。 その一方で、ドライバーできない可能性があります、ドライバーが呼び出されない場合は、全体のフレームの作業を行うための Direct3D API *pfnPerformAmortizedProcessingCb*交互のフレームのレンダリング デザインしている可能性があります。 ドライバーを呼び出す必要はありません*pfnPerformAmortizedProcessingCb*場合よりも必然的、過剰であるためより多くの場合、(ドライバーを呼び出さなかった場合など、 *pfnPerformAmortizedProcessingCb*1 ミリ秒タイム フレームで、API をポンプする時間をするする必要があります)。 のみ、既存の判断するために、ドライバーが必要な[ **pfnRenderCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)も指定する呼び出し**pfnPerformAmortizedProcessingCb**と、当然ながら、スレッド処理操作のセマンティクスに準拠しています。

コマンド リストをサポートするドライバー、それらのドライバーを呼び出す必要がありますも[ **pfnPerformAmortizedProcessingCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_perform_amortized_processing_cb)余地がないそれらのドライバーが実行されるたびに、遅延のコンテキストから (同様の頻度、すべてイミディ エイト コンテキスト フラッシュ)。 Direct3D のバージョン 11 ランタイムが、要求は、このような操作中に、少なくともそのハイ ウォーターマークをトリミングします。 関連する、スレッド処理セマンティクスはため[ **pfnRenderCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb) Direct3D のバージョン 11、同時実行を引き続きをフックするDirect3Dのバージョン11を許可するには、問題を解決する必要が緩和されました**pfnRenderCb**、制限なし。

### <a name="new-ddi-error-code"></a>新しい DDI エラー コード

D3DDDIERR\_APPLICATIONERROR エラー コードは Direct3D のバージョン 11 API しなかった検証に参加するドライバーを許可するように作成します。 以前は、ドライバーには、E が返された場合\_INVALIDARG エラー コード、例外を発生させる API の原因となります。 デバッグ レイヤーが存在はデバッグの出力が発生して、ドライバーが内部エラーを返す必要があります。 デバッグの出力は、ドライバーにバグがあり、開発者にお勧めします。 場合は、ドライバーは返します D3DDDIERR\_アプリケーションが代わりには、エラー、APPLICATIONERROR デバッグ レイヤーを決定します。

### <a name="retroactively-requiring-free-threaded-calcprivate-ddis"></a>フリー スレッド CalcPrivate DDI が遡及的に必要

始まる Direct3D のバージョン 11 が過去にさかのぼってドライバー機能を必要と*pfnCalcPrivate*フリー スレッド化されたに Direct3D のバージョン 10 DDI 関数。 この事後対応の要件に一致する Direct3D のバージョン 11 の動作を常に必要とする DDI *pfnCalcPrivate\** と[ **pfnCalcDeferredContextHandleSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcdeferredcontexthandlesize)無料関数、スレッドの場合でも、ドライバーを示します DDI スレッド処理をサポートしていません。 この事後対応要件の詳細については、次を参照してください。 [Retroactively Requiring Free-Threaded CalcPrivate Ddi](retroactively-requiring-free-threaded-calcprivate-ddis.md)します。

### <a name="deferred-destruction-and-flush-d3d10"></a>遅延の破棄とフラッシュ D3D10

破棄のすべての機能は、フリー スレッドようになりましたが、ため、Direct3D のランタイムの破棄中にコマンド バッファーをフラッシュできません。 そのため、破棄関数は、ドライバーがイミディ エイト コンテキストを操作するスレッドがそのオブジェクトが存続する依存が不要になったことを確認することができますに達するまで、実際にオブジェクトの破棄を 必要があります。 イミディ エイト コンテキストを不連続の各メソッドは、破棄この問題を解決するために同期を使用効率的にことはできません。そのため、ドライバーは、コマンド バッファーをフラッシュする場合にのみ、同期を使用する必要があります。 Direct3D のランタイムは、同様の問題に取り組む必要がある場合にもこの同じデザインを使用します。

遅延の破棄の抜本的、原因は、Direct3D ランタイムは、遅延破棄の回避策を許容できないアプリケーションが代わりに明示的なメカニズムを使用する代弁者です。 そのため、ドライバーの呼び出し中に遅延破棄キューを処理する必要があります、 [ **Flush(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_flush) (たとえコマンド バッファーが空の) にこれらのメカニズムが実際に動作できるようにする機能します。

同期の破棄のフォームを必要とするこれらのアプリケーションは、次のパターンのいずれかを使用する必要があります、重い紙方法に応じて、破棄が必要があります。

-   アプリケーションは、そのオブジェクトに対するすべての依存関係が解放されたことを確認した後 (リスト、ビュー、中間の ware およびなどのコマンドは、)、アプリケーションは、次のパターンを使用します。
    ```cpp
    Object::Release(); // Final release
    ImmediateContext::ClearState(); // Remove all ImmediateContext references as well.
    ImmediateContext::Flush(); // Destroy all objects as quickly as possible.
    ```

-   次のパターンでは、複数 heavywight 破棄を示します。
    ```cpp
    Object::Release(); // Final release
    ImmediateContext::ClearState(); // Remove all ImmediateContext references as well.
    ImmediateContext::Flush();
    ImmediateContext::End( EventQuery );
    while( S_FALSE == ImmediateContext::GetData( EventQuery ) ) ;
    ImmediateContext::Flush(); // Destroy all objects, completely.
    ```

### <a name="primary-exceptions"></a>プライマリ例外

プライマリは、ランタイムは、ドライバーの呼び出しで作成します。 リソース[ **CreateResource(D3D11)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)関数。 ランタイムを設定して、プライマリを作成する、 **pPrimaryDesc**のメンバー、 [ **D3D11DDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)への有効なポインターをに構造体[**DXGI\_DDI\_プライマリ\_DESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)構造体。 プライマリでは、direct3d10 から direct3d11 への前の変更に関して、次の注目すべき例外があります。

-   ドライバーの両方の[ **CreateResource(D3D11)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)と[ **DestroyResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyresource)プライマリはフリー スレッドでない関数ドメインのスレッドのイミディ エイト コンテキストを共有します。 同時実行を開始する関数と存在できます*pfnCreate*と*pfnDestroy*、CreateResource(D3D11) および DestroyResource(D3D10) が含まれます。 同時実行できません。 ただし、 **CreateResource(D3D11)** と**DestroyResource(D3D10)** プライマリにします。 たとえば、ドライバーでは、その CreateResource(D3D11) または DestroyResource(D3D10) 関数の呼び出しがプライマリではおよびこと、または安全を使用できる関数呼び出しの期間のイミディ エイト コンテキストのメモリをタッチことが決まることを検出できます。

-   プライマリ破棄は、Direct3D ランタイムによって遅延されることはできませんし、ドライバーを呼び出す必要があります、 [ *pfnDeallocateCb* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocatecb)ドライバーへの呼び出し内で適切に関数[ **DestroyResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyresource)関数。

 

 

