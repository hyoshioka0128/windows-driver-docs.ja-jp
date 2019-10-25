---
title: AVStream のアロケーター
description: AVStream のアロケーター
ms.assetid: cda90faa-d4e3-4f17-aa5a-87dcde314bfd
keywords:
- AVStream アロケーター WDK
- アロケーター WDK AVStream
- WDK AVStream のフレーム
- データバッファー WDK AVStream
- WDK AVStream のバッファー
- フレームの割り当て WDK AVStream
- フレームの解放 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9f7669b716be81896a880d1d07c192a1db5186c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845019"
---
# <a name="avstream-allocators"></a>AVStream のアロケーター





AVStream クラスドライバーは、*アロケーター*を使用して、*フレーム*と呼ばれる単位でデータバッファーを割り当てます。 フレームは連続したメモリのチャンクで、 [**Kspin\_DESCRIPTOR\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)の**allocatorframing**メンバーを通じてベンダーが指定したサイズです。

ミニドライバー[ストリームポインター](stream-pointers.md) API を使用してこれらのバッファーにアクセスします。[**KsPinGetLeadingEdgeStreamPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer)を呼び出して、ストリームへのポインターを取得します。

AVStream クライアントは、読み取り専用プロパティの[**Ksk プロパティ\_接続\_ALLOCATORFRAMING\_EX**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-allocatorframing-ex)を使用して、pin のフレーム要件に関する情報を取得できます。 このプロパティは、ピンのフレーム要件を記述する[**Ksallocator\_フレーミング\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex)型の構造体を返します。

データが使用されなくなった場合、AVStream はアロケーターを使用してバッファーを解放します。

AVStream では、既定のアロケーターが提供されます。 既定のアロケーターは、 [**Kspin\_DESCRIPTOR\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体の**allocatorframing**メンバーでミニドライバーが提供するアロケーター要件に基づいて、プールメモリを割り当てます。

デバイス固有の割り当て要件を持つベンダーは、独自の割り当てルーチンを含むミニドライバーを作成できます。 たとえば、ドライバーが[共通の DMA バッファー](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-common-buffer-system-dma)からメモリを割り当てる場合は、アロケーターを指定することができます。

アロケーターを提供するには、次のベンダー提供のコールバックルーチンへのポインターを含む[**Ksallocator\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksallocator_dispatch)構造体を指定します。

-   [*AVStrMiniInitializeAllocator*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspininitializeallocator)

-   [*AVStrMiniDeleteAllocator*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksdeleteallocator)

-   [*AVStrMiniAllocate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksdefaultallocate)

-   [*AVStrMiniAllocatorFreeFrame*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksdefaultfree)

このアロケーターがフレームをインスタンス化するピンを記述する[**Kspin\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)構造体の**アロケーター**メンバーで、このアロケーターディスパッチ構造体へのポインターを指定します。

対応する[**Kspin\_DESCRIPTOR\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体の**ディスパッチ**メンバーで、このピンディスパッチ構造体へのポインターを指定します。 AVStream のディスパッチ構造の詳細については、 [Avstream のディスパッチテーブル](avstream-dispatch-tables.md)に関するページを参照してください。

実行時に、graph manager ([カーネルストリーミングプロキシ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)モジュールなど) がアロケーターの選択を処理します。 ベンダーが提供したアロケーターは、graph マネージャーによって選択されるとは限り*ません*。

カーネルモードアロケーターは、接続がカーネルモードの場合にのみ選択されます。 また、アロケーターの要件とアロケーターの機能が一致しない場合は、アロケーターが拒否される可能性があります。 アロケーターが選択されていない場合、 [*Avstrminiinitializeallocator*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspininitializeallocator)のコールバックルーチンは呼び出されません。

「 [Avstream DMA サービス](avstream-dma-services.md)と[ストリームポインター](stream-pointers.md)」も参照してください。

 

 




