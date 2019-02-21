---
title: パケットに基づくバス マスター DMA を使用してください。
description: パケットに基づくバス マスター DMA を使用してください。
ms.assetid: 57b37103-8ae0-4c54-b613-55b1a629d9ae
keywords:
- バス マスター DMA WDK カーネル
- DMA は、WDK カーネル、バス マスター DMA を転送します。
- アダプター オブジェクトの WDK カーネル、バス マスター DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d20d035bc5982c60f3abdc9b9bc5f900efdedb0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538986"
---
# <a name="using-packet-based-bus-master-dma"></a>パケットに基づくバス マスター DMA を使用してください。





パケットに基づく DMA を使用するには、バス マスター DMA のデバイスのドライバーは IRP DMA 転送の要求を処理するときにサポート ルーチンの次の一般的なシーケンスを呼び出します。

-   [**KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041)転送要求をマップ レジスタを割り当て前だけですに、(詳細については、次を参照してください[キャッシュの一貫性を維持](maintaining-cache-coherency.md))。

-   [**AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)ときに、ドライバーは DMA のバス マスター アダプターをプログラムする準備が

-   [**MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539)への最初のパラメーターとして必要な MDL にインデックスを取得する[ **MapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff554402)、および**MapTransfer**にデバイスからアクセス可能な IRP のバッファーをサポートするシステムの物理メモリを作成します。

    すべてのドライバーで説明したように、現在の IRP を満たすためには、複数の転送操作を実行する必要がありますので注意[転送要求の分割](splitting-dma-transfer-requests.md)します。 機能を呼び出すことがないデバイスのドライバー スキャッター/ギャザー **MapTransfer** 1 回あたりの操作を転送します。 機能を呼び出すことができるデバイスのドライバー スキャッター/ギャザー **MapTransfer**各転送操作を設定する 2 回以上。 また、これらのドライバーを使用で説明されている、システムの組み込みのスキャッター/ギャザー サポート[を使用してスキャッター/ギャザー DMA](using-scatter-gather-dma.md)します。

-   [**FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)各 DMA 転送操作と要求されたすべてのデータが完全に転送されるかどうかを判断するために、ターゲット デバイスからの最後に

-   [**FreeMapRegisters** ](https://msdn.microsoft.com/library/windows/hardware/ff546513)ドライバーは IRP がデバイスのために失敗する必要がありますまたはバスの I/O エラーのため、または要求されたすべてのデータが完全に転送されるため、現在 IRP のすべての DMA 操作を実行するようになります

によって返されるアダプター オブジェクト ポインター [ **IoGetDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff549220)に必要なパラメーターは、 **AllocateAdapterChannel**、 **MapTransfer**、 **FlushAdapterBuffers**、および**FreeMapRegisters**します。 Windows 2000 より前の Windows NT のバージョンでは、バス マスター デバイスでした渡すことに注意してください、 **NULL**アダプター オブジェクト ポインター **MapTransfer**と**FlushAdapterBuffers**します。 Windows 2000 以降では、ドライバー不要になった実行できます。

**KeFlushIoBuffers**と**MmGetMdlVirtualAddress**で MDL へのポインターを必要と**Irp -&gt;MdlAddress**します。

個々 のドライバーでは、そのデバイスのサービスを提供する各ドライバーの実装方法に応じて、さまざまな時点でこのサポート ルーチンのシーケンスを呼び出します。 たとえば、1 つのドライバーの[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチンへの呼び出しを行うことがあります**AllocateAdapterChannel**、別のドライバーを削除するルーチンからのこの呼び出しを行う可能性がありますインタロックされたキューのドライバーが作成またはデバイスのキューから Irp します。

使用する代わりには、ルーチンは、任意のドライバーを使用してパケットに基づく DMA サポート ルーチンが効率化するためのものを使用できますスキャッター/ギャザー DMA では、そのデバイスがスキャッター/ギャザーの組み込みサポートを持つかどうかに関係なくをこのセクションで説明します。 参照してください[を使用してスキャッター/ギャザー DMA](using-scatter-gather-dma.md)詳細についてはします。

 

 




