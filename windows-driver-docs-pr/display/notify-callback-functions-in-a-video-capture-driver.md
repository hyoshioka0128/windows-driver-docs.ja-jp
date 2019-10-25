---
title: ビデオ キャプチャ ドライバーでのコールバック関数の通知
description: ビデオ キャプチャ ドライバーでのコールバック関数の通知
ms.assetid: 2b900436-7874-43a7-97bf-7d1eead78126
keywords:
- DxApi ミニポートドライバー WDK DirectDraw、コールバック関数への通知
- コールバック関数への通知 WDK カーネルモードのビデオトランスポート
- コールバック関数 WDK カーネルモードビデオトランスポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29a6933cbf4037fad53ad9610709624b122e2f4e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840530"
---
# <a name="notify-callback-functions-in-a-video-capture-driver"></a>ビデオ キャプチャ ドライバーでのコールバック関数の通知


## <span id="ddk_notify_callback_functions_in_a_video_capture_driver_gg"></span><span id="DDK_NOTIFY_CALLBACK_FUNCTIONS_IN_A_VIDEO_CAPTURE_DRIVER_GG"></span>


ビデオキャプチャドライバーは、特定の操作に対してランタイムの[**Dxapi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxapi/nf-dxapi-dxapi)関数を呼び出す場合に、DirectDraw ランタイムに通知コールバック関数を提供します。 たとえば、ビデオキャプチャドライバーは、 [**DD\_dxapi\_OPENVIDEOPORT**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551498(v=vs.85))関数識別子を使用して**dxapi**を呼び出してビデオポートを開くと、 [*notifycallback*](https://docs.microsoft.com/windows/desktop/api/ddkmapi/nc-ddkmapi-lpdd_notifycallback)関数を提供します。 ビデオポートが閉じると、DirectDraw ランタイムに通知され、 *Notifycallback*が呼び出されます。 ビデオキャプチャドライバーは、ビデオポートのクローズに関連する必要な操作を実行できます。

ビデオキャプチャドライバーは、ビデオキャプチャドライバーが[**Dxapi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxapi/nf-dxapi-dxapi)関数を呼び出して、次のいずれかの関数識別子を指定するときに、DirectDraw ランタイムに*notifycallback*関数を提供します。

-   [**DD\_DXAPI\_OPENDIRECTDRAW**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550702(v=vs.85))

-   [**DD\_DXAPI\_OPENSURFACE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550711(v=vs.85))

-   [**DD\_DXAPI\_OPENVIDEOPORT**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551498(v=vs.85))

-   [**DD\_DXAPI\_登録\_コールバック**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551502(v=vs.85))

-   [**DD\_DXAPI\_OPENVPCAPTUREDEVICE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551500(v=vs.85))

その後、関数識別子に関連付けられているイベントが発生すると、DirectDraw ランタイムは*Notifycallback*関数を呼び出します。 ビデオキャプチャドライバーの*Notifycallback*は、イベントに関連する操作を実行するために実装されています。

 

 





