---
title: KS のアロケーター
description: KS のアロケーター
ms.assetid: 07812703-a66f-450a-b28e-4cf765267c4a
keywords:
- カーネルストリーミング WDK、アロケーター
- KS WDK、アロケーター
- アロケーター WDK カーネルストリーミング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9becd44c358cf243c086966dcd8d6b74c69674f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842627"
---
# <a name="ks-allocators"></a>KS のアロケーター





*アロケーター*は、i/o 要求の*フレーム*と呼ばれるデータバッファーをインスタンス化する KS オブジェクトです。 フレームは連続したメモリのチャンクで、 [**Kspin\_DESCRIPTOR\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)の**allocatorframing**メンバーを通じてベンダーが指定したサイズです。

ミニドライバーは、ビデオカードのオンボード RAM などの複数のバッファーの種類に対してアロケーターをサポートできます。 ただし、ほとんどのミニドライバーでは、*既定のアロケーター*を使用してシステムメモリを割り当てます。 ミニドライバーでは、フレームサイズ、最大フレーム数、およびアラインメント要件を指定できます。 既定のアロケーターは要件を満たしているため、破棄されたフレームを再利用することでパフォーマンスを最適化することができます。

ミニドライバーは、 [**KsCreateAllocator**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreateallocator)ルーチンまたは関連する関数を呼び出すことによってアロケーターを作成します。 この呼び出しでは、ミニドライバーは[**Ksallocator\_フレーミング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing)構造体へのポインターを渡します。 この構造体には、要求されたアロケーターを記述するパラメーターが含まれています。

Stream クラスモデルでは、ミニドライバーがアロケーターを作成すると、[**接続\_ALLOCATORFRAMING プロパティに ksk\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-allocatorframing)がサポートされます。 これは、指定されたシンクハンドルの関連する[**Ksallocator\_フレーミング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing)構造体へのポインターを返す読み取り専用の要求です。

アロケーターを提供するミニドライバーは、 [**Ksk プロパティ\_ストリーム\_アロケーター**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-allocator)プロパティもサポートする必要があります。 このプロパティは、ストリーム接続ポイントに現在割り当てられているアロケーターのハンドルへの読み取り/書き込みアクセスを提供します。

AVStream で実行されるミニドライバーには、独自のアロケーターを実装する pin を含めることができます。 これを行うには、 [**Ksallocator\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksallocator_dispatch)ディスパッチ構造体[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)のディスパッチメンバーを設定します。 この pin のアロケーターを指定しない場合は、このメンバーに**NULL**を指定します。

さらに、AVStream ミニドライバーは、 [**Ksallocator\_フレーミング\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex)構造体を使用してアロケーターの要件を指定します。 次にクライアントは、 [**Ksk プロパティ\_接続\_ALLOCATORFRAMING\_EX**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-allocatorframing-ex)プロパティを使用して、pin のフレーム要件を取得します。 詳細については、 [Avstream アロケーター](avstream-allocators.md)を参照してください。

ここでは、次の追加情報について説明します。

[既定のアロケーター](default-allocators.md)

[特定のアロケーターをフィルター処理する](filter-specific-allocators.md)

[割り当てスキーム](allocation-schemes.md)

 

 




