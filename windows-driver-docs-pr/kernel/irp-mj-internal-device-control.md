---
title: IRP_MJ_INTERNAL_DEVICE_CONTROL
description: 一般に、内部デバイス制御要求をサポートする既存のドライバーを置き換える場合は、DispatchInternalDeviceControl ルーチンでこの要求を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: fb3d4534-9c6f-4956-b702-5752f9798600
keywords:
- IRP_MJ_INTERNAL_DEVICE_CONTROL カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: ccb75ac674b75d581212501f3dbfeb71aeb46a10
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828120"
---
# <a name="irp_mj_internal_device_control"></a>IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL


一般に、内部デバイス制御要求をサポートする既存のドライバーを置き換える場合は、 [*DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンでこの要求を処理する必要があります。 このようなドライバーでは、置き換えられるドライバーと同じセットの内部 i/o 制御コードがサポートされている必要があります。 それ以外の場合は、既存の上位レベルのドライバーが新しいドライバーで動作しない可能性があります。

この要求を処理するには、特定の下位レベルのシステムドライバーを置き換えるドライバーが必要です。 たとえば、システムパラレルポートドライバーの代わりに、既存の並列クラスドライバーを引き続きサポートする必要があります。 この要求を処理する特定のシステムドライバーは、特にシステムによって提供される SCSI およびビデオポートドライバーに置き換えることはできないことに注意してください。

<a name="when-sent"></a>送信時
---------

作成要求が正常に完了した後、いつでも。

## <a name="input-parameters"></a>入力パラメーター


I/o 制御コードは、IRP の i/o スタック位置にある**DeviceIoControl**に含まれています。また、

その他の入力パラメーターは、i/o 制御コードの値によって異なります。 詳細については、「 [I/o 制御コードのバッファーの説明](https://docs.microsoft.com/windows-hardware/drivers/kernel/buffer-descriptions-for-i-o-control-codes)」を参照してください。

## <a name="output-parameters"></a>出力パラメーター


出力パラメーターは、i/o 制御コードの値によって異なります。 詳細については、「 [I/o 制御コードのバッファーの説明](https://docs.microsoft.com/windows-hardware/drivers/kernel/buffer-descriptions-for-i-o-control-codes)」を参照してください。

<a name="operation"></a>操作
---------

ドライバーは、 **IRP\_MJ\_内部\_デバイス\_** 、他のドライバーが[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)または[**ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)を呼び出して要求を作成するときに要求を制御します。

この i/o 制御コードは、1つまたは複数のクラスドライバーがポートドライバー上に階層化されている場合など、ペアのカーネルモードドライバー間の通信用に定義されています。 上位レベルのドライバーは、デバイスまたはドライバー固有の i/o 制御コードを使用して Irp を設定し、次に低いドライバーからのサポートを要求します。

要求された操作は、デバイスまたはドライバー固有のものです。

Irp\_MJ の i/o 制御コードに関する一般的な情報については[ **\_デバイス\_control**](irp-mj-device-control.md)または**irp\_MJ\_内部\_デバイス\_コントロール**要求の場合は、「 [i/o 制御コードの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)」を参照してください。 「[デバイスの種類に固有の I/o 要求](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-type-specific-i-o-requests)」も参照してください。

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
<td>Wdm (Wdm .h、Ntddk、または Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)

[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

 

 




