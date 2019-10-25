---
title: PCI ベースの TV キャプチャ
description: PCI ベースの TV キャプチャ
ms.assetid: ae97d5f7-82de-4d6e-9835-ff4c7427f333
keywords:
- フィルターグラフの構成 WDK ビデオキャプチャ、PCI ベースのテレビキャプチャ
- PCI ベースの TV キャプチャの WDK ビデオキャプチャ
- TV キャプチャの WDK ビデオキャプチャ
- テレビキャプチャ WDK ビデオキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55c3d06fe972f64c2c9fa41083b0929df8b8ecab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845307"
---
# <a name="pci-based-tv-capture"></a>PCI ベースの TV キャプチャ


TV/ラジオチューナー、テレビオーディオ、およびクロスバーを備えた PCI ベースのキャプチャデバイスは、複雑なフィルターグラフを必要とします。また、多くの場合、ハードウェアには個別のプレビューストリームとキャプチャストリームがあり、それぞれに異なる色空間とフレームがあります。ディメンジョン. このようなデバイスでは、VBI またはタイムコード用に個別のストリームを提供することもできます。

次の図は、プレビューストリームとキャプチャストリームに接続された別のレンダラーを示しています。

![プレビューストリームとキャプチャストリームに接続された別のレンダラーを示す図](images/pci-tvtuner.gif)

[Propsetid\_アロケーター\_コントロール](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-allocator-control)のプロパティセットは、この種類のフィルターグラフに固有です。

この種類のフィルターグラフのオプションのバリエーションは、 [**KS\_VIDEOINFOHEADER2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_videoinfoheader2) structure 形式を使用して、標準のビデオレンダラーの代わりに、プレビューピンを video Mixer/レンダラー (VMR) DirectShow フィルターに接続することです。 このモードで構成されている場合、ビデオポートマネージャー (VPM) と[ビデオポート拡張](video-port-based-capture.md)(vpm) のカーネルモードのビデオトランスポートをサポートするディスプレイデバイスを使用して、バッファーは Microsoft DirectDraw surface ハンドルと共にキャプチャデバイスに渡されます。[**KS\_FRAME\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)構造体。

その後、ビデオキャプチャミニドライバーは、バッファーの所有権を無期限に保持できます。つまり、ロック、塗りつぶし、ロック解除を行い、キャプチャ時にサーフェイスを反転させることができます。 ミニドライバーは、全画面の MS-DOS アプリケーションまたは排他モードのゲームの実行中にサーフェイスが失われたことを示す通知を登録する必要があります。 このような場合、ミニドライバーはバッファーをキャプチャフィルターに戻す必要があります。

ビデオキャプチャハードウェアに FM ラジオチューナーが搭載されている場合は、「[ラジオチューナーを使用したビデオキャプチャデバイス](video-capture-devices-with-radio-tuners.md)」を参照してください。

 

 




