---
title: カーネル モード ドライバーのサンプル
description: カーネル モード ドライバーのサンプル
ms.assetid: 09d08e07-e991-458f-aedf-018a0dd20af5
keywords:
- カーネル モード ドライバー WDK サンプル
- サンプル ドライバー WDK のカーネル モード
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0eb9b6ac42f87181a368358a603853eba95c3ee2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538983"
---
# <a name="sample-kernel-mode-drivers"></a>カーネル モード ドライバーのサンプル

WDK は、さまざまなサンプルのカーネル モード ドライバーを提供します。 Src、WDK をインストールした後\\全般のサブディレクトリには、すべてのカーネル モード ドライバーに適用できるサンプル ドライバーのコードが含まれています。 サンプルは、オンラインも保持されます。 これらのサンプルを以下に示します。

[**トースター**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster/toastpkg)  
準拠しているドライバーの一連のサンプル コードを提供、 [Windows Driver Model](windows-driver-model.md) (WDM)。 このサンプルでは、サンプルのインストール ソフトウェアも含まれています。

[**HID デバイスのフィルター ドライバーを KMDF** (ioctl サンプル)](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/firefly)  
ドライバーが I/O 制御コードをサポートする方法について説明します。

[**イベント**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/event)  
アプリケーションが通知を要求した場合、ハードウェアのイベントのアプリケーションに通知するカーネル モード ドライバーが使用できるテクニックを示します。 1 つの方法を使用して[イベント オブジェクト](event-objects.md)、もう一方が依存して[キュー](queuing-and-dequeuing-irps.md)イベントが発生するまで、通知要求。

[**キャンセル**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/cancel)  
使用方法を示します[キャンセル セーフ IRP キュー](cancel-safe-irp-queues.md)します。

[**tracedrv**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)  
使用する方法を示します[WPP ソフトウェア トレース](https://msdn.microsoft.com/library/windows/hardware/ff556204)します。

その他のサブディレクトリ、 \\src ディレクトリには、さまざまな種類のハードウェア用のカーネル モード ドライバーのサンプル コードが含まれます。

## <a name="see-also"></a>関連項目

[Microsoft Windows ドライバー サンプル](https://github.com/Microsoft/Windows-driver-samples)github
