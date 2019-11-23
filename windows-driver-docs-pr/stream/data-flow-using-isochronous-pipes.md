---
title: 等時性パイプを使用したデータ フロー
description: 等時性パイプを使用したデータ フロー
ms.assetid: a66f4191-53ce-4ca2-aae7-8fb24a1a9a16
keywords:
- アイソクロナスパイプ WDK USBCAMD2
- Windows 2000 カーネルストリーミングモデル WDK、USBCAMD2 ミニドライバーライブラリ
- ストリーミングモデル WDK Windows 2000 カーネル、USBCAMD2 ミニドライバーライブラリ
- カーネルストリーミングモデル WDK、USBCAMD2 ミニドライバーライブラリ
- USBCAMD2 ミニドライバー library WDK Windows 2000 カーネルストリーミング
- USB ベースのストリーミングカメラの WDK USBCAMD2
- カメラ WDK USBCAMD2
- データフロー WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7ddf3eaf87bd2d1890855fbd8b233d95c8547fd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845065"
---
# <a name="data-flow-using-isochronous-pipes"></a>等時性パイプを使用したデータ フロー





USBCAMD2 は、32パケットの2つの転送を要求することによって、アイソクロナスパイプのストリーミングを開始します。 各パケットの最大サイズは、選択した代替設定の最大サイズに対応しています。

**   アイソクロナス**パイプでのストリーミングは、Microsoft DirectShow Streaming に依存しません。

 

ダブルバッファーのアイソクロナス転送要求は USBCAMD2 に継続的に送信され、次の2つの条件のいずれかが発生した場合にのみ停止します。

1.  DirectShow ストリームの停止状態が発行されます (KSK 状態\_停止)。

2.  カメラミニドライバーは、 [*USBCAMD\_SetIsoPipeState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pfnusbcamd_setisopipestate)の呼び出しで*PIPESTATEFLAGS*パラメーターに USBCAMD\_stop\_streaming フラグを渡すことによって、アイソクロナスストリーミングを停止するように USBCAMD2 に要求します。

ストリーミングの進行中、USBCAMD2 とカメラミニドライバーは、ストリーミングが停止するまで、次のプロセスを繰り返します。

1.  USBCAMD2 は、USB バスドライバーから USBCAMD2 が受信するすべてのパケットについて、カメラミニドライバーの[*CamProcessUSBPacketEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_process_packet_routine_ex)コールバック関数 (IRQL = ディスパッチ\_レベル) を呼び出します。 カメラミニドライバーは、エラー状態の場合に適切なエラーフラグを設定する必要があります。 **CamProcessUSBPacketEx**の*FrameComplete*パラメーターを使用して新しいビデオフレームの先頭が検出された場合、ミニドライバーは新しいビデオフレームフラグも設定する必要があります。

2.  カメラミニドライバーがビデオフレームが完了したと判断した後、USBCAMD2 は、(ワーカースレッドのコンテキストから) カメラミニドライバーの[*CamProcessRawVideoFrameEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_process_raw_frame_routine_ex)コールバック関数を呼び出して、色空間の変換または圧縮解除を実行する必要がある場合にビデオフレームを処理します。 USBCAMD2 は、ミニドライバークラスドライバーに完了した未加工のフレームを返し*ます。これ*は、カメラによって処理され、IRQL = パッシブ\_レベルで実行されます。 フレームデータが不足している場合や、不適切なデータが原因で圧縮解除中にエラーが発生した場合などは、 **CamProcessRawVideoFrameEx**に*返された bytesreturned*を0に設定する必要があります。

 

 




