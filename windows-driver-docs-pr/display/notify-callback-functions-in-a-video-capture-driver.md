---
title: ビデオ キャプチャ ドライバーでのコールバック関数の通知
description: ビデオ キャプチャ ドライバーでのコールバック関数の通知
ms.assetid: 2b900436-7874-43a7-97bf-7d1eead78126
keywords:
- DxApi ミニポート ドライバー WDK DirectDraw、コールバック関数への通知
- コールバック関数 WDK カーネル モードのビデオ トランスポートを通知します。
- コールバック関数 WDK のカーネル モードのビデオ トランスポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4eff67d8f33f85d044b1540cc09ffc09ae0547e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370207"
---
# <a name="notify-callback-functions-in-a-video-capture-driver"></a>ビデオ キャプチャ ドライバーでのコールバック関数の通知


## <span id="ddk_notify_callback_functions_in_a_video_capture_driver_gg"></span><span id="DDK_NOTIFY_CALLBACK_FUNCTIONS_IN_A_VIDEO_CAPTURE_DRIVER_GG"></span>


ビデオ キャプチャ ドライバーに用意されているビデオ キャプチャ ドライバーは、ランタイムを呼び出すときに、DirectDraw ランタイムにコールバック関数を通知する[ **DxApi** ](https://msdn.microsoft.com/library/windows/hardware/ff557364)関数の特定の操作。 たとえば、ビデオが装置のドライバーをキャプチャ、 [ *NotifyCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff568545)機能ドライバーを呼び出すと**DxApi**で、 [ **DD\_DXAPI\_OPENVIDEOPORT** ](https://msdn.microsoft.com/library/windows/hardware/ff551498)ビデオ ポートを開く識別子に機能します。 DirectDraw ランタイムに通知され、呼び出しのビデオ ポートを閉じた後*NotifyCallback*します。 ビデオ キャプチャ ドライバー関連のビデオ ポート終了するために必要な操作を実行できます。

ビデオ キャプチャ ドライバーに用意されている、 *NotifyCallback* DirectDraw ランタイム、ビデオ ドライバーの呼び出しをキャプチャするときに関数、 [ **DxApi** ](https://msdn.microsoft.com/library/windows/hardware/ff557364)関数をいずれかを指定します次の関数の識別子。

-   [**DD\_DXAPI\_OPENDIRECTDRAW**](https://msdn.microsoft.com/library/windows/hardware/ff550702)

-   [**DD\_DXAPI\_OPENSURFACE**](https://msdn.microsoft.com/library/windows/hardware/ff550711)

-   [**DD\_DXAPI\_OPENVIDEOPORT**](https://msdn.microsoft.com/library/windows/hardware/ff551498)

-   [**DD\_DXAPI\_登録\_コールバック**](https://msdn.microsoft.com/library/windows/hardware/ff551502)

-   [**DD\_DXAPI\_OPENVPCAPTUREDEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff551500)

その後、関数の識別子に関連付けられているイベントの発生時に、DirectDraw ランタイムが呼び出す、 *NotifyCallback*関数。 ビデオ キャプチャ ドライバーの*NotifyCallback*イベントに関連する操作を実行する実装されます。

 

 





