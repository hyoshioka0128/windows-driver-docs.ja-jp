---
title: アダプター オブジェクトの取得
description: アダプター オブジェクトの取得
ms.assetid: 2af4ac28-b3c0-4e46-afb1-9c6897c67f03
keywords:
- アダプタオブジェクト WDK カーネル、取得
- DEVICE_DESCRIPTION
- DMA_OPERATIONS
- DMA 転送 WDK カーネル、アダプターオブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a36e21c949db10747b57c1fd522c3e4cd48a714
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838685"
---
# <a name="getting-an-adapter-object"></a>アダプター オブジェクトの取得





デバイスの起動時に、システムまたはバスマスタ DMA を使用するドライバーは[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)を呼び出して、アダプターオブジェクトへのポインターを取得し、各転送操作で使用可能なマップレジスタの最大数を決定します。 ドライバーが**IoGetDmaAdapter**を呼び出すと、i/o マネージャーは HAL を呼び出して、必要なプラットフォーム固有の情報を取得します。

ドライバーは、 **IoGetDmaAdapter**の呼び出しで、システム定義の[**デバイス\_記述**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_description)構造体に特定の情報を提供する必要があります。 ドライバーは、値を設定する前に、 [**Rtlゼロメモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory)を使用して、**デバイス\_記述**構造体をゼロで初期化する必要があります。

必要なデータには、デバイスがバスマスターであるかどうか、スキャッター/ギャザー機能があるかどうか、デバイスが一度に転送できるデータのバイト数 (**Maximumlength**) など、ドライバーのデバイスの機能に関する情報が含まれます。

必要なデバイスの説明データには、バスマスターデバイスのドライバーが制御するバスのプラットフォーム固有の番号やシステムによって割り当てられた番号など、プラットフォーム固有の情報も含まれます。 ドライバーは、 [**Iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)を呼び出すことによってこの情報を取得できます。

**デバイス\_説明**の構造には、一部の DMA デバイスまたはドライバーに関係のないフィールドが含まれています。 たとえば、 **Busnumber**フィールドは WDM ドライバーでは使用されません。 各ドライバーは、関連する構造体メンバーの値を指定する必要があり、その他のすべてのメンバーの値を0に設定する必要があります。

要求を複数の DMA 操作に分割する必要がある場合に、デバイスがシステム DMA コントローラーの再プログラミングを待機できるようにしない限り、下位デバイスのドライバーは、 **ScatterGather**フィールドに**TRUE**を渡しません。

**IoGetDmaAdapter**は、アダプターオブジェクトへのポインターと、各 DMA 転送操作のアダプターオブジェクトで使用できるマップレジスタの数を示す、プラットフォーム固有またはデバイス固有の値の両方を返します。

返されたアダプターオブジェクトには、ドライバーからアクセス可能な3つのフィールドが含まれています。

-   バージョン番号 (**バージョン**)

-   サイズ (**サイズ**)

-   [**DMA\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_operations)構造体へのポインター (**DmaOperations**)

**Dma\_操作**の構造は、ドライバーがデバイスで dma 操作を実行するために使用する必要がある関数へのポインターのテーブルで構成されます。 関数は、このデータ構造体のポインターを通じてのみアクセスできます。ドライバーは、名前を指定して直接呼び出すことはできません。 (これらのルーチンは、以前のバージョンの Windows NT でサポートされている**Hal * Xxx*** ルーチンに代わるものであることに注意してください。 レガシドライバーの互換性を確保するために、Wdm および Ntddk ヘッダーファイルは古い名前のマクロを提供しますが、新しいドライバーは常にデータ構造を通じて関数を呼び出す必要があります)。

マップレジスタの数は、デバイスやプラットフォームによって異なります。 一般に、次の条件に従って、さまざまなマップレジスタが割り当てられます。

-   可能であれば、HAL は、ドライバーの**IoGetDmaAdapter**への呼び出しで指定されているように、 **maximumlength**バイトを転送するために必要なマップレジスタの数より1つ多い値を返します。

-   それ以外の場合、HAL は、特定のプラットフォームで可能な限り小さい値を返します。

つまり、通常、各ドライバーはデバイスの DMA スループットを最大化するために十分なマップレジスタを提供しますが、一部の Windows プラットフォームでは、より小さい値を返すことができます。 ドライバーが要求したマップレジスタの数を取得する保証はないため、ドライバーは常に返された値を確認する必要があります。

任意の DMA デバイスドライバーは、 **IoGetDmaAdapter**によって返されるアダプターオブジェクトポインターと*numberofmapregisters*値のための記憶域を提供する必要があります。 このポインターは、DMA に使用されるシステム指定のサポートルーチンの必須パラメーターです。 これらのサポートルーチンの多くは、IRQL = ディスパッチ\_レベルで呼び出す必要があるため、ドライバーによって割り当てられたストレージが常駐している必要があります。 ほとんどの DMA ドライバーは、[デバイス拡張機能](device-extensions.md)に必要な記憶域を提供します。 ただし、ドライバーが[コントローラーオブジェクト](using-controller-objects.md)を使用している場合、またはドライバーによって割り当てられた非ページプールで、記憶域がコントローラー拡張機能に含まれる場合もあります。 詳細については、「[システム領域メモリの割り当て](allocating-system-space-memory.md)」および「[ハードウェアの優先順位の管理](managing-hardware-priorities.md)」を参照してください。

ドライバーがすべての DMA 操作を完了すると、 [**PutDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_dma_adapter)を呼び出して、アダプターオブジェクトを解放します。

次のセクション ([システム dma](using-system-dma.md)を使用し、[バスマスター dma を使用](using-bus-master-dma.md)) では、DMA デバイスのモノリシックドライバーがサポートルーチンを使用して転送要求を満たす方法について説明します。 これらのセクションでは、ドライバーが次のものであることを前提としています。

-   Irp の内部キューを設定および管理するのではなく、標準の[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチン

-   マップレジスタの数が不足している転送要求を分割する内部ルーチン

-   デバイス固有の DMA 制約はありません

つまり、これらのセクションでは、ドライバーの DMA 操作に関して考えられる最も簡単な方法について説明しますが、個々のドライバーがまったく同じ手法を使用するとは限りません。 DMA デバイスのドライバーについては、大容量 DMA 転送要求を分割する必要があるドライバールーチンは、ドライバーモデル (クラス/ポートまたはモノリシック)、デバイスの機能、およびドライバーが処理する必要のあるデバイス固有の DMA 制約によって異なります。

 

 




