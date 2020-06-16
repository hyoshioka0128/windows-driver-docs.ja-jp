---
title: 既存の AVStream ドライバーへの VRAM キャプチャ サポートの追加
description: 既存の AVStream ドライバーに VRAM capture サポートを追加する
ms.assetid: 10736533-3873-4f1d-91c5-d2e55163daaa
keywords:
- VRAM capture WDK AVStream、既存のドライバーサポート
ms.date: 06/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: be99f53f57397ecf9d8e3445a8776c6cc8de6473
ms.sourcegitcommit: 77c63789350cfc1dc740baaafdef64803d86217f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84793736"
---
# <a name="adding-vram-capture-support-to-existing-avstream-drivers"></a>既存の AVStream ドライバーに VRAM capture サポートを追加する

DMA を使用する既存のピン中心の AVStream ドライバーに VRAM キャプチャサポートを追加するには、次の手順に従います。

1. [*Avstrminipinprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)コールバックルーチンに VRAM キャプチャサポートを追加します。 Avstream でシミュレートされた[ハードウェアサンプルドライバー (AVSHwS)](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/)の**CCapturePin::P rocess**メソッドは、この*方法の 1*つを示しています。

1. このセクションで前述したように、VRAM キャプチャのプロパティ要求を処理します。

1. 子キャプチャドライバーまたは親ディスプレイミニポートドライバーのいずれかにサポートを追加して、DX カーネルハンドルを VRAM アドレスにマップします。

1. StopCapture 機能を実装します。 KMD がキャプチャの停止通知を送信すると、キャプチャドライバーはすべてのキャプチャを停止する必要があります。 通知を登録するために、キャプチャドライバーは[*DxgkDdiStopCapture*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_stopcapture)コールバックルーチンを提供します。 キャプチャドライバーは、この通知を受信した後、ユーザーモードからのキャプチャ要求をすべて失敗させる必要があります。
