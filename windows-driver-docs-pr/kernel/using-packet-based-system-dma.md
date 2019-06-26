---
title: パケットベース システム DMA の使用
description: パケットベース システム DMA の使用
ms.assetid: 5d175193-4a28-49fd-80b5-18f116232c6e
keywords:
- DMA WDK カーネルでは、パケットに基づくシステム
- DMA WDK カーネルのパケットに基づく
- DMA は、パケットに基づく、WDK のカーネルを転送します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c56dc0f2a53b8ea0a3fc706e06cf91641b5ec2c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381580"
---
# <a name="using-packet-based-system-dma"></a>パケットベース システム DMA の使用





パケットに基づく DMA を使用する下位のデバイスのドライバーは IRP DMA 転送の要求を処理するときにサポート ルーチンの次の一般的なシーケンスを呼び出します。

-   [**KeFlushIoBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keflushiobuffers)システム DMA コント ローラーを割り当てようとしての直前に (詳細については、次を参照してください[キャッシュの一貫性を維持](maintaining-cache-coherency.md))。

-   [**AllocateAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel)ドライバーが DMA のデバイスをプログラミングする準備が整うし、システム DMA コント ローラーが必要

    **AllocateAdapterChannel**、ドライバーを呼び出して[ *AdapterControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control)ルーチン。

-   [**MmGetMdlVirtualAddress** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)最初の呼び出しでパラメーターとして必要な MDL にインデックスを取得する**MapTransfer**

-   [**MapTransfer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pmap_transfer)転送操作のシステムの DMA コント ローラーのプログラミング

    ドライバーを呼び出す必要があります**MapTransfer**で説明したように、すべての要求されたデータを転送する 2 回以上[転送要求の分割](splitting-dma-transfer-requests.md)します。

-   [**FlushAdapterBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pflush_adapter_buffers)各 DMA の直後後の転送との下位のデバイスからの操作

    ドライバーを呼び出す必要がある場合**MapTransfer**より後に、要求されたすべてのデータを転送するには、呼び出す必要があります**FlushAdapterBuffers**回数が呼び出されます**MapTransfer**します。

-   [**FreeAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_adapter_channel)デバイス I/O エラーのため IRP がドライバーに失敗した場合または要求されたすべてのデータが転送されたようになります

によって返されるアダプター オブジェクト ポインター [ **IoGetDmaAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)を除くこれらのルーチンのそれぞれに必要なパラメーターは、 **KeFlushIoBuffers**と**MmGetMdlVirtualAddress**に渡される MDL へのポインターが必要な**Irp -&gt;MdlAddress**します。

個々 のドライバーでは、そのデバイスのサービスを提供する各ドライバーの実装方法に応じて、さまざまな時点でこのサポート ルーチンのシーケンスを呼び出します。 たとえば、1 つのドライバーの[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチンへの呼び出しを行うことがあります**AllocateAdapterChannel**、別のドライバーは Irp からを削除するルーチンから呼び出しを行うことがありますキュー、ドライバーが作成したインター ロックし、その下位の DMA デバイスでは、データを転送する準備が示されている場合、さらに別のドライバーはこの呼び出しを行うことがあります。

 

 




