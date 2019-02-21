---
title: VRAM AVStream を使用するビデオのキャプチャ
description: VRAM AVStream を使用するビデオのキャプチャ
ms.assetid: c4ca4a67-83cb-4a89-bc84-e06b1dc67b66
keywords:
- AVStream WDK、VRAM のキャプチャ
- VRAM キャプチャ WDK AVStream
- VRAM WDK AVStream にビデオのキャプチャ
- VRAM WDK AVStream にビデオのキャプチャ
- VRAM WDK AVStream にオーディオのキャプチャ
- VRAM WDK AVStream にデータのキャプチャ
- ミニドライバー WDK VRAM キャプチャを表示します。
- ミニドライバー WDK VRAM のキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15648b4a90d3be8e89662406132babbad8ab4a72
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529251"
---
# <a name="capturing-video-to-vram-using-avstream"></a>VRAM AVStream を使用するビデオのキャプチャ


Windows vista 以降では、ビデオおよびオーディオ グラフィックス アダプターの VRAM に直接、AVStream ドライバーはキャプチャできます。 Windows Vista より前に存在していた AVStream ドライバーでは、まず VRAM にデータ、システム メモリに転送する、および VRAM を表示するため最後にバックアップする必要があります。

GPU がスケジュール設定と VRAM の仮想化によって提供される新しい VRAM のキャプチャのサポートを利用、 [Windows Vista Display Driver Model](https://msdn.microsoft.com/library/windows/hardware/ff570593)します。

VRAM をキャプチャするには、デバイスはキャプチャを含めるし、同じビデオ カードの機能を表示する必要があります。

以下のセクションでは、新規または既存のドライバーを VRAM のキャプチャのサポートを追加する方法について説明します。

[AVStream で Capture VRAM の概要](overview-of-vram-capture-in-avstream.md)

[VRAM キャプチャ プロパティ](vram-capture-properties.md)

[VRAM に圧縮されていないデータのキャプチャ](capturing-uncompressed-data-to-vram.md)

[既存の AVStream ドライバーに VRAM のキャプチャのサポートを追加します。](adding-vram-capture-support-to-existing-avstream-drivers.md)

VRAM キャプチャを示すサンプル コードを見つけることができます、 [AVStream シミュレートされたハードウェア ドライバーのサンプル (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)します。

 

 




