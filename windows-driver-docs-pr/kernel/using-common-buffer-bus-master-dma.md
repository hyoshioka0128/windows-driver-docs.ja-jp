---
title: 共通バッファー バス マスター DMA の使用
description: 共通バッファー バス マスター DMA の使用
ms.assetid: 55b5d819-e257-4863-b02a-5eeb83f72c65
keywords:
- 連続 DMA WDK カーネル
- 共通バッファー DMA WDK カーネル
- DMA 転送 WDK カーネル、共通バッファー
- バスマスタ DMA WDK カーネル
- DMA 転送 WDK カーネル、バスマスタ DMA
- アダプタオブジェクト WDK カーネル、バスマスタ DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c6948218e9cfc32d57d2c34543b8ee2a2abe5cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836017"
---
# <a name="using-common-buffer-bus-master-dma"></a>共通バッファー バス マスター DMA の使用





「 [Bus マスタ dma の使用](using-bus-master-dma.md)」で説明されているように、バスマスタ dma デバイスの一部のドライバーでは、共通バッファー dma のみを使用し、一部のドライバーはパケットベースの dma と組み合わせて使用します。

一般的なバッファー DMA を経済的に使用します。 共通バッファーを設定すると、バスマスターアダプターを表すアダプターオブジェクトに関連付けられているマップレジスタの一部 (またはすべてが、要求されたバッファーのサイズによっては) を結び付けることができます。

**ページ\_サイズ**のチャンクや1つの割り当てなどを使用して、一般的なバッファー領域を経済的に設定すると、パケットベースの DMA 操作に使用できるマップレジスタが増えます。 また、他の目的のためにより多くのシステムメモリが残されるため、ドライバーとシステムの全体的なパフォーマンスが向上します。

バスマスタ DMA 用の共通バッファーを設定するには、バスマスタ DMA デバイスドライバーが、 [**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)から返されたアダプターオブジェクトポインターを使用して[**Allocatecommonbuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_common_buffer)を呼び出す必要があります。 通常、ドライバーは、\_デバイスの要求を[**開始\_\_、IRP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)の[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンからこの呼び出しを行います。 ドライバーは、ドライバーが読み込まれた状態のまま、DMA 操作にバッファーを繰り返し使用する場合にのみ、共通バッファーを割り当てる必要があります。 次の図は、 **Allocatecommonbuffer**の呼び出しを示しています。

![バスマスタ dma 用の共通バッファーの割り当てを示す図](images/3halcbff.png)

前の図では、バッファーに対して要求されたサイズ (Length Forbuffer) によって、共通バッファーの仮想-論理マッピングを提供するために使用する必要があるマップレジスタの数が決定されます。 [**Bytes\_to\_pages**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)マクロを使用して、必要なページの最大数を決定します (\_ページ (*length forbuffer*)**に\_バイト**)。 この値は、 [**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)によって返される*numberofmapregisters*より大きくすることはできません。

さらに、呼び出し元は次のものを提供する必要があります。

-   キャッシュを有効にする必要があるかどうかを示すブール値です。

    **メモ**   この値は無視されます。 オペレーティングシステムは、割り当てられる共通バッファーでキャッシュされたメモリを有効にするかどうかを決定します。 この決定は、プロセッサアーキテクチャとデバイスバスに基づいています。 

    X86 ベース、x64 ベース、および Itanium ベースのプロセッサを搭載したコンピューターでは、キャッシュされたメモリが有効になります。 

    ARM または ARM 64 ベースのプロセッサを搭載しているコンピューターでは、オペレーティングシステムはすべてのデバイスに対してキャッシュされたメモリを自動的に有効にしません。 システムは、デバイスがキャッシュに整合性があるかどうかを判断するために、各デバイスの ACPI_CCA メソッドに依存しています。 

-   **Allocatecommonbuffer**からの復帰時に、デバイスからアクセス可能なバッファーのベース*論理アドレス*(前の図では bufferlogicaladdress) を格納するドライバー定義変数へのポインター

呼び出しが成功した場合、 **Allocatecommonbuffer**は、ドライバーからアクセスできるベースの仮想アドレス (前の図の buffervirtualaddress) を返します。ドライバーは、デバイス拡張機能、コントローラー拡張機能、またはその他のドライブに保存する必要があります。ドライバーがアクセス可能な常駐ストレージ領域 (ドライバーによって割り当てられた非ページプール)。

**Allocatecommonbuffer**は、バッファーにメモリを割り当てられない場合に**NULL**を返します。 返された基本仮想アドレスが**NULL**の場合、ドライバーはシステムのパケットベースの DMA サポートのみを使用する必要があります。または、ドライバーが IRP\_を失敗させて **\_デバイス**の要求を開始し、状態を返す必要があり\_\_\_リソースが不足しています。

それ以外の場合、ドライバーは、割り当てられた共通バッファーを、DMA 転送用のドライバーおよびアダプターがアクセス可能なストレージ領域として使用できます。

PnP マネージャーが、デバイスを停止または削除する IRP を送信する場合、ドライバーは[**Freecommonbuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_common_buffer)を呼び出して、割り当てられている各共通バッファーを解放する必要があります。

 

 




