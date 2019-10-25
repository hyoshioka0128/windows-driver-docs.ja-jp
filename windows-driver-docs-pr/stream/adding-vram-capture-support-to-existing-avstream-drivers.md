---
title: 既存の AVStream ドライバーへの VRAM キャプチャ サポートの追加
description: 既存の AVStream ドライバーへの VRAM キャプチャ サポートの追加
ms.assetid: 10736533-3873-4f1d-91c5-d2e55163daaa
keywords:
- VRAM capture WDK AVStream、既存のドライバーサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79c68b415af97e7cdf5b28bf5eeca5470094c131
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845583"
---
# <a name="adding-vram-capture-support-to-existing-avstream-drivers"></a>既存の AVStream ドライバーへの VRAM キャプチャ サポートの追加


DMA を使用する既存のピン中心の AVStream ドライバーに VRAM キャプチャサポートを追加するには、次の手順に従います。

1.  [*Avstrminipinprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)コールバックルーチンに VRAM キャプチャサポートを追加します。 Avstream でシミュレートされた[ハードウェアサンプルドライバー (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)の**CCapturePin::P rocess**メソッドは、この*方法の 1*つを示しています。

2.  このセクションで前述したように、VRAM キャプチャのプロパティ要求を処理します。

3.  子キャプチャドライバーまたは親ディスプレイミニポートドライバーのいずれかにサポートを追加して、DX カーネルハンドルを VRAM アドレスにマップします。

4.  StopCapture 機能を実装します。 KMD がキャプチャの停止通知を送信すると、キャプチャドライバーはすべてのキャプチャを停止する必要があります。 通知を登録するために、キャプチャドライバーは[*DxgkDdiStopCapture*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_stopcapture)コールバックルーチンを提供します。 キャプチャドライバーは、この通知を受信した後、ユーザーモードからのキャプチャ要求をすべて失敗させる必要があります。

 

 




