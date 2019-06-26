---
title: カスタム IOCTL に対する SPB_TRANSFER_LIST 構造体の使用
description: シンプルな周辺機器バス (SPB) コント ローラーのドライバーでは、1 つ以上のカスタム I/O 制御 (IOCTL) 要求をサポートする場合は、SPB_TRANSFER_LIST 構造を使用して、読み取りを記述し、これらの要求でバッファーを記述します。
ms.assetid: 577122CC-D1F8-41C5-BE77-A22FC8516B82
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47fc55613b702f848d12368e434e9f19b2c1c8a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383493"
---
# <a name="using-the-spbtransferlist-structure-for-custom-ioctls"></a>SPB を使用して\_転送\_カスタム Ioctl のリストの構造


シンプルな周辺機器バス (SPB) コント ローラーのドライバーが 1 つをサポートまたは複数のカスタム I/O 制御 (IOCTL) を要求、使用、 [ **SPB\_転送\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spb/ns-spb-spb_transfer_list)構造を記述する、これらの要求でバッファーを読み書きします。 この構造体は、要求内のバッファーを記述する一貫した方法を提供し、バッファーのコピー メソッドに関連付けられたオーバーヘッドを回避できます\_バッファー I/O 操作。

カスタム、IOCTL が使用を要求した場合、 **SPB\_転送\_一覧**SPB コント ローラーのドライバーを呼び出す必要があります、構造、 [ **SpbRequestCaptureIoOtherTransferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nf-spbcx-spbrequestcaptureioothertransferlist)メソッド要求の送信元のプロセスのコンテキストでこれらのバッファーをキャプチャします。 ドライバーを呼び出すことができます、 [ **SpbRequestGetTransferParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nf-spbcx-spbrequestgettransferparameters)これらのバッファーにアクセスするメソッド。

