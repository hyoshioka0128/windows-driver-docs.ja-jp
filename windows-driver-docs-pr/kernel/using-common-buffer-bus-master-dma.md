---
title: 共通バッファー バス マスター DMA の使用
description: 共通バッファー バス マスター DMA の使用
ms.assetid: 55b5d819-e257-4863-b02a-5eeb83f72c65
keywords:
- 継続的な DMA WDK カーネル
- 一般的なバッファー DMA WDK カーネル
- DMA は、WDK カーネルでは、一般的なバッファーを転送します。
- バス マスター DMA WDK カーネル
- DMA は、WDK カーネル、バス マスター DMA を転送します。
- アダプター オブジェクトの WDK カーネル、バス マスター DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ca67ef7c2a228369649e3224106cb214db00bbd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382237"
---
# <a name="using-common-buffer-bus-master-dma"></a>共通バッファー バス マスター DMA の使用





」の説明に従って[バス マスター DMA を使用して](using-bus-master-dma.md)バス マスター DMA のデバイスの一部のドライバーが排他的に一般的なバッファー DMA を使用して、パケットに基づく DMA と組み合わせて共通バッファー DMA を使用して、いくつか。

経済的な共通バッファー DMA を使用します。 一般的なバッファーの設定は、バス マスター アダプタを表すアダプター オブジェクトに関連付けられたマップ レジスタの一部 (または要求するバッファーのサイズによっては、すべて) を関連付けることができます。

経済的な一般的なバッファー領域の設定などを使用して**ページ\_サイズ**のチャンク単位または 1 回の割り当て、パケットに基づく DMA 操作に使用できる複数のマップのレジスタのままです。 外に出て空きシステム メモリ、他の目的をより適切な全体的なドライバーとシステムのパフォーマンスを生成します。

バス マスター DMA の一般的なバッファーを設定するバス マスター DMA のデバイス ドライバーを呼び出す必要があります[ **AllocateCommonBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_common_buffer)によって返されるアダプター オブジェクト ポインターと[ **IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)します。 ドライバーからのこの呼び出しは、通常、その[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)の日常的な[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求。 ドライバーは、使用するバッファー繰り返し DMA 操作、ドライバーが読み込まれたまま場合にのみ共通のバッファーを割り当てる必要があります。 次の図は、このような呼び出し**AllocateCommonBuffer**します。

![バス マスター dma の一般的なバッファーの割り当てを示す図](images/3halcbff.png)

マップの数、要求された LengthForBuffer、としては、前の図に示すように、バッファーのサイズを決定しますレジスタを使用して、一般的なバッファーの仮想の論理的なマッピングを提供する必要があります。 使用して、 [**バイト\_TO\_ページ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)必要なページの最大数を決定するマクロ (**バイト\_TO\_ページ**(*LengthForBuffer*))。 この値より大きくすることはできません、 *NumberOfMapRegisters*によって返される[ **IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)します。

さらに、呼び出し元は、次に指定する必要があります。

-   キャッシュを有効する必要があるかどうかを示すブール値

    **注**この値は無視されます。 オペレーティング システムは、キャッシュされたメモリに割り当てられる一般的なバッファーを有効にするかどうかを決定します。 その判断は、プロセッサのアーキテクチャとデバイスのバスに基づいています。 

    X86 ベース、x64 ベースおよび Itanium ベースのプロセッサを搭載したコンピューターは、キャッシュされたメモリが有効にします。 

    ARM または ARM 64 ベースのプロセッサを搭載したコンピューターのオペレーティング システムに自動的に有効にしませんキャッシュ メモリのすべてのデバイス。 システムは、デバイスがキャッシュの一貫性のあるかどうかを判断するには、各デバイスの ACPI_CCA メソッドに依存します。 

-   デバイスからアクセス可能な情報を格納するドライバーの定義の変数へのポインター*論理アドレス*から返された場合、バッファー (前の図で BufferLogicalAddress) の**AllocateCommonBuffer**

呼び出しが成功すると、 **AllocateCommonBuffer**バッファー (前の図の BufferVirtualAddress)、ドライバー、デバイスの拡張機能内コント ローラーとの保存の必要がありますのドライバーにアクセス可能な基本仮想アドレスを返します拡張機能、またはその他のドライバーにアクセス可能なの常駐ストレージ領域 (ドライバーによって割り当てられた非ページ プール) の場合は。

**AllocateCommonBuffer**返します**NULL**場合は、バッファーのメモリを割り当てることができません。 返されるベースの仮想アドレス場合**NULL**、ドライバーかする必要がありますだけを使用、システムのパケットに基づく DMA サポート、ドライバーが失敗する必要があります、 **IRP\_MN\_開始\_デバイス**状態を返す要求\_不十分\_リソース。

それ以外の場合、ドライバーは、DMA 転送、ドライバー、およびアダプター アクセスできる記憶域として割り当てられている一般的なバッファーを使用できます。

PnP マネージャーでは、停止するか、デバイスを削除する IRP を送信するとき、ドライバーを呼び出す必要があります[ **FreeCommonBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_common_buffer)割り当て済みがある一般的な各バッファーを解放します。

 

 




