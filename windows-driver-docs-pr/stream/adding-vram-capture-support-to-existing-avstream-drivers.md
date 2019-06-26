---
title: 既存の AVStream ドライバーへの VRAM キャプチャ サポートの追加
description: 既存の AVStream ドライバーへの VRAM キャプチャ サポートの追加
ms.assetid: 10736533-3873-4f1d-91c5-d2e55163daaa
keywords:
- VRAM キャプチャ WDK AVStream、既存のドライバー サポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 127d5be369e571c275097b275168acba8792fbe7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386775"
---
# <a name="adding-vram-capture-support-to-existing-avstream-drivers"></a>既存の AVStream ドライバーへの VRAM キャプチャ サポートの追加


DMA を使用する既存の暗証番号 (pin) を中心とした AVStream ドライバーに VRAM のキャプチャのサポートを追加するに次の手順に従います。

1.  VRAM キャプチャ サポートを追加、 [ *AVStrMiniPinProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspin)コールバック ルーチン。 **CCapturePin::Process**メソッド*Capture.cpp*の[AVStream シミュレートされたハードウェア ドライバーのサンプル (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)これを行う方法を示しています。

2.  このセクションで説明したとおり、VRAM キャプチャ プロパティ要求を処理します。

3.  子のキャプチャ ドライバーまたは DX カーネル ハンドルを VRAM アドレスにマップするには、親ディスプレイ ミニポート ドライバーでサポートを追加します。

4.  StopCapture 機能を実装します。 KMD は停止キャプチャ通知を送信するときに、キャプチャ ドライバーは、すべてのキャプチャを停止する必要があります。 キャプチャ ドライバーは、通知に登録する、 [ *DxgkDdiStopCapture* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_stopcapture)コールバック ルーチン。 キャプチャ ドライバーには、この通知を受信した後、ユーザー モードから送信されるすべてのキャプチャ要求が失敗する必要があります。

 

 




