---
title: 等時性パイプを使用したデータ フロー
description: 等時性パイプを使用したデータ フロー
ms.assetid: a66f4191-53ce-4ca2-aae7-8fb24a1a9a16
keywords:
- アイソクロナス パイプ WDK USBCAMD2
- Windows 2000 カーネル ストリーミング モデル WDK、USBCAMD2 ミニドライバー ライブラリ
- ストリーミング モデル WDK Windows 2000 カーネル、USBCAMD2 ミニドライバー ライブラリ
- カーネル ストリーミング モデルの WDK、USBCAMD2 ミニドライバー ライブラリ
- WDK Windows 2000 のカーネル ストリーミング USBCAMD2 ミニドライバー ライブラリ
- USB ベースのストリーミング カメラ WDK USBCAMD2
- カメラ WDK USBCAMD2
- データ フローの WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bcc93205206201c3e356647d50938116d16efab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376384"
---
# <a name="data-flow-using-isochronous-pipes"></a>等時性パイプを使用したデータ フロー





USBCAMD2 32 パケットの 2 つの転送を要求することによってアイソクロナス パイプでストリーミングを開始します。 各パケットでは、選択した別の設定の最大サイズに対応する最大サイズがあります。

**注**  アイソクロナス パイプでストリーミングは Microsoft DirectShow のストリーミングに依存しません。

 

ダブル バッファー isochronous 転送の要求では、USBCAMD2 に継続的に送信され、停止のみ次の 2 つの条件のいずれかが発生した場合。

1.  DirectShow のストリームの状態、停止が発行されます (KSSTATE\_停止) します。

2.  カメラ ミニドライバー要求、USBCAMD を渡すことによって isochronous ストリーミングを停止 USBCAMD2\_停止\_ストリーミング フラグ、 *PipeStateFlags*への呼び出しでパラメーター [ *USBCAMD\_SetIsoPipeState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pfnusbcamd_setisopipestate)します。

ストリーミングは、進行中は、USBCAMD2 とカメラ ミニドライバー繰り返します、次のプロセスまで、ストリーミングを停止します。

1.  USBCAMD2 呼び出しカメラ ミニドライバーの[ *CamProcessUSBPacketEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_process_packet_routine_ex)コールバック関数 (IRQL = ディスパッチ\_レベル)、USB バス ドライバーから USBCAMD2 を受信するすべてのパケットの。 カメラのミニドライバーは、エラー状態の場合適切なエラー フラグを設定する必要があります。 使用して、新しいビデオ フレームの先頭が検出された場合、ミニドライバーは新しいビデオ フレーム フラグを設定も必要があります、 *FrameComplete*パラメーターの**CamProcessUSBPacketEx**します。

2.  カメラ ミニドライバーは、ビデオ フレームが完了したことが決定されます、USBCAMD2 呼び出してカメラ ミニドライバーの[ *CamProcessRawVideoFrameEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_process_raw_frame_routine_ex) (ワーカー スレッドのコンテキスト) からのコールバック関数色空間変換または圧縮解除を実行する必要がある場合は、ビデオのフレームを処理します。 USBCAMD2 が完了した生フレームを返します、 *stream.sys* IRQL でカメラ ミニドライバーによって処理されるクラス ドライバー = パッシブ\_レベル。 フレームが不足しているデータがあるか、無効なデータのための圧縮解除中にエラーがなどが発生しました、 *BytesReturned*パラメーターを**CamProcessRawVideoFrameEx**を 0 に設定する必要があります。

 

 




