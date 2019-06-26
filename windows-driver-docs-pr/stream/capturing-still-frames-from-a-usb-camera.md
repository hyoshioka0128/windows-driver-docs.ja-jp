---
title: USB カメラからの静止画のキャプチャ
description: USB カメラからの静止画のキャプチャ
ms.assetid: 762021ea-753c-4cd2-9eec-1403ee918d4e
keywords:
- Windows 2000 カーネル ストリーミング モデル WDK、USBCAMD2 ミニドライバー ライブラリ
- ストリーミング モデル WDK Windows 2000 カーネル、USBCAMD2 ミニドライバー ライブラリ
- カーネル ストリーミング モデルの WDK、USBCAMD2 ミニドライバー ライブラリ
- WDK Windows 2000 のカーネル ストリーミング USBCAMD2 ミニドライバー ライブラリ
- USB ベースのストリーミング カメラ WDK USBCAMD2
- カメラ WDK USBCAMD2
- まだ WDK USBCAMD2 のフレームをキャプチャします。
- フレームはまだ WDK USBCAMD2 をキャプチャします。
- 一括パイプ WDK USBCAMD2
- プッシュ モデル WDK USBCAMD2
- プル モデル WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcc85bc6fa240e59496d1d72dda61d584ddacfbd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386661"
---
# <a name="capturing-still-frames-from-a-usb-camera"></a>USB カメラからの静止画のキャプチャ





USBCAMD2、別の機能を提供する[静止画像ドライバー](https://docs.microsoft.com/windows-hardware/drivers/image/still-image-drivers)カメラの一括パイプを介してカメラからまだフレームを取得します。

***<em>まだフレームのキャプチャをサポートするためには、USBCAMD2 ミニドライバーを次に実行する必要があります。</em>***

-   呼び出す[ *USBCAMD\_BulkReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pfnusbcamd_bulkreadwrite) 、PROPSETID から\_しました\_VIDEOCONTROL プロパティ ハンドラーにミニドライバーに割り当てられたバッファーへのポインターを渡すと静止画像をキャプチャできます。 ポインターがある必要がありますいない**NULL**します。

-   USBCAMD2 を呼び出して、ミニドライバーの[ *CamNewVideoFrameEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_new_frame_routine_ex)一括転送を開始する前に、コールバック関数。 カメラ ミニドライバーは、実際の静止フレームが DirectShow によって割り当てられた最大サイズ未満であると判断した場合、一括転送の要求されたサイズを縮小できます。

-   一括転送が完了したら、USBCAMD2 呼び出してミニドライバーの[ *CamProcessRawVideoFrameEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_process_raw_frame_routine_ex)追加処理を実行するミニドライバーを許可するコールバック関数。

使用するフレーム データ フローは、引き続き、*プル*モデル。 プルは、アプリケーションは、静止フレームを要求したときに発生します。 または、まだフレーム データ フロー内でも、*プッシュ*モデル。 プッシュは、ユーザーにプッシュ ボタン、カメラ デバイス イベントをトリガーするときに発生します。

*<strong>* 使用する、* * *</strong>プル** * * *、STI ミニドライバー * * * から取得するモデルがまだフレーム

-   カメラに関連付けられている WDM ビデオ キャプチャ ソース フィルターを開きます。

-   前の手順で取得されたフィルター ハンドルでまだ暗証番号 (pin) を開きます。

-   呼び出す**ReadFile**の最大サイズのバッファーでは、その pin。

-   一時停止から実行するように、ストリームの状態を設定します。

-   USBCAMD2 カメラ ミニドライバーのインターフェイス ポインターを取得[PROPSETID\_しました\_VIDEOCONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videocontrol)プロパティ セット。

-   設定、 *KS\_VideoControlFlag\_トリガー*に関連付けられているフラグ[ **KSPROPERTY\_VIDEOCONTROL\_モード**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-mode).

*<strong>* サポートするために、* * *</strong>プッシュ** * * * を取得するモデルは、まだカメラ * からフレーム

-   渡す、 *USBCAMD\_CamControlFlag\_EnableDeviceEvents*フラグを呼び出すときに[ **USBCAMD\_InitializeNewInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_initializenewinterface)からミニドライバーの SRB 内\_初期化\_デバイス ハンドラー。 ミニドライバー処理 SRB\_初期化\_内からデバイスの[ *AdapterReceivePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-padapter_receive_packet_routine)コールバック関数。

-   USBCAMD2 送信、 [ **KSEVENT\_VIDCAPTOSTI\_EXT\_トリガー** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vidcaptosti-ext-trigger)イベント、ユーザーに、[トリガー] ボタンをプッシュするときに、登録済みのイメージング アプリケーションをカメラ。

要求された一括読み取りまたは書き込みを取り消す場合は、アプリケーションを呼び出す必要があります**CancelIO**静止暗証番号 (pin) へのハンドルをします。 アプリケーションを呼び出す必要があります (USB 一括アウト パイプ) 経由のカメラに転送する必要があるテーブル場合、 **WriteFile**静止暗証番号 (pin) へのハンドルをします。

 

 




