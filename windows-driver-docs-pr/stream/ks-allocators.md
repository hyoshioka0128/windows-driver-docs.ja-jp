---
title: KS のアロケーター
description: KS のアロケーター
ms.assetid: 07812703-a66f-450a-b28e-4cf765267c4a
keywords:
- カーネルの WDK、アロケーターのストリーミング
- KS WDK、アロケーター
- ストリーミング アロケーター WDK カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 323d0433528d7d9f93e728adbe7f14b999b5b535
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382535"
---
# <a name="ks-allocators"></a>KS のアロケーター





*アロケーター*データ バッファーをインスタンス化する KS オブジェクトと呼びます*フレーム*の I/O 要求。 フレームのサイズはを通じて仕入先が指定した継続的なメモリのチャンクは、 **AllocatorFraming**のメンバー [ **KSPIN\_記述子\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex).

ミニドライバーをサポートできますアロケーターは、複数のバッファーの種類のビデオ カードの RAM を内蔵型のインスタンス。 ただし、ほとんどのミニドライバーを使用して、*既定のアロケーター*システム メモリを割り当てることです。 ミニドライバーは、フレーム サイズ、フレーム、および配置の要件の最大数を指定できます。 既定のアロケーターは、要件を満たしてに任せし、破棄されたフレームを再利用してパフォーマンスを最適化することがあります。

呼び出して、ミニドライバーがアロケーターを作成、 [ **KsCreateAllocator** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreateallocator)ルーチンまたは関連する関数。 この呼び出しで、ミニドライバーはへのポインターを渡す、 [ **KSALLOCATOR\_フレーム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksallocator_framing)構造体。 この構造体には、要求されたアロケーターを記述するパラメーターが含まれています。

ストリーム クラスのモデルでは、アロケーターを作成するミニドライバー サポート、 [ **KSPROPERTY\_接続\_ALLOCATORFRAMING** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-allocatorframing)プロパティ。 これは読み取り専用の要求で、関連するポインターを返します[ **KSALLOCATOR\_フレーム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksallocator_framing)構造体の指定したシンクのハンドル。

アロケーターを提供するミニドライバーをサポートする必要がありますも、 [ **KSPROPERTY\_ストリーム\_アロケーター** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-allocator)プロパティ。 このプロパティは、ストリームの接続ポイントに現在割り当てられているアロケーターのハンドルへの読み取り/書き込みアクセスを提供します。

AVStream で実行されているミニドライバーは、独自のアロケーターを実装するピンを含めることができます。 これには、設定、 [ **KSALLOCATOR\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksallocator_dispatch)のメンバー、 [ **KSPIN\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_dispatch)構造体. 指定**NULL**このピンのアロケーターを指定しない場合は、このメンバーにします。

AVStream ミニドライバーをさらに、使用、 [ **KSALLOCATOR\_フレーム\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksallocator_framing_ex)アロケーターの要件を指定する構造体。 クライアントを使用して、 [ **KSPROPERTY\_接続\_ALLOCATORFRAMING\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-allocatorframing-ex) pin のフレームの要件を取得するプロパティ。 参照してください[AVStream アロケーター](avstream-allocators.md)詳細についてはします。

このセクションには、次の追加情報が含まれています。

[既定のアロケーター](default-allocators.md)

[特定のアロケーターをフィルター処理します。](filter-specific-allocators.md)

[割り当てのパターン](allocation-schemes.md)

 

 




