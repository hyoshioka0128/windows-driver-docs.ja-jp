---
title: パケットベース バス マスター DMA の使用
description: パケットベース バス マスター DMA の使用
ms.assetid: 57b37103-8ae0-4c54-b613-55b1a629d9ae
keywords:
- バスマスタ DMA WDK カーネル
- DMA 転送 WDK カーネル、バスマスタ DMA
- アダプタオブジェクト WDK カーネル、バスマスタ DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58b34c66c4dd1d7e744d56750899f95b67b24422
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835941"
---
# <a name="using-packet-based-bus-master-dma"></a>パケットベース バス マスター DMA の使用





パケットベースの DMA を使用するには、バスマスタ DMA デバイスのドライバーが、DMA 転送を要求する IRP を処理するときに、次の一般的なサポートルーチンを呼び出します。

-   [**Keflushiobuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers)は、転送要求のマップレジスタの割り当てを試行する直前に実行します (詳細については、「[キャッシュの一貫性の維持](maintaining-cache-coherency.md)」を参照してください)。

-   ドライバーが DMA 用のバスマスターアダプターをプログラミングする準備ができたときの[**Allocateadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)

-   [**Mmgetmdlvirtualaddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を使用して、MDL へのインデックスを取得します。これは、 [**maptransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)の初期パラメーターとして必要であり、IRP のバッファーデバイスにアクセス可能なシステム物理メモリを確保するために**maptransfer**によって使用されます。

    すべてのドライバーは、「[転送要求の分割](splitting-dma-transfer-requests.md)」で説明されているように、現在の IRP を満たすために複数の転送操作を実行することが必要になる場合があることに注意してください。 スキャッター/ギャザー機能がないデバイスのドライバーは、転送操作ごとに**Maptransfer**を呼び出すことができます。 スキャッター/ギャザー機能が搭載されているデバイスのドライバーは、各転送操作を設定するために**Maptransfer**を複数回呼び出すことができます。 また、これらのドライバーでは、「[スキャッター/ギャザー DMA の使用](using-scatter-gather-dma.md)」で説明されているシステムの組み込みのスキャッター/ギャザーサポートを使用できます。

-   要求されたすべてのデータが完全に転送されたかどうかを判断するために、ターゲットデバイスとの間で各 DMA 転送操作が終了したときの[**Flushadapterbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)

-   要求されたすべてのデータが完全に転送されているか、デバイスまたはバス i/o エラーのためにドライバーが IRP を失敗させる必要があるため、現在の IRP のすべての DMA 操作が完了するとすぐに[**FreeMapRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers) 。

[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)によって返されるアダプターオブジェクトポインターは、 **Allocateadapterchannel**、 **maptransfer**、 **flushadapterbuffers**、および**FreeMapRegisters**の必須パラメーターです。 Windows 2000 より前のバージョンの Windows NT では、バスマスタデバイスが、 **Maptransfer** **バッファーと Flushadapterbuffers**に**NULL**のアダプターオブジェクトポインターを渡す可能性があることに注意してください。 Windows 2000 以降では、ドライバーはこれを実行できなくなります。

**Keflushiobuffers**と**Mmgetmdlvirtualaddress**には、 **Irp (&gt;mdladdress)** へのポインターが必要です。

個々のドライバーは、各ドライバーがどのように実装されているかに応じて、さまざまな時点でこの一連のサポートルーチンを呼び出します。 たとえば、あるドライバーの[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンが**Allocateadapterchannel**を呼び出す可能性があり、別のドライバーは、ドライバーで作成されたインタロックされたキューまたはデバイスキューから irp を削除するルーチンからこの呼び出しを行う場合があります。

このセクションで説明されているルーチンを使用する代わりに、パケットベースの DMA を使用するドライバーでは、デバイスにスキャッター/ギャザーサポートが組み込まれているかどうかに関係なく、スキャッター/ギャザー DMA を効率化するためのサポートルーチンを使用できます。 詳細については、「[スキャッター/GATHER DMA の使用](using-scatter-gather-dma.md)」を参照してください。

 

 




