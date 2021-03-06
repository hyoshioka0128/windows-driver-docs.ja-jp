---
Description: ホスト コント ローラーのドライバーを UCX から送信された I/O 要求を処理するためのベスト プラクティス。
title: USB ホスト コントローラー ドライバーでの I/O 要求の処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2035fc6a2ce8d3f1d1fba754603e3601377da03d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386261"
---
# <a name="handle-io-requests-in-a-usb-host-controller-driver"></a>USB ホスト コントローラー ドライバーでの I/O 要求の処理


ホスト コント ローラーのドライバーを UCX から送信された I/O 要求を処理するためのベスト プラクティス。

UCX の追跡、USB バス上のデバイス用のホスト コント ローラー ドライバーによって作成されたすべてのエンドポイント。 ハブのドライバーまたは別のドライバーは、USB デバイス スタックの上位にある送信データ転送要求は最初 UCX によって処理されます。 UCX は適切なエンドポイントのキューに framework 要求オブジェクトを転送します。 要求に含まれている USB 要求ブロック (URB)、エンドポイントのハンドルを指定できます。 場合は、エンドポイントのハンドルを指定すると、デバイスの現在のエンドポイント間で、対応するエンドポイントの UCX を確認します。 指定したエンドポイントのハンドルが存在する場合、要求は、エンドポイントのキューに転送されます。 指定したエンドポイントのハンドルが存在しない場合、要求が失敗しました。 ハンドルが指定されていない場合は、要求は、既定のエンドポイントに対するし UCX がそのデバイスのホスト コント ローラー ドライバーの既定のエンドポイントのキューに要求を転送します。

既存の USB ドライバーとの互換性のために、URB 要求の完了時にホスト コント ローラーが、次の要件に準拠する必要があります。

-  [**WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)ディスパッチで呼び出す必要がある\_レベル。
-   URB がそのフレームワークのキューに配信されたドライバーは、同期的に、呼び出し元のドライバーのスレッドまたは DPC の処理が開始した場合は、要求も完了できません同期的にします。 呼び出しをスケジュールできる個別の DPC に要求を完了する必要があります[ **WdfDpcEnqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nf-wdfdpc-wdfdpcenqueue)します。
-   受信すると、上記の要件のような[ **EVT_WDF_IO_QUEUE_IO_CANCELED_ON_QUEUE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue)または[ **EVT_WDF_REQUEST_CANCEL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)、ホスト コント ローラーのドライバーは、呼び出し元のスレッドから別の DPC または DPC URB 要求を完了する必要があります。 既定では、WDF では、キューで取り消された要求が同期的に完了します。 その動作 URB 要求の問題が発生する可能性があります。 このため、ドライバーが提供する必要があります、 *EvtIoCanceledOnQueue* URB キューのコールバック。

フレームワークの要求オブジェクト、 [ **IOCTL\_内部\_USB\_送信\_URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb)にある、URB を含む**Parameters.Others.Arg1**の要求。 か USBD に URB 状態を設定する必要があります、要求が完了したら、\_状態\_成功した場合、または、エラーの性質を示すエラー状態にします。 失敗の状態値は、usb.h ヘッダー ファイルで定義されます。

## <a name="related-topics"></a>関連トピック
[USB ホスト コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-host-controllers.md)  



