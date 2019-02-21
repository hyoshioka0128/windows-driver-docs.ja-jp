---
title: 既存の AVStream ドライバーに VRAM のキャプチャのサポートを追加します。
description: 既存の AVStream ドライバーに VRAM のキャプチャのサポートを追加します。
ms.assetid: 10736533-3873-4f1d-91c5-d2e55163daaa
keywords:
- VRAM キャプチャ WDK AVStream、既存のドライバー サポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7e90a157e5e2f40d939be708adbeab913dde608
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559201"
---
# <a name="adding-vram-capture-support-to-existing-avstream-drivers"></a>既存の AVStream ドライバーに VRAM のキャプチャのサポートを追加します。


DMA を使用する既存の暗証番号 (pin) を中心とした AVStream ドライバーに VRAM のキャプチャのサポートを追加するに次の手順に従います。

1.  VRAM キャプチャ サポートを追加、 [ *AVStrMiniPinProcess* ](https://msdn.microsoft.com/library/windows/hardware/ff556351)コールバック ルーチン。 **CCapturePin::Process**メソッド*Capture.cpp*の[AVStream シミュレートされたハードウェア ドライバーのサンプル (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)これを行う方法を示しています。

2.  このセクションで説明したとおり、VRAM キャプチャ プロパティ要求を処理します。

3.  子のキャプチャ ドライバーまたは DX カーネル ハンドルを VRAM アドレスにマップするには、親ディスプレイ ミニポート ドライバーでサポートを追加します。

4.  StopCapture 機能を実装します。 KMD は停止キャプチャ通知を送信するときに、キャプチャ ドライバーは、すべてのキャプチャを停止する必要があります。 キャプチャ ドライバーは、通知に登録する、 [ *DxgkDdiStopCapture* ](https://msdn.microsoft.com/library/windows/hardware/ff560776)コールバック ルーチン。 キャプチャ ドライバーには、この通知を受信した後、ユーザー モードから送信されるすべてのキャプチャ要求が失敗する必要があります。

 

 




