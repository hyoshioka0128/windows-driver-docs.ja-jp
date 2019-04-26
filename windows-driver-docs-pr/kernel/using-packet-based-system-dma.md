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
ms.openlocfilehash: 758bac46c48c4dc24bbe81646acafe9d55c682fc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354194"
---
# <a name="using-packet-based-system-dma"></a>パケットベース システム DMA の使用





パケットに基づく DMA を使用する下位のデバイスのドライバーは IRP DMA 転送の要求を処理するときにサポート ルーチンの次の一般的なシーケンスを呼び出します。

-   [**KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041)システム DMA コント ローラーを割り当てようとしての直前に (詳細については、次を参照してください[キャッシュの一貫性を維持](maintaining-cache-coherency.md))。

-   [**AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)ドライバーが DMA のデバイスをプログラミングする準備が整うし、システム DMA コント ローラーが必要

    **AllocateAdapterChannel**、ドライバーを呼び出して[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)ルーチン。

-   [**MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539)最初の呼び出しでパラメーターとして必要な MDL にインデックスを取得する**MapTransfer**

-   [**MapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff554402)転送操作のシステムの DMA コント ローラーのプログラミング

    ドライバーを呼び出す必要があります**MapTransfer**で説明したように、すべての要求されたデータを転送する 2 回以上[転送要求の分割](splitting-dma-transfer-requests.md)します。

-   [**FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)各 DMA の直後後の転送との下位のデバイスからの操作

    ドライバーを呼び出す必要がある場合**MapTransfer**より後に、要求されたすべてのデータを転送するには、呼び出す必要があります**FlushAdapterBuffers**回数が呼び出されます**MapTransfer**します。

-   [**FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff546507)デバイス I/O エラーのため IRP がドライバーに失敗した場合または要求されたすべてのデータが転送されたようになります

によって返されるアダプター オブジェクト ポインター [ **IoGetDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff549220)を除くこれらのルーチンのそれぞれに必要なパラメーターは、 **KeFlushIoBuffers**と**MmGetMdlVirtualAddress**に渡される MDL へのポインターが必要な**Irp -&gt;MdlAddress**します。

個々 のドライバーでは、そのデバイスのサービスを提供する各ドライバーの実装方法に応じて、さまざまな時点でこのサポート ルーチンのシーケンスを呼び出します。 たとえば、1 つのドライバーの[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチンへの呼び出しを行うことがあります**AllocateAdapterChannel**、別のドライバーは Irp からを削除するルーチンから呼び出しを行うことがありますキュー、ドライバーが作成したインター ロックし、その下位の DMA デバイスでは、データを転送する準備が示されている場合、さらに別のドライバーはこの呼び出しを行うことがあります。

 

 




