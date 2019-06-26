---
title: VMR ビデオの処理
description: VMR ビデオの処理
ms.assetid: 149f881d-1a6e-46b7-9a37-971c7bb7b79d
keywords:
- ProcAmp WDK DirectX va なので、VMR
- VMR WDK DirectX VA
- プログレッシブ ビデオ WDK DirectX VA
- ミキサー WDK VRM
- 色空間の変換が WDK DirectX VA
- パイプラインを WDK VRM
- 水平方向の WDK VRM をサイズ変更
- ハードウェア WDK VRM
- ビデオのイメージを水平方向にサイズ変更
- 色空間を変換します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06ebeef1b0248d627d16c43ef2df6161eb0496de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381848"
---
# <a name="vmr-video-processing"></a>VMR ビデオの処理


## <span id="ddk_vmr_video_processing_gg"></span><span id="DDK_VMR_VIDEO_PROCESSING_GG"></span>


VMR は、次の順序で表示する前に、ビデオに対する処理を実行できます。 VMR のミキサーのコンポーネントは、常に表示されている順序でこれらの操作を行います。 色空間変換と縦横比は、すべてのビデオ ストリームに適用されます。その他の操作は省略可能です。 VMR は、ビデオの再生アプリケーションによって要求された操作のみを実行します。

-   ProcAmp 制御の調整

-   デインター レース

-   縦横比

-   色空間変換

-   垂直または水平方向のミラーリングとアルファ ブレンド

可能であれば、VMR のミキサーは、多くのビデオの処理に必要な全体のメモリ帯域幅を削減できるだけのこれらのプロセスとして結合します。 これらのプロセスを結合できる度合いは、ハードウェアの機能によって決定されます。

このセクションの図は、処理パイプラインで VMR のミキサー ProcAmp コントロールの操作中にビデオ処理に使用されるビデオを表示します。 ミキサーで実行される操作は、ハードウェアの機能に依存します。 図で Direct3D サーフェイスを表す四角形と円は、Direct3D または DirectX VA の演算を表します。 図は、次の機能のビデオの処理パイプラインを示しています。

-   色空間変換を実行しても、ビデオ、イメージの水平方向にサイズを変更するハードウェアです。

-   色空間変換を実行することはできませんとビデオのイメージに水平方向にサイズを変更することはできませんが YUV テクスチャをサポートするハードウェアです。

-   色空間の変換を実行できないハードウェアでは、ビデオ、イメージに水平方向にサイズを変更することはできず、YUV テクスチャをサポートすることはできません。

VMR の処理パイプラインの出力画面は、Direct3D のレンダー ターゲットでは常にします。 アプリケーションは、Direct3D テクスチャまたは Direct3D スワップ チェーンの一部があります、出力のレンダー ターゲットにするように、VMR を構成できます。

次の図に、VMR を処理するために使用するビデオの処理パイプライン*プログレッシブ*ビデオ ProcAmp コントロール ハードウェアに色空間変換を実行し、ビデオ、イメージの水平方向にサイズを変更することができます。

![色空間変換を実行したり、水平方向にあるビデオ画像のサイズを変更するハードウェアを示す図](images/procamp1.png)

通常、VMR アルファ ブレンドを実行すること、またはとビデオの垂直/水平方向のミラーリングが表示されます、ビデオの再生アプリケーションは要求しません。 VMR は処理の 1 つのステージにすべてのビデオを組み込むことができます。 この場合、最初のパイプラインを使用します。 VMR がアルファ ブレンドまたは垂直/水平方向のミラーリングを実行すると、アプリケーションが要求 VMR、表示する前にビデオのイメージは、パイプラインに追加のステージを挿入します。 この場合、2 つ目のパイプラインを使用します。

次の図は、処理するために使用 VMR ビデオ パイプライン*プログレッシブ*ビデオ ProcAmp コントロール ハードウェアが色空間変換を実行することはできず、水平方向にことはできません中にあるビデオ画像のサイズを変更します。ProcAmp 調整操作 (、DXVA によって示される\_VideoProcess\_YUV2RGB と DXVA\_VideoProcess\_StretchX 列挙子に[ **DXVA\_VideoProcessCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ne-dxva-_dxva_videoprocesscaps))、YUV テクスチャをサポートしています。

![色空間変換を実行することはできませんと水平方向にサイズを変更できませんが yuv テクスチャをサポートできるハードウェアを示す図](images/procamp2.png)

次の図は、処理するために使用 VMR ビデオ パイプライン*プログレッシブ*ビデオ ProcAmp コントロール ハードウェアは、色空間の変換を実行できないことはできません、ProcAmp 中にビデオ画像の水平方向にサイズ変更調整操作 (、DXVA によって示される\_VideoProcess\_YUV2RGB と DXVA\_VideoProcess\_StretchX 列挙子に[ **DXVA\_VideoProcessCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ne-dxva-_dxva_videoprocesscaps))、YUV テクスチャはサポートされていません。

![色空間の変換を実行できないハードウェアを示す図は、水平方向にサイズ変更できないし、yuv テクスチャをサポートすることはできません。](images/procamp3.png)

VMR は、アプリケーションがアルファ ブレンドまたはビデオのイメージのミラーリングを要求しない場合、最初のパイプラインを使用します。 VMR は、アプリケーションは、いずれかのアルファ ブレンドまたはビデオのイメージのミラーリングを要求した場合、2 つ目のパイプラインを使用します。

 

 





