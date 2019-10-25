---
title: USB カメラからの静止画のキャプチャ
description: USB カメラからの静止画のキャプチャ
ms.assetid: 762021ea-753c-4cd2-9eec-1403ee918d4e
keywords:
- Windows 2000 カーネルストリーミングモデル WDK、USBCAMD2 ミニドライバーライブラリ
- ストリーミングモデル WDK Windows 2000 カーネル、USBCAMD2 ミニドライバーライブラリ
- カーネルストリーミングモデル WDK、USBCAMD2 ミニドライバーライブラリ
- USBCAMD2 ミニドライバー library WDK Windows 2000 カーネルストリーミング
- USB ベースのストリーミングカメラの WDK USBCAMD2
- カメラ WDK USBCAMD2
- まだフレームをキャプチャする WDK USBCAMD2
- 静止フレームは WDK USBCAMD2 をキャプチャします
- bulk pipe WDK USBCAMD2
- プッシュモデルの WDK USBCAMD2
- プルモデルの WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1499661294b68fe5ea22d1dad939b825cbfb85e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844739"
---
# <a name="capturing-still-frames-from-a-usb-camera"></a>USB カメラからの静止画のキャプチャ





USBCAMD2 は、カメラのバルクパイプを介してカメラから静止フレームを取得するために、別の[静止イメージドライバー](https://docs.microsoft.com/windows-hardware/drivers/image/still-image-drivers)の機能を提供します。

***<em>静止フレームキャプチャをサポートするために、USBCAMD2 ミニドライバーは次を実行する必要があります。</em>***

-   PROPSETID\_VIDCAP\_VIDEOCONTROL プロパティハンドラーから[*USBCAMD\_BulkReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pfnusbcamd_bulkreadwrite)を呼び出し、静止イメージをキャプチャできるミニドライバーに割り当てられたバッファーへのポインターを渡します。 ポインターを**NULL**にすることはできません。

-   次に、USBCAMD2 は、一括転送を開始する前に、ミニドライバーの[*CamNewVideoFrameEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_new_frame_routine_ex) callback 関数を呼び出します。 カメラミニドライバーは、実際の静止フレームが、DirectShow によって割り当てられた最大サイズよりも小さくなると判断した場合に、要求されたサイズの一括転送を減らすことができます。

-   一括転送が完了すると、USBCAMD2 はミニドライバーの[*CamProcessRawVideoFrameEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_process_raw_frame_routine_ex) callback 関数を呼び出して、ミニドライバーが追加の処理を実行できるようにします。

静止フレームデータフローは、*プル*モデルでの使用を目的としています。 プルは、アプリケーションが静止フレームを要求したときに発生します。 また、フレームデータフローも*プッシュ*モデルで機能します。 プッシュは、ユーザーがカメラのボタンを押してデバイスイベントをトリガーしたときに発生します。

\* * プル * * * * モデルを使用して、STI ミニドライバーから静止フレームを取得するには * * * *  *<strong>*  *</strong>*

-   カメラに関連付けられている WDM ビデオキャプチャソースフィルターを開きます。

-   前の手順で取得したフィルターハンドルで静止ピンを開きます。

-   最大サイズのバッファーを使用して、そのピンで**ReadFile**を呼び出します。

-   ストリームの状態を "一時停止" から "実行" に設定します。

-   USBCAMD2 camera ミニドライバーの[Propsetid\_VIDCAP\_VIDEOCONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videocontrol)プロパティセットへのインターフェイスポインターを取得します。

-   [ **\_VIDEOCONTROL\_モード**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-mode)に関連付けられている、 *\_videocontrolflag\_トリガー*フラグを設定します。

\* * プッシュ * * * モデルをサポートして、カメラから静止フレームを取得するには * * * *  *<strong>*  *</strong>*

-   ミニドライバーの SRB\_INITIALIZE\_DEVICE handler 内から[**USBCAMD\_InitializeNewInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_initializenewinterface)を呼び出すと、 *USBCAMD\_CamControlFlag\_enabledeviceevents*フラグが渡されます。 ミニドライバーは、 [*Adapterreceivepacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-padapter_receive_packet_routine)コールバック関数内から\_デバイスを初期化\_処理します。

-   USBCAMD2 は、ユーザーがカメラの [トリガー] ボタンを押すと、登録されているイメージングアプリケーションに[**KSEVENT\_VIDCAPTOSTI\_EXT\_TRIGGER**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vidcaptosti-ext-trigger)イベントを送信します。

要求された一括読み取りまたは書き込みをキャンセルするには、アプリケーションが静止ピンをハンドルする**CancelIO**を呼び出す必要があります。 (USB 一括送信パイプを使用して) テーブルをカメラに転送する必要がある場合は、アプリケーションで**WriteFile**を呼び出して、まだ pin をハンドルする必要があります。

 

 




