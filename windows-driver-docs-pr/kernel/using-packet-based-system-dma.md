---
title: パケットベース システム DMA の使用
description: パケットベース システム DMA の使用
ms.assetid: 5d175193-4a28-49fd-80b5-18f116232c6e
keywords:
- システム DMA WDK カーネル、パケットベース
- パケットベースの DMA WDK カーネル
- DMA 転送 WDK カーネル、パケットベース
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 592acd1025443207d7c83a105e31721814f98bb1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835925"
---
# <a name="using-packet-based-system-dma"></a>パケットベース システム DMA の使用





パケットベースの DMA を使用する下位デバイスのドライバーは、DMA 転送を要求する IRP を処理するときに、次のような一般的なサポートルーチンを呼び出します。

-   [**Keflushiobuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers)システム DMA コントローラーの割り当てを試みる直前 (詳細については、「[キャッシュの一貫性の維持](maintaining-cache-coherency.md)」を参照してください)

-   ドライバーが DMA 用にデバイスをプログラミングする準備ができていて、システム DMA コントローラーが必要な場合の[**Allocateadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)

    さらに、 **Allocateadapterchannel**は、ドライバーの[*adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンを呼び出します。

-   [**Mmgetmdlvirtualaddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)は、 **maptransfer**への最初の呼び出しでパラメーターとして必要な、MDL へのインデックスを取得します。

-   転送操作のためにシステム DMA コントローラーをプログラムするための[**Maptransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)

    ドライバーは、[転送要求の分割](splitting-dma-transfer-requests.md)に関する説明に従って、要求されたすべてのデータを転送するために**maptransfer**を複数回呼び出す必要がある場合があります。

-   1つの下位デバイスとの間で各 DMA 転送操作を行った直後の[**Flushadapterbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)

    ドライバーが**Maptransfer**を複数回呼び出して、要求されたすべてのデータを転送する必要がある場合は、 **maptransfer**を呼び出す回数だけ**flushadapterbuffers**を呼び出す必要があります。

-   すべての要求されたデータが転送された直後、またはデバイス i/o エラーが原因でドライバーが IRP に失敗した場合に、 [**Freeadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)

[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)によって返されるアダプターオブジェクトのポインターは、これらの各ルーチンに必須のパラメーターです。 **Keflushiobuffers**と**Mmgetmdlvirtualaddress**を除きます。これは、 **&gt;Irp に渡された MDL へのポインターを必要とします。MdlAddress**。

個々のドライバーは、各ドライバーがどのように実装されているかに応じて、さまざまな時点でこの一連のサポートルーチンを呼び出します。 たとえば、1つのドライバーの[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンが**Allocateadapterchannel**を呼び出す可能性があります。別のドライバーは、ドライバーによって作成されたインタロックされたキューから irp を削除するルーチンからこの呼び出しを行う可能性がありますが、別のドライバーがこれを行う可能性があります。データ転送の準備ができていることを下位 DMA デバイスが示している場合は、を呼び出します。

 

 




