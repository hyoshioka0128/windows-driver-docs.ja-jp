---
title: アダプター オブジェクトの取得
description: アダプター オブジェクトの取得
ms.assetid: 2af4ac28-b3c0-4e46-afb1-9c6897c67f03
keywords:
- アダプター オブジェクトの WDK カーネルを取得します。
- DEVICE_DESCRIPTION
- DMA_OPERATIONS
- DMA は、WDK カーネルでは、アダプタ オブジェクトを転送します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 519b184bf177a79ba04d9c6f0f1f8a200c94f176
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386031"
---
# <a name="getting-an-adapter-object"></a>アダプター オブジェクトの取得





システムまたはバス マスター DMA を使用してドライバーを呼び出し、デバイスの起動時に[ **IoGetDmaAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)アダプター オブジェクトへのポインターを取得し、各で使用できるマップ レジスタの最大数を決定するには転送操作。 ドライバーを呼び出すと**IoGetDmaAdapter**、I/O マネージャーで、さらに、必要なプラットフォームに固有の情報を取得する HAL を呼び出します。

ドライバーはシステム定義で特定の情報を指定する必要があります[**デバイス\_説明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_description)呼び出しで構造**IoGetDmaAdapter**します。 ドライバーを使用する必要があります[ **RtlZeroMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlzeromemory)初期化するために、**デバイス\_説明**に値を設定する前にゼロを含む構造体。

必要なデータには、デバイスがスキャッター/ギャザーの機能がある場合に、バス マスターをどのようにがかどうかや、デバイスを同時に転送できるデータのバイト数などのドライバーのデバイスの機能に関する情報が含まれています (**MaximumLength**).

必要なデバイスの説明のデータには、バス マスター デバイスのドライバーを制御するバスのプラットフォームに固有とシステムによって割り当てられた番号などのプラットフォームに固有の情報も含まれています。 ドライバーは、呼び出すことでこの情報を取得できます[ **IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)します。

**デバイス\_説明**構造に関連するいくつかの DMA デバイスまたはドライバーがない可能性がありますをいくつかのフィールドが含まれています。 たとえば、 **BusNumber** WDM ドライバーではフィールドは使用されません。 各ドライバーでは、関連する構造体のメンバーの値を指定する必要があります、値をその他のすべてのメンバーをゼロに設定する必要があります。

下位のデバイスのドライバーを渡さないでください**TRUE**で、 **ScatterGather**デバイスが待機中の場合、要求を分割する必要がありますを行ったりするシステム DMA コント ローラーのできる限りフィールド2 つ以上の DMA 操作。

**IoGetDmaAdapter**両方のポインターを返します、アダプター オブジェクトを特定のプラットフォームまたはデバイスに固有の値がマップの数を示すレジスタが各 DMA 転送操作のアダプタ オブジェクトを使用します。

返されるアダプター オブジェクトには、ドライバーにアクセスできる 3 つのフィールドが含まれています。

-   バージョン番号 (**バージョン**)

-   サイズ (**サイズ**)

-   ポインターを[ **DMA\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_dma_operations)構造 (**DmaOperations**)

**DMA\_操作**構造体は、そのデバイス上の DMA 操作を実行するドライバーを使用する必要があります関数へのポインターのテーブルを構成します。 関数は、このデータ構造体でポインターを介してのみアクセスできます。ドライバーは、名前で直接それらを呼び出すことはできません。 (これらのルーチンを置き換えるので注意**Hal * Xxx*** ルーチンの以前のバージョンの Windows NT ではサポートされています。 従来のドライバーの互換性を確保するには、Wdm.h と Ntddk.h ヘッダー ファイル、古い形式の名前を持つマクロが、新しいドライバーは、データ構造を使用して、関数を呼び出す必要があります常にします。)

マップのレジスタの数は、デバイスからデバイスとプラットフォームに異なります。 一般に、HAL には、次の基準に従ってマップ レジスタの数値が割り当てられます。

-   HAL、可能な値を返す場合は、マップのレジスタの数より 1 つ以上に必要な転送**MaximumLength** (バイト単位)、ドライバーの呼び出しで指定されている**IoGetDmaAdapter**します。

-   それ以外の場合、HAL は、特定のプラットフォームの可能な限り大きくはより低い値を返します。

つまり、HAL 通常各ドライバー、そのデバイスに対して DMA のスループットを最大化するための十分なマップのレジスタには、HAL は、一部の Windows プラットフォームで小さい方の値を返すことができます。 ドライバーは、要求のマップのレジスタの数を取得するためのドライバーが返される値を常に確認する必要があります保証はありません。

DMA デバイス ドライバーは、オブジェクトのポインターをアダプターにストレージを提供する必要がありますと*NumberOfMapRegisters*によって返される値**IoGetDmaAdapter**します。 このポインターは、DMA を使用するシステム提供のサポート ルーチンに必要なパラメーターです。 IRQL でルーチンを呼び出す必要があるため、これらの多くをサポートしてディスパッチ =\_レベル、ドライバーによって割り当てられたストレージは、常駐である必要があります。 DMA のほとんどのドライバーで必要な記憶域の提供、[デバイス拡張機能](device-extensions.md)します。 ただし、記憶域にできるコント ローラーの拡張機能ドライバーにも使用している場合、[コント ローラー オブジェクト](using-controller-objects.md)またはドライバーが割り当てられる非ページ プール。 参照してください[システム容量のメモリを割り当てる](allocating-system-space-memory.md)と[を管理するハードウェアの優先順位](managing-hardware-priorities.md)詳細についてはします。

ドライバーには、すべての DMA 操作が完了したら、それを呼び出す[ **PutDmaAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pput_dma_adapter)アダプター オブジェクトを解放します。

次のセクションでは、([を使用してシステム DMA](using-system-dma.md)と[バス マスター DMA を使用して](using-bus-master-dma.md)) 転送要求を満たすために、デバイスの使用サポート DMA ルーチンのドライバーがモノリシック方法について説明します。 これらのセクションでは、ドライバーは、次のことを前提としています。

-   標準的な[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチンではなくを設定して Irp の内部キューを管理します。

-   転送要求の数が不足してマップに登録を分割する内部のルーチンは使用できます。

-   DMA 制約のないデバイスに固有

つまり、これらのセクションでは、ドライバーの DMA 操作では、最も簡単な方法を説明しますが、個々 のドライバーが正確に同じ手法を必ずしも使用しないでください。 DMA デバイスのドライバーが任意の場合、ドライバー モデルに依存ルーチンが大きなを分割する必要がありますドライバー DMA 転送要求 (クラス/ポート モノリシックな)、そのドライバーを処理する必要があります、デバイスの機能と、デバイスに固有の DMA 制約。

 

 




