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
ms.openlocfilehash: aa0de06382e2095502390e76e7eff11bb2e5dae4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573415"
---
# <a name="ks-allocators"></a>KS のアロケーター





*アロケーター*データ バッファーをインスタンス化する KS オブジェクトと呼びます*フレーム*の I/O 要求。 フレームのサイズはを通じて仕入先が指定した継続的なメモリのチャンクは、 **AllocatorFraming**のメンバー [ **KSPIN\_記述子\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534).

ミニドライバーをサポートできますアロケーターは、複数のバッファーの種類のビデオ カードの RAM を内蔵型のインスタンス。 ただし、ほとんどのミニドライバーを使用して、*既定のアロケーター*システム メモリを割り当てることです。 ミニドライバーは、フレーム サイズ、フレーム、および配置の要件の最大数を指定できます。 既定のアロケーターは、要件を満たしてに任せし、破棄されたフレームを再利用してパフォーマンスを最適化することがあります。

呼び出して、ミニドライバーがアロケーターを作成、 [ **KsCreateAllocator** ](https://msdn.microsoft.com/library/windows/hardware/ff561633)ルーチンまたは関連する関数。 この呼び出しで、ミニドライバーはへのポインターを渡す、 [ **KSALLOCATOR\_フレーム**](https://msdn.microsoft.com/library/windows/hardware/ff560979)構造体。 この構造体には、要求されたアロケーターを記述するパラメーターが含まれています。

ストリーム クラスのモデルでは、アロケーターを作成するミニドライバー サポート、 [ **KSPROPERTY\_接続\_ALLOCATORFRAMING** ](https://msdn.microsoft.com/library/windows/hardware/ff565099)プロパティ。 これは読み取り専用の要求で、関連するポインターを返します[ **KSALLOCATOR\_フレーム**](https://msdn.microsoft.com/library/windows/hardware/ff560979)構造体の指定したシンクのハンドル。

アロケーターを提供するミニドライバーをサポートする必要がありますも、 [ **KSPROPERTY\_ストリーム\_アロケーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565684)プロパティ。 このプロパティは、ストリームの接続ポイントに現在割り当てられているアロケーターのハンドルへの読み取り/書き込みアクセスを提供します。

AVStream で実行されているミニドライバーは、独自のアロケーターを実装するピンを含めることができます。 これには、設定、 [ **KSALLOCATOR\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff560976)のメンバー、 [ **KSPIN\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff563535)構造体. 指定**NULL**このピンのアロケーターを指定しない場合は、このメンバーにします。

AVStream ミニドライバーをさらに、使用、 [ **KSALLOCATOR\_フレーム\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff560982)アロケーターの要件を指定する構造体。 クライアントを使用して、 [ **KSPROPERTY\_接続\_ALLOCATORFRAMING\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff565101) pin のフレームの要件を取得するプロパティ。 参照してください[AVStream アロケーター](avstream-allocators.md)詳細についてはします。

このセクションには、次の追加情報が含まれています。

[既定のアロケーター](default-allocators.md)

[特定のアロケーターをフィルター処理します。](filter-specific-allocators.md)

[割り当てのパターン](allocation-schemes.md)

 

 