[ **IOCTL\_SPB\_完全\_双方向**](https://msdn.microsoft.com/library/windows/hardware/hh974774)と[ **IOCTL\_SPB\_EXECUTE\_シーケンス**](https://msdn.microsoft.com/library/windows/hardware/hh450857) 、要求の一部として定義されている、 [SPB の I/O 要求インターフェイス](https://docs.microsoft.com/previous-versions/hh698224(v=vs.85))を使用して、 **SPB\_転送\_一覧**説明の読み取りおよび書き込みバッファーの構造体。 **SPB\_転送\_一覧**用の構造、 **IOCTL\_SPB\_完全\_双方向**要求には、書き込みバッファーがについて説明します、要求に (この順序で) で読み取りバッファー。 **SPB\_転送\_一覧**用の構造、 **IOCTL\_SPB\_EXECUTE\_シーケンス**要求を任意に記述できますシーケンスでは、読み取りおよび書き込みバッファー。

同様を必要とする、カスタムの Ioctl を定義することができます、 **SPB\_転送\_一覧**読み取りのいくつかの組み合わせを使用し、バッファーの書き込みと一覧内のバッファーの任意の順序の指定の構造を必要な場合があります。

SPB の周辺機器のカーネル モード ドライバー Foundation (KMDF) ドライバーなどのメソッドの呼び出し[ **WdfIoTargetSendIoctlSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously) SPB コント ローラーに IOCTL 要求を送信します。 このメソッドは*InputBuffer*と*OutputBuffer*パラメーター。 一部の種類のデバイス ドライバーは、これら 2 つのパラメーターを使用して、書き込みバッファーを指すを IOCTL 要求のそれぞれに、バッファーを読み取る可能性があります。 ただし、SPB コント ローラーに IOCTL 要求を送信する SPB の周辺機器のデバイス ドライバ設定、 *InputBuffer*パラメーターが指すメモリ記述子を**SPB\_転送\_リスト**構造体。 構造体が記述いずれかの読み取りまたは書き込み I/O の管理操作に必要なバッファー。 ドライバーのセット、 *OutputBuffer*パラメーターを NULL にします。

同様に、メソッドを呼び出す SPB の周辺機器デバイスのユーザー モード ドライバー Foundation (UMDF) ドライバーなど[ **IWDFIoTarget::FormatRequestForIoctl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl) I/O コントロールの I/O 要求を書式設定するには操作です。 このメソッドは*pInputMemory*と*pOutputMemory*パラメーター。 一部の種類のデバイス ドライバーは、これら 2 つのパラメーターを使用して、書き込みバッファーをポイントして、IOCTL 要求用のバッファーを読み取る可能性があります。 ただし、SPB コント ローラーに IOCTL 要求を送信する SPB の周辺機器のデバイス ドライバ設定、 *pInputMemory*パラメーターを格納しているメモリ オブジェクトを指す、 **SPB\_転送\_一覧**構造体。 構造体が記述いずれかの読み取りまたは書き込み I/O の管理操作に必要なバッファー。 ドライバーのセット、 *pOutputMemory*パラメーターを NULL にします。

## <a name="parameter-checking-and-buffer-capture"></a>パラメーターのチェックとバッファーのキャプチャ


SPB フレームワーク拡張機能 (SpbCx) を受信すると、 **IOCTL\_SPB\_EXECUTE\_シーケンス**要求、SpbCx SPB コント ローラーのドライバーをドライバーのを呼び出すことによってこの要求を通過する[ *EvtSpbControllerIoSequence* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_controller_sequence)関数。 SpbCx を調べ、この呼び出しの前に、 **SPB\_転送\_一覧**要求内のバッファーを記述する構造体。 SpbCx では、要求の送信元のプロセスのコンテキストでこれらのバッファーをキャプチャします。 (ユーザー モードのメモリ内のバッファーはメモリを割り当てがプロセスでのみアクセスできます)。さらに、SpbCx は、要求内のパラメーター値が有効かどうかを確認します。

SpbCx を受信すると、 **IOCTL\_SPB\_完全\_双方向**IOCTL 要求の要求またはカスタム、SpbCx SPB コント ローラーのドライバーを呼び出してドライバーのこの要求を通過する[ *EvtSpbControllerIoOther* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_controller_other)コールバック関数。 この呼び出しを行う前に SpbCx は、要求内のパラメーター値の検証は行われません、発信元のコンテキストでは、要求のバッファーをキャプチャしません。 これらの要求パラメーターをチェックし、バッファーのキャプチャでは、SPB コント ローラーのドライバーの役目です。

SPB のコント ローラー ドライバーがサポートしている場合、 **IOCTL\_SPB\_完全\_双方向**要求、またはを使用するカスタムの IOCTL 要求をサポートしている、 **SPB\_転送\_リスト**構造、そのバッファーのドライバーを実装する必要があります、 [ *EvtIoInCallerContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)コールバック関数。 ドライバーによって、この関数へのポインターへの呼び出しの入力パラメーターとして、 [ **SpbControllerSetIoOtherCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nf-spbcx-spbcontrollersetioothercallback)ドライバーの登録メソッド*EvtSpbControllerIoOther*コールバック関数。 SpbCx を受信すると、 **IOCTL\_SPB\_完全\_双方向**IOCTL 要求の要求またはカスタム、SpbCx 呼び出しのドライバーの*EvtIoInCallerContext*関数で、発信元のコンテキスト。 IOCTL 要求で使用する場合、 **SPB\_転送\_一覧**構造、 *EvtIoInCallerContext*関数呼び出し、 [ **SpbRequestCaptureIoOtherTransferList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nf-spbcx-spbrequestcaptureioothertransferlist)要求内のバッファーをキャプチャするメソッド。 *EvtIoInCallerContext*関数は、要求のいくつかの暫定的な処理も実行可能性があります。

次のコード例は、 *EvtIoInCallerContext* SPB のコント ローラー ドライバーによって実装されている関数。

```cpp
VOID
EvtIoInCallerContext(
    _In_  WDFDEVICE   SpbController,
    _In_  WDFREQUEST  FxRequest
    ) 
{
    NTSTATUS status = STATUS_SUCCESS;
    WDF_REQUEST_PARAMETERS fxParams;
  
    WDF_REQUEST_PARAMETERS_INIT(&fxParams);
    WdfRequestGetParameters(FxRequest, &fxParams);

    if ((fxParams.Type != WdfRequestTypeDeviceControl) &&
        (fxParams.Type != WdfRequestTypeDeviceControlInternal))
    {
        status = STATUS_NOT_SUPPORTED;
        goto exit;
    }

    //
    // The driver should check for custom IOCTLs that it handles.
    // If the IOCTL is not recognized, complete the request with a
    // status of STATUS_NOT_SUPPORTED.
    //

    switch (fxParams.Parameters.DeviceIoControl.IoControlCode)
    {
        ...

    default:
        status = STATUS_NOT_SUPPORTED;
        goto exit;
    }

    //
    // The IOCTL is recognized. Capture the buffers in the request.
    //

    status = SpbRequestCaptureIoOtherTransferList((SPBREQUEST)FxRequest);

    //
    // If the capture fails, the driver must complete the request instead
    // of placing it in the SPB controller's request queue.
    //

    if (!NT_SUCCESS(status))
    {
        goto exit;
    }

    status = WdfDeviceEnqueueRequest(SpbController, FxRequest);

    if (!NT_SUCCESS(status))
    {
        goto exit;
    }

exit:

    if (!NT_SUCCESS(status))
    {
        WdfRequestComplete(FxRequest, status);
    }
}
```

上記のコード例で、**切り替える**ステートメントでは、IOCTL SPB のコント ローラー ドライバーが認識するが、要求に含まれていることを確認します。 (簡潔にするため、本文、**切り替える**ステートメントが示されていません)。次への呼び出し、 **SpbRequestCaptureIoOtherTransferList**メソッドは、要求内のバッファーをキャプチャします。 この呼び出しに成功した場合は、要求が SPB コント ローラーの I/O キューに追加されます。 それ以外の場合、要求がエラー状態コードで完了します。

[のコード例](https://docs.microsoft.com/windows-hardware/drivers/spb/handling-ioctl-spb-full-duplex-requests#code-example)パラメーターによってチェックを示す、 *EvtSpbControllerIoOther*関数を参照してください[処理**IOCTL\_SPB\_完全\_双方向**要求](https://docs.microsoft.com/windows-hardware/drivers/spb/handling-ioctl-spb-full-duplex-requests)します。

 

 




