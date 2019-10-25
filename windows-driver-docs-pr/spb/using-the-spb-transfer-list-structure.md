---
title: カスタム IOCTL に対する SPB_TRANSFER_LIST 構造体の使用
description: シンプルな周辺機器バス (SPB) コントローラードライバーで1つ以上のカスタム i/o 制御 (IOCTL) 要求がサポートされている場合は、SPB_TRANSFER_LIST 構造体を使用して、これらの要求の読み取りバッファーと書き込みバッファーを記述します。
ms.assetid: 577122CC-D1F8-41C5-BE77-A22FC8516B82
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db2c5048a1d3c0ad49e880f31d57a5bfc6bddc30
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839620"
---
# <a name="using-the-spb_transfer_list-structure-for-custom-ioctls"></a>カスタム Ioctl の SPB\_TRANSFER\_LIST 構造の使用


シンプルな周辺機器バス (SPB) コントローラードライバーで1つ以上のカスタム i/o 制御 (IOCTL) 要求がサポートされている場合は、 [**SPB\_TRANSFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list)構造体を使用して、これらの要求の読み取りバッファーと書き込みバッファーを記述します。 この構造体は、要求内のバッファーを記述するための統一された方法を提供し、メソッド\_バッファー i/o 操作に関連するバッファーコピーのオーバーヘッドを回避します。

カスタム IOCTL 要求で**spb\_TRANSFER\_LIST**構造体を使用する場合、spb コントローラードライバーは、要求のプロセスコンテキストでこれらのバッファーをキャプチャするために[**SpbRequestCaptureIoOtherTransferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbrequestcaptureioothertransferlist)メソッドを呼び出す必要があります。送信者. ドライバーは、これらのバッファーにアクセスするために、 [**Spbrequestgettransferparameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbrequestgettransferparameters)メソッドを呼び出すことができます。

