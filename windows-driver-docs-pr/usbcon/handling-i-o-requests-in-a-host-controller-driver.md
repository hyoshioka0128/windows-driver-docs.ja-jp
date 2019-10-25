---
Description: UCX によって送信された i/o 要求を処理するためのホストコントローラードライバーのベストプラクティス。
title: USB ホスト コントローラー ドライバーでの I/O 要求の処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eaceb81d948704c0ab0df6b9ff872f043f99d739
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844999"
---
# <a name="handle-io-requests-in-a-usb-host-controller-driver"></a>USB ホスト コントローラー ドライバーでの I/O 要求の処理


UCX によって送信された i/o 要求を処理するためのホストコントローラードライバーのベストプラクティス。

UCX は、USB バス上のデバイスのホストコントローラードライバーによって作成されたすべてのエンドポイントを追跡します。 ハブドライバーまたは USB デバイススタックの上位にある別のドライバーによって送信されたすべてのデータ転送要求は、最初に UCX によって処理されます。 UCX は、フレームワークの要求オブジェクトを適切なエンドポイントキューに転送します。 要求に含まれる USB 要求ブロック (URB) は、エンドポイントハンドルを指定できます。 エンドポイントハンドルが指定されている場合、UCX は、デバイスに存在するエンドポイント間で対応するエンドポイントをチェックします。 指定されたエンドポイントハンドルが存在する場合、要求はエンドポイントのキューに転送されます。 指定されたエンドポイントハンドルが見つからない場合、要求は失敗します。 ハンドルが指定されていない場合、要求は既定のエンドポイントに対して行われ、UCX はそのデバイスのホストコントローラードライバーの既定のエンドポイントキューに要求を転送します。

既存の USB ドライバーとの互換性を確保するには、ホストコントローラーが URB 要求を完了するときに、次の要件を満たしている必要があります。

-  [**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)はディスパッチ\_レベルで呼び出す必要があります。
-   URB がフレームワークキューに配信され、ドライバーが呼び出し元ドライバーのスレッドまたは DPC で同期処理を開始した場合、要求も同期的に完了する必要はありません。 要求は別の DPC で完了する必要があります。これは、 [**Wdfdpcenqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nf-wdfdpc-wdfdpcenqueue)を呼び出すことでスケジュールできます。
-   前の要件と同様に、 [**EVT_WDF_IO_QUEUE_IO_CANCELED_ON_QUEUE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue)または[**EVT_WDF_REQUEST_CANCEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)を受け取ると、ホストコントローラードライバーは、呼び出し元のスレッドまたは dpc とは別の dpc で URB 要求を完了する必要があります。 既定では、WDF はキューでのキャンセルされた要求を同期的に完了します。 その動作によって、URB 要求の問題が発生する可能性があります。 このため、ドライバーは、URB キューの*EvtIoCanceledOnQueue*コールバックを提供する必要があります。

[**IOCTL\_内部\_USB\_送信\_urb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb)のフレームワーク要求オブジェクトには、パラメーターにある urb が含まれています **。** 要求が完了したら、URB ステータスを [USBD\_STATUS\_SUCCESS] に設定するか、エラーの性質を示すエラー状態に設定する必要があります。 エラー状態の値は、usb .h ヘッダーファイルで定義されています。

## <a name="related-topics"></a>関連トピック
[USB ホスト コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-host-controllers.md)  



