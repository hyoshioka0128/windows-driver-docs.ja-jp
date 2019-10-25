---
title: 変更の提供と再利用
description: Windows Display Driver Model (WDDM) v2 では、オファーと再利用に関する要件が緩和されています。
ms.assetid: 1A987708-DE73-4998-B5F9-03A9D502205A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce81472b86ae091ee7cd5e1e7450035c92e54427
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840501"
---
# <a name="offer-and-reclaim-changes"></a>変更の提供と再利用


Windows Display Driver Model (WDDM) v2 では、*オファー*と再*利用*に関する要件が緩和されています。 ユーザーモードドライバーは、内部割り当てでプランを使用して再利用するために必要なくなりました。 アイドル/中断されたアプリケーションは、Microsoft DirectX 11.1 で導入された**Trim**API を使用して、ドライバーの内部リソースを排除します。

プランと再利用は引き続き API レベルでサポートされます。ユーザーモードドライバーは、アプリケーションの要求を転送してカーネルにリソースを提供または解放する必要があります。 WDDM v2 では、割り当てリストによる割り当ての提供はサポートされなくなりました。そのため、ユーザーモードドライバーは、プランの実装方法と再利用方法を変更する必要があります。

アプリケーションによって提供されるリソースは、 **OfferCb**を呼び出すことにより、ユーザーモードドライバーによってすぐに提供される必要があります。これは、リソースが、現在すべてのコンテキストにわたって構築されているダイレクトメモリアクセス (DMA) バッファーに参照されていない場合です。 作成中の DMA バッファー内のリソースの参照が保留中の場合、ユーザーモードドライバーは、依存する DMA バッファーが[*Rendercb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)を介して送信されるまで、 **OfferCb**への呼び出しを延期する必要があります。 グラフィックスカーネルは、リソースを安全に提供できるようになるまで、非ブロッキングの方法で操作を延期することに対処します。そのため、ユーザーモードドライバーは、依存操作が完了するまで**OfferCb**への呼び出しを遅延させる必要があることを心配する必要はありません。グラフィックス処理装置 (GPU) 上。

再利用の要求の一覧にある場合 (つまり、ユーザーまたはドライバーが割り当てを[*MakeResidentCb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)呼び出しによって配置するように要求した場合)、解放を呼び出すと自動的にページが割り当てられます。 [**ReclaimAllocations2Cb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocations2cb)の場合、この操作は非同期であり、ページングフェンスが返されます。 *MakeResidentCb*から返されるフェンスと同じように処理する必要があります。 フェンスがシグナル状態になると、割り当ては、GPU 上で存在し、使用可能であることが保証されます。

[**ReclaimAllocationsCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocationscb)/[**ReclaimAllocations2Cb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocations2cb)から制御が戻った直後に、割り当てのバッキングストアが有効であることが保証され、割り当てが[*Lock2Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock2cb)経由で CPU アクセスの下に配置される可能性があります。 ドライバーは、ページングフェンスを待機する必要はありません。

 

 





