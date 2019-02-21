---
Description: Best practices for a host controller driver for handling I/O requests sent by UCX.
title: USB ホスト コント ローラー ドライバーでの I/O 要求を処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1e2837d698a81d8fa27820b7b5c62d168901217
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553129"
---
# <a name="handle-io-requests-in-a-usb-host-controller-driver"></a>USB ホスト コント ローラー ドライバーでの I/O 要求を処理します。


ホスト コント ローラーのドライバーを UCX から送信された I/O 要求を処理するためのベスト プラクティス。

UCX の追跡、USB バス上のデバイス用のホスト コント ローラー ドライバーによって作成されたすべてのエンドポイント。 ハブのドライバーまたは別のドライバーは、USB デバイス スタックの上位にある送信データ転送要求は最初 UCX によって処理されます。 UCX は適切なエンドポイントのキューに framework 要求オブジェクトを転送します。 要求に含まれている USB 要求ブロック (URB)、エンドポイントのハンドルを指定できます。 場合は、エンドポイントのハンドルを指定すると、デバイスの現在のエンドポイント間で、対応するエンドポイントの UCX を確認します。 指定したエンドポイントのハンドルが存在する場合、要求は、エンドポイントのキューに転送されます。 指定したエンドポイントのハンドルが存在しない場合、要求が失敗しました。 ハンドルが指定されていない場合は、要求は、既定のエンドポイントに対するし UCX がそのデバイスのホスト コント ローラー ドライバーの既定のエンドポイントのキューに要求を転送します。

既存の USB ドライバーとの互換性のために、URB 要求の完了時にホスト コント ローラーが、次の要件に準拠する必要があります。

-  [**WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)ディスパッチで呼び出す必要がある\_レベル。
-   URB がそのフレームワークのキューに配信されたドライバーは、同期的に、呼び出し元のドライバーのスレッドまたは DPC の処理が開始した場合は、要求も完了できません同期的にします。 呼び出しをスケジュールできる個別の DPC に要求を完了する必要があります[ **WdfDpcEnqueue**](https://msdn.microsoft.com/library/windows/hardware/ff547148)します。
-   受信すると、上記の要件のような[ **EVT_WDF_IO_QUEUE_IO_CANCELED_ON_QUEUE** ](https://msdn.microsoft.com/library/windows/hardware/ff541756)または[ **EVT_WDF_REQUEST_CANCEL** ](https://msdn.microsoft.com/library/windows/hardware/ff541817)、ホスト コント ローラーのドライバーは、呼び出し元のスレッドから別の DPC または DPC URB 要求を完了する必要があります。 既定では、WDF では、キューで取り消された要求が同期的に完了します。 その動作 URB 要求の問題が発生する可能性があります。 このため、ドライバーが提供する必要があります、 *EvtIoCanceledOnQueue* URB キューのコールバック。

フレームワークの要求オブジェクト、 [ **IOCTL\_内部\_USB\_送信\_URB** ](https://msdn.microsoft.com/library/windows/hardware/ff537271)にある、URB を含む**Parameters.Others.Arg1**の要求。 か USBD に URB 状態を設定する必要があります、要求が完了したら、\_状態\_成功した場合、または、エラーの性質を示すエラー状態にします。 失敗の状態値は、usb.h ヘッダー ファイルで定義されます。

## <a name="related-topics"></a>関連トピック
[USB ホスト コント ローラーの Windows ドライバーの開発](developing-windows-drivers-for-usb-host-controllers.md)  



