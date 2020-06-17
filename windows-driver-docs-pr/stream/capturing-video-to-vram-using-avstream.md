---
title: AVStream を使用してビデオを VRAM にキャプチャする
description: AVStream を使用してビデオを VRAM にキャプチャする
ms.assetid: c4ca4a67-83cb-4a89-bc84-e06b1dc67b66
keywords:
- AVStream WDK、VRAM キャプチャ
- VRAM キャプチャ WDK AVStream
- ビデオをキャプチャして VRAM WDK AVStream に
- VRAM WDK AVStream へのビデオキャプチャ
- VRAM WDK AVStream へのオーディオキャプチャ
- VRAM WDK AVStream へのデータキャプチャ
- ミニドライバー WDK VRAM キャプチャを表示する
- ミニドライバー WDK VRAM capture
ms.date: 06/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: a10245f7caf2f989ea6804882a259841cd2debd5
ms.sourcegitcommit: 97a8d24b1b48602e4ccaa63a113f7c8cdb0c6df5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84812444"
---
# <a name="capturing-video-to-vram-using-avstream"></a>AVStream を使用してビデオを VRAM にキャプチャする

Windows Vista 以降では、AVStream ドライバーはビデオとオーディオをグラフィックアダプターの VRAM に直接取り込むことができます。 Windows Vista より前に存在していた AVStream ドライバーでは、最初にデータを VRAM に配置し、システムメモリに転送してから、最後に VRAM に戻して表示する必要があります。

VRAM キャプチャのサポートは、 [Windows Display Driver Model (WDDM) 設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/display/windows-vista-display-driver-model-design-guide)で提供されている GPU スケジューリングと VRAM 仮想化を利用します。

VRAM にキャプチャするには、デバイスに同じビデオカードのキャプチャと表示の機能が含まれている必要があります。

次のセクションでは、新規または既存のドライバーに VRAM キャプチャサポートを追加する方法について説明します。

[AVStream での VRAM キャプチャの概要](overview-of-vram-capture-in-avstream.md)

[VRAM キャプチャのプロパティ](vram-capture-properties.md)

[圧縮されていないデータの VRAM へのキャプチャ](capturing-uncompressed-data-to-vram.md)

[既存の AVStream ドライバーへの VRAM キャプチャ サポートの追加](adding-vram-capture-support-to-existing-avstream-drivers.md)

Avstream のシミュレートされた[ハードウェアサンプルドライバー (AVSHwS)](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/)には、VRAM キャプチャを示すサンプルコードがあります。
