---
title: AVStream のアロケーター
description: AVStream のアロケーター
ms.assetid: cda90faa-d4e3-4f17-aa5a-87dcde314bfd
keywords:
- AVStream allocators WDK
- アロケーター WDK AVStream
- WDK AVStream フレーム
- データ バッファーの WDK AVStream
- WDK AVStream のバッファー
- WDK AVStream のフレームの割り当てください。
- WDK AVStream のフレームの解放
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4396c1322d131155e5494e02111db6af8b8d631
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386707"
---
# <a name="avstream-allocators"></a>AVStream のアロケーター





AVStream クラス ドライバーを使用して、*アロケーター*という単位でのデータ バッファーを割り当てる*フレーム*します。 フレームのサイズはを通じて仕入先が指定した継続的なメモリのチャンクは、 **AllocatorFraming**のメンバー [ **KSPIN\_記述子\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex).

ミニドライバー アクセスからこれらのバッファー、 [Stream ポインター](stream-pointers.md) API; 呼び出し[ **KsPinGetLeadingEdgeStreamPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspingetleadingedgestreampointer)をストリームにポインターを取得します。

AVStream クライアントは読み取り専用プロパティを使用して、pin のフレームの要件に関する情報を取得することができます[ **KSPROPERTY\_接続\_ALLOCATORFRAMING\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-allocatorframing-ex). このプロパティは、型の構造体を返す[ **KSALLOCATOR\_フレーム\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksallocator_framing_ex)暗証番号 (pin) のフレームの要件を記述します。

データが使用されて不要になったときに AVStream はアロケーターを使用して、バッファーを解放します。

AVStream では、既定のアロケーターを提供します。 既定のアロケーターで、ミニドライバーを提供するアロケーターの要件に基づいてプールのメモリを割り当てて、 **AllocatorFraming**のメンバー、 [ **KSPIN\_記述子\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)構造体。

デバイスに固有の配賦の要件と仕入先には、独自割り当てルーチンを含むミニドライバーを作成できます。 場合は、ドライバーからメモリを割り当てるアロケーターを指定できますなど、[共通 DMA バッファー](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-common-buffer-system-dma)します。

アロケーターを提供するには、指定、 [ **KSALLOCATOR\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksallocator_dispatch)次のベンダーから提供されたコールバック ルーチンへのポインターを含む構造体。

-   [*AVStrMiniInitializeAllocator*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspininitializeallocator)

-   [*AVStrMiniDeleteAllocator*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksdeleteallocator)

-   [*AVStrMiniAllocate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksdefaultallocate)

-   [*AVStrMiniAllocatorFreeFrame*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksdefaultfree)

このアロケーター ディスパッチ構造へのポインターを提供、**アロケーター**のメンバー、 [ **KSPIN\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_dispatch)を暗証番号 (pin) を記述する構造体このアロケーターは、フレームをインスタンス化されます。

この pin ディスパッチ構造へのポインターを指定、**ディスパッチ**の対応するメンバー [ **KSPIN\_記述子\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)構造体。 AVStream でディスパッチ構造に関する詳細については、「 [AVStream ディスパッチ テーブル](avstream-dispatch-tables.md)します。

実行時に、グラフのマネージャー (たとえば、[カーネル ストリーミング プロキシ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index)モジュール) アロケーターの選択範囲を処理します。 ベンダーから提供されたアロケーター*いない*グラフ マネージャーによって選択されることが保証します。

接続がカーネル モードの場合にのみ、カーネル モードのアロケーターが選択されます。 さらに、アロケーターの要件とアロケーターの機能に不一致がある場合は、アロケーターを拒否でした。 アロケーターが選択されていない場合、 [ *AVStrMiniInitializeAllocator* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspininitializeallocator)コールバック ルーチンは呼び出されません。

参照してください[AVStream DMA サービス](avstream-dma-services.md)と[Stream ポインター](stream-pointers.md)します。

 

 




