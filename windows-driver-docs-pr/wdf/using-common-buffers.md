---
title: 共通バッファーの使用
description: 共通バッファーの使用
ms.assetid: 81a56f62-917e-4798-b2cc-6469c802fab8
keywords:
- DMA 操作 WDK KMDF、共通バッファー
- バスマスタ DMA WDK KMDF、共通バッファー
- common buffers WDK KMDF
- WDK KMDF のバッファー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8a07775256f67dcaaa9eaeb53ef0dec4882483a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843096"
---
# <a name="using-common-buffers"></a>共通バッファーの使用


\[は KMDF にのみ適用され\]




DMA デバイスのドライバーは、デバイスとドライバーの両方がアクセスできるバッファー領域を割り当てることが必要になる場合があります。 たとえば、デバイスがバイト数などの転送情報をこのバッファー領域に書き込み、ドライバーがそれを読み取って転送されたバイト数を確認できる場合があります。 この種類のバッファー領域は、*共通バッファー*と呼ばれます。

共通のバッファーを割り当てるには、ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数を使用します。

-   [**WdfDmaEnablerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)を呼び出して、DMA イネーブラーオブジェクトを作成します。

-   バッファーを作成するには、 [**Wdfcommonbuffercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffercreate)または[**Wdfcommonbuffercreatewithconfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffercreatewithconfig)を呼び出します。

-   [**WdfCommonBufferGetAlignedLogicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffergetalignedlogicaladdress)を呼び出して、デバイスがアクセスできるバッファーの論理アドレスを取得します。

-   [**WdfCommonBufferGetAlignedVirtualAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffergetalignedvirtualaddress)を呼び出して、ドライバーがアクセスできるバッファーの仮想アドレスを取得します。

次のコード例は、 [PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)サンプルの *.c*ファイルから取得されています。 このコードは、KMDF ドライバーが一般的なバッファー領域を割り当てる方法を示しています。

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

[**WdfDmaEnablerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)を呼び出す前に、ドライバーが[**Wdfdevicesetaligned 要件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetalignmentrequirement)を呼び出すと、 **WdfDmaEnablerCreate**によって作成されるバッファーは、ドライバーによって指定され**たメモリアドレス境界に合わせて調整されます。Wdfdevicesetの要件**。 それ以外の場合、一般的なバッファーは単語のアドレス境界に合わせて調整されます。 また、ドライバーは、 [**Wdfcommonbuffercreatewithconfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffercreatewithconfig)を呼び出して、1つのバッファーのアラインメントを指定することもできます。

ドライバーが割り当てた共通バッファーの長さを取得するために、ドライバーは[**WdfCommonBufferGetLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffergetlength)を呼び出すことができます。

ドライバーが共通のバッファーを使用して終了すると、ドライバーは[**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出します。









