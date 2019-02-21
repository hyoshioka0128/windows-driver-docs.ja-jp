---
title: AVStream アロケーター
description: AVStream アロケーター
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
ms.openlocfilehash: f5b8935f81faa6f5a6669dc2f68964fa702e32f1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550476"
---
# <a name="avstream-allocators"></a>AVStream アロケーター





AVStream クラス ドライバーを使用して、*アロケーター*という単位でのデータ バッファーを割り当てる*フレーム*します。 フレームのサイズはを通じて仕入先が指定した継続的なメモリのチャンクは、 **AllocatorFraming**のメンバー [ **KSPIN\_記述子\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534).

ミニドライバー アクセスからこれらのバッファー、 [Stream ポインター](stream-pointers.md) API; 呼び出し[ **KsPinGetLeadingEdgeStreamPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff563513)をストリームにポインターを取得します。

AVStream クライアントは読み取り専用プロパティを使用して、pin のフレームの要件に関する情報を取得することができます[ **KSPROPERTY\_接続\_ALLOCATORFRAMING\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff565101). このプロパティは、型の構造体を返す[ **KSALLOCATOR\_フレーム\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff560982)暗証番号 (pin) のフレームの要件を記述します。

データが使用されて不要になったときに AVStream はアロケーターを使用して、バッファーを解放します。

AVStream では、既定のアロケーターを提供します。 既定のアロケーターで、ミニドライバーを提供するアロケーターの要件に基づいてプールのメモリを割り当てて、 **AllocatorFraming**のメンバー、 [ **KSPIN\_記述子\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)構造体。

デバイスに固有の配賦の要件と仕入先には、独自割り当てルーチンを含むミニドライバーを作成できます。 場合は、ドライバーからメモリを割り当てるアロケーターを指定できますなど、[共通 DMA バッファー](https://msdn.microsoft.com/library/windows/hardware/ff565362)します。

アロケーターを提供するには、指定、 [ **KSALLOCATOR\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff560976)次のベンダーから提供されたコールバック ルーチンへのポインターを含む構造体。

-   [*AVStrMiniInitializeAllocator*](https://msdn.microsoft.com/library/windows/hardware/ff556321)

-   [*AVStrMiniDeleteAllocator*](https://msdn.microsoft.com/library/windows/hardware/ff554273)

-   [*AVStrMiniAllocate*](https://msdn.microsoft.com/library/windows/hardware/ff554265)

-   [*AVStrMiniAllocatorFreeFrame*](https://msdn.microsoft.com/library/windows/hardware/ff554266)

このアロケーター ディスパッチ構造へのポインターを提供、**アロケーター**のメンバー、 [ **KSPIN\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff563535)を暗証番号 (pin) を記述する構造体このアロケーターは、フレームをインスタンス化されます。

この pin ディスパッチ構造へのポインターを指定、**ディスパッチ**の対応するメンバー [ **KSPIN\_記述子\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)構造体。 AVStream でディスパッチ構造に関する詳細については、「 [AVStream ディスパッチ テーブル](avstream-dispatch-tables.md)します。

実行時に、グラフのマネージャー (たとえば、[カーネル ストリーミング プロキシ](https://msdn.microsoft.com/library/windows/hardware/ff560877)モジュール) アロケーターの選択範囲を処理します。 ベンダーから提供されたアロケーター*いない*グラフ マネージャーによって選択されることが保証します。

接続がカーネル モードの場合にのみ、カーネル モードのアロケーターが選択されます。 さらに、アロケーターの要件とアロケーターの機能に不一致がある場合は、アロケーターを拒否でした。 アロケーターが選択されていない場合、 [ *AVStrMiniInitializeAllocator* ](https://msdn.microsoft.com/library/windows/hardware/ff556321)コールバック ルーチンは呼び出されません。

参照してください[AVStream DMA サービス](avstream-dma-services.md)と[Stream ポインター](stream-pointers.md)します。

 

 




