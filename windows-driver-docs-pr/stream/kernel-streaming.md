---
title: カーネル ストリーミング
description: カーネル ストリーミング
ms.assetid: dcd28218-b3bf-4e5d-b1a7-6910103afb96
keywords:
- Windows 2000 カーネルストリーミングモデル WDK、カーネルストリーミング
- ストリーミングモデル WDK Windows 2000 カーネル、カーネルストリーミング
- カーネルストリーミングモデル WDK、カーネルストリーミング
- カーネルストリーミング WDK
- カーネルストリーミング WDK、カーネルストリーミングについて
- KS WDK
- KS WDK、カーネルストリーミングについて
- ミニドライバー WDK カーネルストリーミング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c95b5a984dad9fd88835f0f68cf324f658554d5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845559"
---
# <a name="kernel-streaming"></a>カーネル ストリーミング





カーネルストリーミング (KS) は、ストリーミングされたデータのカーネルモード処理をサポートする、Microsoft が提供するサービスを指します。

Microsoft には、ポートクラス、ストリームクラス、および AVStream という3つのマルチメディアクラスドライバーモデルが用意されています。 ベンダは、これら3つのクラスドライバーモデルのいずれかで実行されるミニドライバーを書き込みます。

これらのクラスドライバーは、エクスポートドライバー (カーネルモード Dll) として、システムファイル*portcls* *、.sys、および* *ks*に実装されています。 Windows XP 以降では、 *ks*は avstream と呼ばれています。

Windows XP SP2 以降では、 [USB ビデオクラス](usb-video-class-driver.md)ドライバーが Microsoft によって提供されています。

このセクションには、元の (XP) *ks*クラスドライバーに関連する次のトピックに関する従来のドキュメントが含まれています。

[KS ミニドライバーのアーキテクチャ](ks-minidriver-architecture.md)

[KS プロパティ、イベント、およびメソッド](ks-properties--events--and-methods.md)

[KS クロック](ks-clocks.md)

[KS アロケーター](ks-allocators.md)

*Portcls*の詳細については、「 [Audio Drivers](https://docs.microsoft.com/windows-hardware/drivers/audio/index)」を参照してください。

*Stream .sys*ドライバーの詳細については、「 [Streaming ミニドライバー](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)」を参照してください。

AVStream の詳細については、「 [avstream の概要](avstream-overview.md)」を参照してください。

[DVD デコーダーミニドライバー](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)は、 *.sys*のクライアントです。

[Video capture ミニドライバー](video-capture-devices.md)は、 *.sys*または*ks*のいずれかのクライアントにすることができます。

AVStream の下で、 [Broadcast Driver Architecture ミニドライバー](broadcast-driver-architecture-minidrivers.md)を実行します。

 

 




