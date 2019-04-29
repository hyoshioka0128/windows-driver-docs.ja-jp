---
title: ProcAmp コントロールの処理
description: ProcAmp コントロールの処理
ms.assetid: feb66d91-1b25-415b-83f4-a75361b9dc11
keywords:
- DirectX ビデオ アクセラレータ WDK Windows 2000 の表示、ProcAmp
- ビデオ アクセラレータ WDK DirectX、ProcAmp
- VA WDK DirectX、ProcAmp
- ProcAmp WDK DirectX VA
- ProcAmp WDK DirectX va なので、ProcAmp コントロールの処理について
- VMR WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9826277c1a8d27f92088485b743437a43fedfae4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383921"
---
# <a name="procamp-control-processing"></a>ProcAmp コントロールの処理


## <span id="ddk_procamp_control_processing_gg"></span><span id="DDK_PROCAMP_CONTROL_PROCESSING_GG"></span>


ProcAmp コントロール DDI ProcAmp コントロールをサポートし、グラフィック デバイス ドライバー、ビデオ コンテンツの処理を投稿する DirectX VA を拡張します。 DDI ProcAmp コントロールはビデオのミキシング レンダラー間のインターフェイス (*VMR*) とグラフィックス デバイス ドライバー。 既存の DirectDraw と DirectX VA DDI DDI にマップします。 DDI 経由でアクセスできますが、 **IAMVideoAccelerator**インターフェイス。 ProcAmp コントロール DDI は Microsoft DirectX のバージョン 9.0 で使用できます。

ドライバーは、圧縮されたビデオの高速のデコードをサポートする場合、VMR はデコード作業、および ProcAmp の調整に厳密に使用する、その他の実際のビデオを実行する 1 つ、2 つの DirectX VA デバイスを作成するドライバーを呼び出します。

このセクションでは、次のトピックについて説明します。

[8 ビット YUV の色空間の処理](processing-in-the-8-bit-yuv-color-space.md)

[VMR ビデオの処理](vmr-video-processing.md)

[DirectDraw を DirectX VA ProcAmp コントロール DDI のマッピング](mapping-the-procamp-control-ddi-to-directdraw-and-directx-va.md)

[ProcAmp プロパティ](procamp-properties.md)

[ProcAmp コントロールのためのサンプル関数](sample-functions-for-procamp-control.md)

 

 





