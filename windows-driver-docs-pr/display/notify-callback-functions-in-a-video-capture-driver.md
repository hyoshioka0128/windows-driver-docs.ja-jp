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
ms.openlocfilehash: d912fb7b285f0c157eba4a3505dde2e8d484db5b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372806"
---
# <a name="notify-callback-functions-in-a-video-capture-driver"></a>ビデオ キャプチャ ドライバーでのコールバック関数の通知


## <span id="ddk_notify_callback_functions_in_a_video_capture_driver_gg"></span><span id="DDK_NOTIFY_CALLBACK_FUNCTIONS_IN_A_VIDEO_CAPTURE_DRIVER_GG"></span>


ビデオ キャプチャ ドライバーに用意されているビデオ キャプチャ ドライバーは、ランタイムを呼び出すときに、DirectDraw ランタイムにコールバック関数を通知する[ **DxApi** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxapi/nf-dxapi-dxapi)関数の特定の操作。 たとえば、ビデオが装置のドライバーをキャプチャ、 [ *NotifyCallback* ](https://docs.microsoft.com/windows/desktop/api/ddkmapi/nc-ddkmapi-lpdd_notifycallback)機能ドライバーを呼び出すと**DxApi**で、 [ **DD\_DXAPI\_OPENVIDEOPORT** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551498(v=vs.85))ビデオ ポートを開く識別子に機能します。 DirectDraw ランタイムに通知され、呼び出しのビデオ ポートを閉じた後*NotifyCallback*します。 ビデオ キャプチャ ドライバー関連のビデオ ポート終了するために必要な操作を実行できます。

ビデオ キャプチャ ドライバーに用意されている、 *NotifyCallback* DirectDraw ランタイム、ビデオ ドライバーの呼び出しをキャプチャするときに関数、 [ **DxApi** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxapi/nf-dxapi-dxapi)関数をいずれかを指定します次の関数の識別子。

-   [**DD\_DXAPI\_OPENDIRECTDRAW**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550702(v=vs.85))

-   [**DD\_DXAPI\_OPENSURFACE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550711(v=vs.85))

-   [**DD\_DXAPI\_OPENVIDEOPORT**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551498(v=vs.85))

-   [**DD\_DXAPI\_登録\_コールバック**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551502(v=vs.85))

-   [**DD\_DXAPI\_OPENVPCAPTUREDEVICE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551500(v=vs.85))

その後、関数の識別子に関連付けられているイベントの発生時に、DirectDraw ランタイムが呼び出す、 *NotifyCallback*関数。 ビデオ キャプチャ ドライバーの*NotifyCallback*イベントに関連する操作を実行する実装されます。

 

 





