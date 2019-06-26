---
title: 共通バッファーの使用
description: 共通バッファーの使用
ms.assetid: 81a56f62-917e-4798-b2cc-6469c802fab8
keywords:
- DMA 操作 WDK KMDF、一般的なバッファー
- バス マスター DMA WDK KMDF、一般的なバッファー
- 一般的なバッファー WDK KMDF
- バッファー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94cc731c6c5b715894f07cc51796d005d055e771
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372283"
---
# <a name="using-common-buffers"></a>共通バッファーの使用


\[KMDF にのみ適用されます。\]




DMA デバイスも用のドライバーでは、デバイスとドライバーの両方にアクセスできるバッファー領域を割り当てる必要があります。 たとえば、デバイスは、バイト数などの転送情報を書き込む可能性があります、このバッファーに領域と、ドライバーを読み取れる転送されたバイト数を判断するためにします。 バッファーの容量は、この型が呼び出される、*共通バッファー*します。

バッファーを割り当てることを共通のドライバーの[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数。

-   呼び出し[ **WdfDmaEnablerCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate) DMA イネーブラー オブジェクトを作成します。

-   呼び出し[ **WdfCommonBufferCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffercreate)または[ **WdfCommonBufferCreateWithConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffercreatewithconfig)バッファーを作成します。

-   呼び出し[ **WdfCommonBufferGetAlignedLogicalAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffergetalignedlogicaladdress)がデバイスにアクセスできる、バッファーの論理アドレスを取得します。

-   呼び出し[ **WdfCommonBufferGetAlignedVirtualAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffergetalignedvirtualaddress)ドライバーがアクセスできる、バッファーの仮想アドレスを取得します。

次のコード例がから取得した、 *Init.c*のファイル、 [PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)サンプル。 このコードは、KMDF ドライバーでの一般的なバッファー領域の割り当て方法を示しています。

```cpp
// Allocate common buffer for building writes
DevExt->WriteCommonBufferSize = 
         sizeof( DMA_TRANSFER_ELEMENT) * DevExt->WriteTransferElements;
status = WdfCommonBufferCreate( DevExt->DmaEnabler,
                                DevExt->WriteCommonBufferSize,
                                WDF_NO_OBJECT_ATTRIBUTES, 
                                &DevExt->WriteCommonBuffer );
if (!NT_SUCCESS(status)) {
    . . . //Error-handling code omitted 
    }
DevExt->WriteCommonBufferBase = 
             WdfCommonBufferGetAlignedVirtualAddress(
                      DevExt->WriteCommonBuffer);
DevExt->WriteCommonBufferBaseLA = 
             WdfCommonBufferGetAlignedLogicalAddress(
                      DevExt->WriteCommonBuffer);
RtlZeroMemory( DevExt->WriteCommonBufferBase, DevExt->WriteCommonBufferSize);
```

ドライバーを呼び出す場合[ **WdfDeviceSetAlignmentRequirement** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetalignmentrequirement)呼び出す前に[ **WdfDmaEnablerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)バッファーを**WdfDmaEnablerCreate**を作成するドライバーが指定されているメモリ アドレスの境界に揃えられます**WdfDeviceSetAlignmentRequirement**します。 それ以外の場合、共通のバッファーは、アドレスの単語の境界に揃えて配置されます。 ドライバーを呼び出すことができますも[ **WdfCommonBufferCreateWithConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffercreatewithconfig)を 1 つのバッファーの配置を指定します。

ドライバーを呼び出すことができます、ドライバーが割り当てられている一般的なバッファーの長さを取得する[ **WdfCommonBufferGetLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffergetlength)します。

ドライバーが完了すると、一般的なバッファー、ドライバーの呼び出しを使用して[ **WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)します。









