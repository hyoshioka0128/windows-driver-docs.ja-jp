---
title: IRP_MJ_INTERNAL_DEVICE_CONTROL
description: 一般に、内部デバイス制御の要求をサポートする既存のドライバーの置換は DispatchInternalDeviceControl ルーチンでは、この要求を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: fb3d4534-9c6f-4956-b702-5752f9798600
keywords:
- IRP_MJ_INTERNAL_DEVICE_CONTROL カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 4da0c0d69b381c65da3313b80299eb1152f32e35
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370906"
---
# <a name="irpmjinternaldevicecontrol"></a>IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL


一般に、内部デバイス制御の要求をサポートする既存のドライバーの置換がでこの要求を処理する、 [ *DispatchInternalDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。 このようなドライバーは、少なくとも置き換えますドライバーと内部の I/O 制御コードの同じセットをサポートする必要があります。 それ以外の場合、既存のより高度なドライバーは、新しいドライバーでは動作しません。

ドライバーのドライバーは、この要求を処理するために必要な特定の低レベル システムが交換してください。 たとえば、パラレル ポート ドライバーがシステムに代わるものは、parallel クラスの既存のドライバーをサポートするために続ける必要があります。 その特定のシステム ドライバーこの要求の処理を置き換えることができません、具体的には、システム提供の SCSI とドライバーのビデオ ポートに注意してください。

<a name="when-sent"></a>送信時
---------

いつの作成要求が正常に完了後します。

## <a name="input-parameters"></a>入力パラメーター


I/O 制御コードが含まれている**Parameters.DeviceIoControl.IoControlCode** I/O スタック IRP の場所。

その他の入力パラメーターは、I/O 制御コードの値によって異なります。 詳細については、次を参照してください。 [I/O 制御コードの説明をバッファー](https://docs.microsoft.com/windows-hardware/drivers/kernel/buffer-descriptions-for-i-o-control-codes)します。

## <a name="output-parameters"></a>出力パラメーター


出力パラメーターは、I/O 制御コードの値によって異なります。 詳細については、次を参照してください。 [I/O 制御コードの説明をバッファー](https://docs.microsoft.com/windows-hardware/drivers/kernel/buffer-descriptions-for-i-o-control-codes)します。

<a name="operation"></a>操作
---------

ドライバーの受信**IRP\_MJ\_内部\_デバイス\_コントロール**別のドライバーでは、いずれかを呼び出すときに、要求[ **IoBuildDeviceIoControlRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)または[ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)要求を作成します。

この I/O 制御コードは、ペアになっているし、ポートのドライバーの上層に 1 つまたは複数のクラス ドライバーなどのカーネル モード ドライバーの層間の通信用に定義されています。 高度なドライバーは、デバイスまたはドライバー固有 I/O 制御コードは、次の下位ドライバーからサポートを要求すると、Irp を設定します。

要求された操作は、デバイスまたはドライバーに固有です。

I/O に関する一般的な情報のコードを制御[ **IRP\_MJ\_デバイス\_コントロール**](irp-mj-device-control.md)または**IRP\_MJ\_内部\_デバイス\_コントロール**要求を参照してください[I/O 制御コードを使用して](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)します。 参照してください[デバイスの種類に固有の I/O 要求](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-type-specific-i-o-requests)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)

[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

 

 




