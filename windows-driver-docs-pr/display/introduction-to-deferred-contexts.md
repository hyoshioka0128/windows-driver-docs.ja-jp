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
ms.openlocfilehash: bf6bd9399a9c0ab4808fa3e28cde1ef2a8aa4680
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362132"
---
# <a name="introduction-to-deferred-contexts"></a>遅延コンテキストの概要


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

遅延コンテキストは、コマンドのリストを作成するアプリケーションによって使用されます。 ユーザー モードのディスプレイ ドライバーは、D3D11DDICAPS によってコマンド リストをサポートしていることを示す場合\_COMMANDLISTS\_ビルド\_の 2 つのフラグ、 [ **D3D11DDI\_スレッド処理\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff542163)構造を作成し、遅延のコンテキストを操作する機能もサポートする必要があります。 ドライバーがスレッド処理の機能を示す方法の詳細については、次を参照してください。[スレッド処理をサポートしている、コマンドを一覧表示、および 3-D パイプライン](supporting-threading--command-lists--and-3-d-pipeline.md)します。 遅延コンテキストは、生成されたコマンドの一覧を実行することによって、コマンドを実行するアプリケーションが明示的に要求されるまで、遅延のコンテキストを記録するコマンドを実行することはできません、イミディ エイト コンテキストとは異なります。 作成して、遅延のコンテキストを使用して、Direct3D のバージョン 11 は、次の新しい DDI 関数を提供します。 これらの関数は、デバイス/イミディ エイト コンテキストの組み合わせを作成するために必要な情報のサブセットです。

-   [**AbandonCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff538199)

-   [**CalcPrivateDeferredContextSize**](https://msdn.microsoft.com/library/windows/hardware/ff538280)

-   [**CreateDeferredContext**](https://msdn.microsoft.com/library/windows/hardware/ff540622)

-   [**RecycleCreateDeferredContext**](https://msdn.microsoft.com/library/windows/hardware/ff569239)

セマンティクス、 [ **CalcPrivateDeferredContextSize** ](https://msdn.microsoft.com/library/windows/hardware/ff538280)と[ **CreateDeferredContext** ](https://msdn.microsoft.com/library/windows/hardware/ff540622)関数は他のと同様に似ていますDDI 関数。

Direct3D のランタイムが呼び出しごとに、ドライバーのドライバーの新しいハンドルとコア層ハンドルで渡します[ **CreateDeferredContext** ](https://msdn.microsoft.com/library/windows/hardware/ff540622)各遅延コンテキストを作成する関数。 遅延コンテキストごとのパイプラインの状態は、パイプラインに相当する必要がありますイミディ エイト コンテキストではあるが、状態のクリア操作が実行された後の状態します。 ドライバーがのメンバーを入力する必要があります、 [ **D3D11DDI\_DEVICEFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff542141)構造体、 **p11ContextFuncs**のメンバー [ **D3D11DDIARG\_CREATEDEFERREDCONTEXT** ](https://msdn.microsoft.com/library/windows/hardware/ff542044)構造体を指す、関数のサブセットを; 関数テーブルからランタイムを使用してそれぞれの対応する遅延コンテキスト D3D10DDI\_HDEVICE ハンドル値を**hDrvContext** D3D11DDIARG のメンバー\_CREATEDEFERREDCONTEXT は、この関数のテーブルを指定します。

ドライバーが始まる関数の提供を続行する必要があります*pfnCreate*、 *pfnOpen*、および*pfnDestroy*遅延コンテキスト。 これらの関数の遅延のコンテキストでは、残りの部分と同じスレッド処理セマンティクスを共有して、その使用を開いたり閉じたりコンテキスト ローカル DDI ハンドル」の説明に従って[を使用してローカル コンテキスト DDI ハンドル](using-context-local-ddi-handles.md)します。 始まる関数*pfnCalcPrivate*または*pfnCheck* ; 遅延のコンテキストの活用がいない、ドライバーがのメンバーを設定するため、 [ **D3D11DDI\_DEVICEFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff542141)にこれらの関数の**NULL**遅延コンテキストが作成されたとき。 遅延コンテキストのサポートの残りのデバイス機能の大半が活用されます。 ドライバーを活用していないその[ **QueryGetData** ](https://msdn.microsoft.com/library/windows/hardware/ff569218)関数は、ただしします。 ただし、ドライバーを活用してその[ **ResourceMap** ](https://msdn.microsoft.com/library/windows/hardware/ff569492)と[ **ResourceUnmap** ](https://msdn.microsoft.com/library/windows/hardware/ff569495)関数。 ドライバーのみをサポート、 [ **ResourceIsStagingBusy** ](https://msdn.microsoft.com/library/windows/hardware/ff569491)関数と Direct3D のイミディ エイト コンテキスト ハンドルを使用して、イミディ エイト コンテキストをクランプします。 バージョン 11 リソースの新しい DDI 関数。 遅延コンテキストの活用がいない関数の完全な一覧を参照してください。[遅延コンテキスト DDI 関数を除く](excluding-ddi-functions-for-deferred-contexts.md)します。

コア、メモリに用意されているコールバック関数のレイヤー ドライバーの活用をブロックする、 **p11UMCallbacks**のメンバー [ **D3D11DDIARG\_CREATEDEFERREDCONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff542044)を指します。 これら core レイヤーのコールバック関数では、各遅延コンテキストの状態の更新 DDI を提供します。 ただしの追加は、最も重要な[ **pfnPerformAmortizedProcessingCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568915)で説明されているコールバック関数[direct3d10 から変更](changes-from-direct3d-10.md)します。

ドライバーは期待できません、 [ **pfnDisableDeferredStagingResourceDestruction** ](https://msdn.microsoft.com/library/windows/hardware/ff568906)するコールバック関数、 **pfnDisableDeferredStagingResourceDestruction**のメンバー [ **D3D11DDI\_CORELAYER\_DEVICECALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff542137)を有効にするポイント。 ドライバーを呼び出す必要がある**pfnDisableDeferredStagingResourceDestruction**内、 [ **CreateDevice(D3D10)** ](https://msdn.microsoft.com/library/windows/hardware/ff540635)デバイス/イミディ エイト コンテキスト; 関数その後、ドライバーは呼び出す必要がありますしない**pfnDisableDeferredStagingResourceDestruction**新しい Direct3D のバージョン 11 DDI セマンティクスを持つ。

ドライバーの[ **RecycleCreateDeferredContext** ](https://msdn.microsoft.com/library/windows/hardware/ff569239)関数する必要がありますクリア遅延のコンテキストでは、パイプラインの状態にする方法と同様のドライバーの[ **CreateDeferredContext** ](https://msdn.microsoft.com/library/windows/hardware/ff540622)遅延コンテキストのパイプラインの状態をクリアします。 ランタイムが呼び出す、ドライバーの後に[ **AbandonCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff538199)、 [ **CreateCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff540602)、または[ **RecycleCreateCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff569238)、ランタイムは、遅延のコンテキスト ハンドルを使用して、ドライバーの[ **DestroyDevice(D3D10)** ](https://msdn.microsoft.com/library/windows/hardware/ff552768)または**RecycleCreateDeferredContext**関数。 詳細については**RecycleCreateDeferredContext**を参照してください[小さなコマンドを一覧表示の最適化](supporting-command-lists.md)します。

 

 





