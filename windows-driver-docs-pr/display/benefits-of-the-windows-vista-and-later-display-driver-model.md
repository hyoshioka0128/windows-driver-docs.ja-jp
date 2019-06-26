---
title: Windows Display Driver Model (WDDM) のメリット
description: Windows Display Driver Model (WDDM) のメリット
ms.assetid: 0e8cd1a9-7137-4fd2-91ab-56768713c9f1
keywords:
- ドライバー モデル WDK Windows Vista では、特典を表示します。
- Windows Vista のディスプレイ ドライバー モデル WDK、利点があります。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76e132ab651e064aed65ebee1083e669086177ac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384629"
---
# <a name="benefits-of-the-windows-display-driver-model-wddm"></a>Windows Display Driver Model (WDDM) のメリット


## <span id="ddk_benefits_of_the_longhorn_display_driver_model_gg"></span><span id="DDK_BENEFITS_OF_THE_LONGHORN_DISPLAY_DRIVER_MODEL_GG"></span>


ディスプレイ ドライバーを作成することは、Windows 表示 Driver Model (WDDM) を使用するのではなく、Windows Vista 以降より使用可能を使用して簡単に、 [Windows 2000 Display Driver Model (XDDM)](windows-2000-display-driver-model-design-guide.md)、次の機能強化のためです。 さらに、少ないドライバー コードは、システム アドレス空間にアクセスし、クラッシュが発生する可能性があるカーネル モードで実行されるため、WDDM ドライバーはオペレーティング システムの安定性とセキュリティに寄与します。

**注**  XDDM と VGA ドライバーは、Windows 8 およびそれ以降のバージョンではコンパイルされません。 ディスプレイ ハードウェアが認定 WDDM 1.2 をサポートする、またはそれ以降であるドライバーがない Windows 8 コンピューターに接続されている場合は、Microsoft Basic 表示ドライバーを実行しているシステムが既定値です。

 

-   マイクロソフトの Direct3D ランタイムおよび Microsoft DirectX グラフィックスのカーネル サブシステム詳細の表示処理を実行 (つまりより多くのコードがランタイムと、ドライバーではなくサブシステムで)。 ビデオ メモリを管理するコードが含まれ、スケジュールは、GPU のメモリ アクセス (DMA) バッファーを送信します。 詳細については、次を参照してください。[ビデオ メモリ管理と GPU がスケジュール](video-memory-management-and-gpu-scheduling.md)します。

-   画面の作成より少ないカーネル モードのステージが必要です。

    サーフェスの作成のオペレーティング システムで以前 Windows Vista よりも次のカーネル モードの連続する呼び出しが必要です。

    1.  [*DdCanCreateSurface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))
    2.  [*DdCreateSurface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))
    3.  [**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)

    WDDM のサーフェスの作成にのみが必要です、 [ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)を呼び出してユーザー モード ディスプレイ ドライバー呼び出し、 [ **pfnAllocateCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)関数。 カーネル モードへの呼び出し[ **DxgkDdiCreateAllocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)関数が実行されます。

-   呼び出しを作成し、サーフェスを破棄して、ロックおよびリソースをロック解除をより均等にペアになっています。

-   ビデオ メモリ、システム メモリ、およびマネージ サーフェスは、WDDM で同じ処理されます。 Windows Vista より前のオペレーティング システムでは、微妙に異なる方法でこれらのコンポーネントを処理します。

-   シェーダーの翻訳は、ディスプレイ ドライバーのユーザー モードの部分で実行されます。

    このアプローチは、シェーダー翻訳がカーネル モードで実行されるときに発生する次の複雑さを排除できます。

    -   デバイス ドライバー インターフェイス (DDI) の抽象化と一致しないハードウェアのモデル
    -   変換で使用される複雑なコンパイラ テクノロジ

    シェーダーの処理は完全にプロセスごとに発生しますハードウェア アクセスが必要ないため、カーネル モードのシェーダーの処理は必要ありません。 そのため、シェーダーの翻訳のコードは、ユーザー モードで処理できます。

    Try の書き込み/、変換コードのユーザー モードの前後のコードを除く必要があります。 変換エラーが発生するアプリケーションの処理に戻す必要があります。

    バック グラウンド変換 (その他の表示を処理するスレッドから別のスレッドで実行されている変換コードは、) は、ユーザー モードの作成の簡素化します。

 

 





