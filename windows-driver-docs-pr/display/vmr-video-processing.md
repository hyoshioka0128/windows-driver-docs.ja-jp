---
title: VMR ビデオの処理
description: VMR ビデオの処理
ms.assetid: 149f881d-1a6e-46b7-9a37-971c7bb7b79d
keywords:
- ProcAmp WDK DirectX VA、VMR
- VMR WDK DirectX VA
- プログレッシブビデオ WDK DirectX VA
- ミキサー WDK VRM
- 色空間の変換 WDK DirectX VA
- パイプライン WDK VRM
- 水平方向のサイズ変更 WDK VRM
- ハードウェア WDK VRM
- ビデオ画像のサイズを水平方向に変更する
- 変換 (色空間を)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26d0fae028b028ea79b47155606a59febff7b5ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825273"
---
# <a name="vmr-video-processing"></a>VMR ビデオの処理


## <span id="ddk_vmr_video_processing_gg"></span><span id="DDK_VMR_VIDEO_PROCESSING_GG"></span>


VMR は、ビデオを表示する前に、ビデオに対して次の一連の処理操作を実行できます。 VMR のミキサーコンポーネントは、これらの操作を常に一覧表示された順序で実行します。 色空間の変換と縦横比の修正は、すべてのビデオストリームに適用されます。その他の操作は省略可能です。 VMR は、ビデオ再生アプリケーションによって要求された操作のみを実行します。

-   ProcAmp コントロールの調整

-   インターレース

-   縦横比の修正

-   色空間の変換

-   垂直方向または水平方向のミラーリングとアルファブレンド

可能な限り、VMR のミキサーは、ビデオの処理に必要な全体的なメモリ帯域幅を減らすために、これらのプロセスの多くを可能な限り結合します。 これらのプロセスを組み合わせることができる程度は、ハードウェアの機能によって決まります。

このセクションの図は、ProcAmp 制御操作中にビデオを処理するために VMR のミキサーによって使用されるビデオ処理パイプラインを示しています。 ミキサーによって実行される操作は、ハードウェアの機能によって異なります。 図では、四角形は Direct3D サーフェイスを表し、円は Direct3D または DirectX VA 操作を表します。 この図は、次の機能のビデオ処理パイプラインを示しています。

-   色空間の変換を実行し、ビデオイメージの水平方向のサイズを変更できるハードウェア。

-   色空間の変換を実行できず、ビデオイメージを水平方向にサイズ変更することはできませんが、YUV テクスチャをサポートできます。

-   色空間の変換を実行できないハードウェア。ビデオイメージのサイズを変更することはできません。また、YUV テクスチャをサポートすることはできません。

VMR の処理パイプラインの出力画面は、常に Direct3D レンダーターゲットです。 アプリケーションでは、出力レンダーターゲットが Direct3D テクスチャまたは Direct3D スワップチェーンの一部である場合もあるように、VMR を構成できます。

次の図は、ProcAmp コントロールハードウェアがカラースペース変換を実行し、ビデオイメージのサイズを水平方向に変更できる場合に、*プログレッシブ*ビデオを処理するために VMR によって使用されるビデオ処理パイプラインを示しています。

![色空間の変換を実行し、ビデオイメージのサイズを水平方向に変更できるハードウェアを示す図](images/procamp1.png)

通常、ビデオ再生アプリケーションは、表示されているビデオのアルファブレンドまたは垂直方向のミラーリングを VMR が実行することを要求しません。 VMR は、すべてのビデオ処理を1つのステージに組み込むことができます。 この場合、最初のパイプラインが使用されます。 アプリケーションで、表示前にビデオイメージのアルファブレンドまたは垂直/水平方向のミラーリングを VMR に実行するように要求すると、VMR によってパイプラインに追加のステージが挿入されます。 この場合、2番目のパイプラインが使用されます。

次の図は、ProcAmp コントロールハードウェアがカラースペース変換を実行できず、ProcAmp 調整中にビデオイメージのサイズを水平方向に変更できないときに*プログレッシブ*ビデオを処理するために VMR によって使用されるビデオパイプラインを示しています。操作 (DXVA\_VideoProcess\_YUV2RGB および DXVA\_VideoProcess\_StretchX 列挙子 ( [**DXVA\_Videoprocesscap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_videoprocesscaps)) で示されますが、YUV テクスチャはサポートされています。

![色空間の変換を実行できないが、水平方向のサイズ変更はできないが、yuv テクスチャをサポートできるハードウェアを示す図](images/procamp2.png)

次の図は、ProcAmp コントロールハードウェアが色空間の変換を実行できず、ProcAmp の調整操作中にビデオイメージのサイズを上下に変更できない場合に、VMR が*プログレッシブ*ビデオを処理するために使用するビデオパイプラインを示しています。(DXVA\_VideoProcess\_YUV2RGB および DXVA\_VideoProcess\_StretchX 列挙子 ( [**DXVA\_Videoprocesscap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_videoprocesscaps)) で示されているように、は YUV テクスチャをサポートしていません。

![色空間の変換を実行できず、水平方向にサイズ変更できず、yuv テクスチャをサポートできないハードウェアを示す図](images/procamp3.png)

アプリケーションがビデオイメージのアルファブレンドやミラーリングを要求しない場合、VMR は最初のパイプラインを使用します。 アプリケーションがビデオイメージのアルファブレンドまたはミラーリングを要求した場合、VMR は2番目のパイプラインを使用します。

 

 