[**Ioctl\_spb\_完全\_双**](https://msdn.microsoft.com/library/windows/hardware/hh974774)方向および[**ioctl\_Spb\_** ](https://msdn.microsoft.com/library/windows/hardware/hh450857) 、 [sp b i/o 要求インターフェイス](https://docs.microsoft.com/previous-versions/hh698224(v=vs.85))の一部として定義されている\_シーケンス要求を実行\_@no__ の転送を使用**t_13_** の読み取りバッファーと書き込みバッファーを記述する構造体。 **IOCTL\_spb\_FULL\_双**方向要求の **\_のリスト構造\_転送**は、書き込みバッファーと、要求内の読み取りバッファーの両方を記述します。 **\_シーケンス要求を実行する IOCTL\_\_spb**の**spb\_TRANSFER\_LIST**構造体は、任意のシーケンスの読み取りバッファーと書き込みバッファーを記述できます。

同様に、カスタム Ioctl を定義して、その**SPB\_転送**し、読み取りバッファーと書き込みバッファーの組み合わせを使用するようにリスト構造\_転送する必要があります。また、必要に応じてリスト内のバッファーの順序を指定することもできます。

SPB 周辺機器のカーネルモードドライバー基盤 (KMDF) ドライバーは、 [**Wdfiotargetsendioctlsynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously)のメソッドを同期的に呼び出して、IOCTL 要求を spb コントローラーに送信します。 このメソッドには、 *InputBuffer*パラメーターと*outputbuffer*パラメーターがあります。 一部の種類のデバイスのドライバーでは、これら2つのパラメーターを使用して、IOCTL 要求に対してそれぞれ書き込みバッファーと読み取りバッファーをポイントすることがあります。 ただし、IOCTL 要求を SPB コントローラーに送信するために、SPB 周辺機器ドライバーは、 *InputBuffer*パラメーターを設定して、 **spb\_転送\_リスト**構造を指すメモリ記述子をポイントします。 この構造体は、i/o 制御操作に必要な読み取りバッファーまたは書き込みバッファーを記述します。 ドライバーは*Outputbuffer*パラメーターを NULL に設定します。

同様に、SPB 周辺機器のユーザーモードドライバー基盤 (UMDF) ドライバーは、 [**Iwdfiotarget:: FormatRequestForIoctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl)などのメソッドを呼び出して、i/o 制御操作の i/o 要求の形式を設定します。 このメソッドには、 *Pinputmemory*パラメーターと*poutputmemory*パラメーターがあります。 一部の種類のデバイスのドライバーでは、これら2つのパラメーターを使用して、IOCTL 要求の書き込みバッファーと読み取りバッファーをポイントする場合があります。 ただし、spb コントローラーに IOCTL 要求を送信するために、SPB 周辺機器ドライバーは、 *Pinputmemory*パラメーターを、 **spb\_TRANSFER\_LIST**構造体を含むメモリオブジェクトを指すように設定します。 この構造体は、i/o 制御操作に必要な読み取りバッファーまたは書き込みバッファーを記述します。 ドライバーは*Poutputmemory*パラメーターを NULL に設定します。

## <a name="parameter-checking-and-buffer-capture"></a>パラメーターチェックとバッファーキャプチャ


SPB フレームワーク拡張機能 (SpbCx) が **\_シーケンス要求を実行\_IOCTL\_spb**を受け取ると、この要求は、ドライバーの[*EvtSpbControllerIoSequence*](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_sequence)関数を呼び出すことによって、spb コントローラードライバーに渡されます。 この呼び出しの前に、SpbCx は SPB を検査して、要求内のバッファーを記述する **\_リスト構造を\_転送**します。 SpbCx は、要求の発信元のプロセスコンテキストでこれらのバッファーをキャプチャします。 (ユーザーモードメモリ内のバッファーには、メモリが割り当てられているプロセス内でのみアクセスできます)。さらに、SpbCx は、要求のパラメーター値が有効かどうかを確認します。

SpbCx が完全\_双方向の要求またはカスタム IOCTL 要求 **\_の ioctl\_spb**を受け取ると、この要求は、ドライバーの[*EvtSpbControllerIoOther*](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_other) callback 関数を呼び出すことによって spb コントローラードライバーに渡されます。 この呼び出しを行う前に、SpbCx は要求内のパラメーター値の検証チェックを行わず、発信元のコンテキストで要求のバッファーをキャプチャしません。 これらの要求のパラメーターチェックとバッファーキャプチャは、SPB コントローラードライバーの役割です。

SPB コントローラードライバーが、**完全\_双方向要求\_IOCTL\_spb**をサポートしている場合、または、 **\_sp b**を使用してバッファーの\_リスト構造を転送するカスタム IOCTL 要求がサポートされている場合、ドライバーはを実装する必要があります。[*Evtioincallercontext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)コールバック関数。 ドライバーは、この関数へのポインターを入力パラメーターとして提供します。このメソッドは、ドライバーの*EvtSpbControllerIoOther* callback 関数を登録する[**spbコントローラー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbcontrollersetioothercallback)を呼び出します。 SpbCx が、完全\_双方向の要求またはカスタム IOCTL 要求 **\_の ioctl\_SPB**を受け取ると、SpbCx は、発信者のコンテキストでドライバーの*Evtioincallercontext*関数を呼び出します。 IOCTL 要求で**SPB\_TRANSFER\_LIST**構造体が使用されている場合、 *Evtioincallercontext*関数は、要求内のバッファーをキャプチャするために[**SpbRequestCaptureIoOtherTransferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbrequestcaptureioothertransferlist)メソッドを呼び出します。 また、 *Evtioincallercontext*関数は、要求の一部の予備処理も実行できます。

次のコード例は、SPB コントローラードライバーによって実装される*Evtioincallercontext*関数を示しています。

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

前のコード例では、 **switch**ステートメントは、SPB コントローラードライバーが認識する IOCTL が要求に含まれていることを確認します。 (簡潔にするために、 **switch**ステートメントの本体は表示されません)。次に、 **SpbRequestCaptureIoOtherTransferList**メソッドの呼び出しによって、要求内のバッファーがキャプチャされます。 この呼び出しが成功すると、要求は SPB コントローラーの i/o キューに追加されます。 それ以外の場合、要求はエラー状態コードを使用して完了します。

*EvtSpbControllerIoOther*関数によるパラメーターチェックを示す[コード例](https://docs.microsoft.com/windows-hardware/drivers/spb/handling-ioctl-spb-full-duplex-requests#code-example)については、「 [**完全\_双方向要求\_IOCTL\_SPB**の処理](https://docs.microsoft.com/windows-hardware/drivers/spb/handling-ioctl-spb-full-duplex-requests)」を参照してください。

 

 




