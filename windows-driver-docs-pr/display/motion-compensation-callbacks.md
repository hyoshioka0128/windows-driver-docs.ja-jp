---
title: モーション補正コールバック
description: モーション補正コールバック
ms.assetid: a1f748e4-0d62-4543-a409-bb9ec02a7d77
keywords:
- WDK DirectDraw の描画、モーション補正
- DirectDraw WDK Windows 2000 ディスプレイ、モーション補正
- モーション補正 WDK
- 圧縮されたビデオデコード WDK DirectDraw
- ビデオデコード WDK DirectDraw
- WDK DirectDraw のデコード
- コールバック関数 WDK DirectDraw モーション補正
- デジタルビデオデコード WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5aaa2a3313c503e02cc89f4f393b26eb42f6b1dc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840556"
---
# <a name="motion-compensation-callbacks"></a>モーション補正コールバック


## <span id="ddk_motion_compensation_callbacks_gg"></span><span id="DDK_MOTION_COMPENSATION_CALLBACKS_GG"></span>


[DirectX ビデオアクセラレーション](directx-video-acceleration.md)では、ビデオデコード処理の高速化のために DirectDraw ドライバーで提供されている次のモーション補正コールバック関数を使用します。このような目的では、DVD サブピクチャと同様にアルファブレンドをサポートしています。ご

[*DdMoCompBeginFrame*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_beginframe)

[*DdMoCompCreate*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)

[*DdMoCompDestroy*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)

[*DdMoCompEndFrame*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_endframe)

[*DdMoCompGetBuffInfo*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getcompbuffinfo)

[*DdMoCompGetFormats*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getformats)

[*DdMoCompGetGuids*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids)

[*DdMoCompGetInternalInfo*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getinternalinfo)

[*DdMoCompQueryStatus*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_querystatus)

[*DdMoCompRender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)

モーション補正コールバック関数は、DirectX Video アクセラレーションインターフェイスのデバイスドライバー側を構成します。 モーション補正コールバック関数は、 [**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造体のメンバーによって指定されます。 次の手順は、モーション補正コールバック関数へのアクセス方法を示しています。

1.  **Iamvideoaccelerator:: GetVideoAcceleratorGUIDs**から受信した guid は、デバイスドライバーの[*Ddmocompgetguids*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids)から生成されます。

2.  下流入力ピンの**Iamvideoaccelerator:: GetUncompFormatsSupported**を呼び出すと、デバイスドライバーの[*Ddmocompgetformats*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getformats)からデータが返されます。

3.  関連する処理の開始時に、デコーダーの**IAMVideoAcceleratorNotify:: GetCreateVideoAcceleratorData**の出力ピンからの[**DXVA\_connectmode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_connectmode)データ構造は、デバイスドライバーの[*ddmocompcreate*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)に渡されます。これにより、ビデオアクセラレーションオブジェクトがデコーダーに通知されます。

4.  **Iamvideoaccelerator:: GetCompBufferInfo**から返されるデータは、デバイスドライバーの[*DdMoCompGetBuffInfo*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getcompbuffinfo)から取得されます。

5.  **Iamvideoaccelerator:: Execute**を使用して送信されたバッファーは、デバイスドライバーの[*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)によって受信されます。

6.  **Iamvideoaccelerator:: QueryRenderStatus**を使用すると、デバイスドライバーの[*DdMoCompQueryStatus*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_querystatus)が呼び出されます。 DdMoCompQueryStatus からの DDERR\_WASSTILLDRAWING のリターンコードは、\_のリターンコードとして、 **Iamvideoaccelerator:: queryrenderstatus**から PENDING として表示されます。

7.  **Iamvideoaccelerator:: beginframe**に送信されるデータは、デバイスドライバーの[*Ddmocompbeginframe*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_beginframe)によって受信されます。 WASSTILLDRAWING\_のリターンコードは、 *Ddmocompbeginframe*から、 **Iamvideoaccelerator:: beginframe**に応答してホストデコーダーによって表示されることが保留されるようにするため\_に必要です。

8.  **Iamvideoaccelerator:: endframe**に送信されるデータは、デバイスドライバーの[*Ddmocompendframe*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_endframe)によって受信されます。

9.  関連する処理の最後に、デバイスドライバーの[*Ddmocompdestroy*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)が使用され、ドライバーが必要なクリーンアップを実行できるように、現在のビデオアクセラレーションオブジェクトが使用されなくなったことがドライバーに通知されます。

 

 





