---
title: Windows Display Driver Model (WDDM) のメリット
description: Windows Display Driver Model (WDDM) のメリット
ms.assetid: 0e8cd1a9-7137-4fd2-91ab-56768713c9f1
keywords:
- ドライバーモデルの表示 WDK Windows Vista、特典
- Windows Vista display driver model WDK、特典
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 557d4318eb56beb033dbe380334c0b44abc06dc8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839825"
---
# <a name="benefits-of-the-windows-display-driver-model-wddm"></a>Windows Display Driver Model (WDDM) のメリット


## <span id="ddk_benefits_of_the_longhorn_display_driver_model_gg"></span><span id="DDK_BENEFITS_OF_THE_LONGHORN_DISPLAY_DRIVER_MODEL_GG"></span>


Windows [2000 Display Driver model (XDDM)](windows-2000-display-driver-model-design-guide.md)を使用するのではなく、windows Vista 以降で使用できる Windows Display driver MODEL (WDDM) を使用すると、表示ドライバーを簡単に作成できます。これは、次の点が強化されているためです。 さらに、WDDM ドライバーは、システムアドレス空間にアクセスでき、場合によってはクラッシュが発生する可能性があるカーネルモードで実行されるドライバーコードが少ないため、オペレーティングシステムの安定性とセキュリティが向上します。

**注**  XDDM および VGA ドライバーは、Windows 8 以降のバージョンではコンパイルされません。 WDDM 1.2 以降をサポートするように認定されたドライバーを使用せずに、ディスプレイハードウェアが Windows 8 コンピューターに接続されている場合、システムは既定で Microsoft Basic Display Driver を実行します。

 

-   Microsoft Direct3D runtime と Microsoft DirectX graphics のカーネルサブシステムでは、より多くの表示処理が実行されます (つまり、ドライバーではなく、ランタイムおよびサブシステムにより多くのコードがあります)。 これには、ビデオメモリを管理し、GPU のダイレクトメモリアクセス (DMA) バッファーをスケジュールするコードが含まれます。 詳細については、「[ビデオメモリ管理と GPU スケジューリング](video-memory-management-and-gpu-scheduling.md)」を参照してください。

-   Surface の作成に必要なカーネルモードのステージが少なくなります。

    Windows Vista より前のオペレーティングシステムでサーフェイスを作成するには、次のカーネルモード呼び出しが必要です。

    1.  [*Ddcanの場合*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))
    2.  [*Ddの/フェイス*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))
    3.  [**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)

    WDDM でのサーフェイスの作成には、 [**Createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)ユーザーモード display driver 呼び出しのみが必要です。この呼び出しは、 [**Pfnallocatecb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)関数を呼び出します。 その後、カーネルモードの[**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)関数の呼び出しが発生します。

-   サーフェイスを作成または破棄し、リソースをロックおよびロック解除する呼び出しが均等になります。

-   ビデオメモリ、システムメモリ、および管理対象のサーフェイスは、WDDM でも同じように処理されます。 Windows Vista より前のオペレーティングシステムでは、これらのコンポーネントをわずかに異なる方法で処理していました。

-   シェーダー変換は、ディスプレイドライバーのユーザーモード部分で実行されます。

    この方法では、シェーダー変換がカーネルモードで実行されるときに発生する次のような複雑さがなくなります。

    -   デバイスドライバーインターフェイス (DDI) の抽象化と一致しないハードウェアモデル
    -   翻訳で使用される複雑なコンパイラテクノロジ

    シェーダー処理はプロセスごとに完全に発生し、ハードウェアアクセスは必要ないため、カーネルモードシェーダー処理は必要ありません。 したがって、シェーダー変換コードはユーザーモードで処理できます。

    ユーザーモード翻訳コードに try/except コードを記述する必要があります。 変換エラーが発生すると、アプリケーションの処理に戻ります。

    バックグラウンド翻訳 (つまり、他の表示処理スレッドとは別のスレッドで実行される翻訳コード) は、ユーザーモード用に簡単に記述できます。

 

 





