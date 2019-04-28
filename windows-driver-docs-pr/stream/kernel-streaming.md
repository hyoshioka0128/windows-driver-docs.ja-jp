---
title: カーネル ストリーミング
description: カーネル ストリーミング
ms.assetid: dcd28218-b3bf-4e5d-b1a7-6910103afb96
keywords:
- Windows 2000 カーネル ストリーミング モデル WDK、カーネルのストリーミング
- ストリーミング モデル WDK Windows 2000 カーネルのカーネルのストリーミング
- カーネル ストリーミング モデルの WDK、カーネルのストリーミング
- カーネルの WDK のストリーミング
- カーネルのカーネルのストリーミングについて、WDK をストリーミングします。
- KS WDK
- カーネルのストリーミングについて、KS WDK
- ストリーミング ミニドライバー WDK カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69095716a217e18fb93825f1c2fff581d2865cd6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376474"
---
# <a name="kernel-streaming"></a>カーネル ストリーミング





カーネル (KS) のストリームは、ストリーミングされたデータのサポートのカーネル モード処理を Microsoft が提供するサービスを参照します。

マイクロソフトは、次の 3 つのマルチ メディア クラス ドライバー モデルを提供しています: クラス、ストリーム クラス, および AVStream のポートします。 仕入先は、これらの 3 つのクラス ドライバー モデルのいずれかで実行されているミニドライバーを書き込みます。

システム ファイルでは、ドライバー (カーネル モード Dll) のエクスポートと、これらのクラス ドライバーが実装されて*portcls.sys*、 *stream.sys*、および*ks.sys*します。 Windows XP 以降では、 *ks.sys* AVStream と呼びます。

Windows XP SP2 以降では、Microsoft が提供、 [USB ビデオ クラス](usb-video-class-driver.md)ドライバー。

このセクションには、元の (XP より前) に関連する次のトピックの以前のドキュメントが含まれています。 *ks.sys*クラス ドライバー。

[KS ミニドライバーのアーキテクチャ](ks-minidriver-architecture.md)

[KS プロパティ、イベント、およびメソッド](ks-properties--events--and-methods.md)

[KS クロック](ks-clocks.md)

[KS アロケーター](ks-allocators.md)

詳細については*portcls.sys*を参照してください[オーディオ ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff536191)します。

詳細については、 *stream.sys*ドライバーを参照してください[ストリーミング ミニドライバー](https://msdn.microsoft.com/library/windows/hardware/ff568275)します。

AVStream については、次を参照してください。、 [AVStream の概要](avstream-overview.md)します。

[DVD デコーダー ミニドライバー](https://msdn.microsoft.com/library/windows/hardware/ff558742)のクライアント*stream.sys*します。

[ビデオ キャプチャ ミニドライバー](video-capture-devices.md)のいずれかのクライアントは、 *stream.sys*または*ks.sys*します。

[ドライバーのアーキテクチャのミニドライバーのブロードキャスト](broadcast-driver-architecture-minidrivers.md)AVStream の下で実行します。

 

 




