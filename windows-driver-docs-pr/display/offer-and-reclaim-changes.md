---
title: 変更の提供と再利用
description: Windows Display Driver Model (WDDM) v2 でのプランと再利用に関する要件が緩和されています。
ms.assetid: 1A987708-DE73-4998-B5F9-03A9D502205A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12a3a0e7f72c6fec26bc232e13ca9803df7c48ba
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383994"
---
# <a name="offer-and-reclaim-changes"></a>変更の提供と再利用


Windows Display Driver Model (WDDM) v2、関連する要件の*提供*と*回収*緩和されています。 ユーザー モード ドライバーをプランを使用し、内部の割り当てを解放する必要なくなりました。 使用してアプリケーションのアイドル状態や中断されたドライバーの内部リソースの削除は、**トリミング**Microsoft DirectX 11.1 で導入された API です。

API レベルでサポートされなければならないプランと再利用を引き続きし、プランまたはカーネルにリソースを解放するアプリケーションの要求を転送するように、ユーザー モード ドライバーが必要です。 WDDM v2 では、割り当ての一覧を割り当ての提供はサポートされなくとその結果、ユーザー モード ドライバーはプランを実装し、再利用方法を変更する必要があります。

アプリケーションが提供している必要がありますによって提供されるすぐに、ユーザー モード ドライバーでは、呼び出すことによってリソース**OfferCb**リソースすべてにわたってビルド中、ダイレクト メモリ アクセス (DMA) バッファーの参照があるない場合は、コンテキスト。 ユーザー モード ドライバーがへの呼び出しを遅らせる場合は、リソースがある保留中のビルド中 DMA バッファー内の参照は、 **OfferCb**まで依存 DMA バッファーがを介して送信された後[ *RenderCb*](https://msdn.microsoft.com/library/windows/hardware/ff568923). グラフィックスのカーネルがリソースを提供する安全では、ユーザー モード ドライバーはへの呼び出しを遅延させるについて心配する必要があるようになるまで、非ブロッキングの方法で、操作を延期することが取得されます**OfferCb**まで、依存する操作は、グラフィックス処理装置 (GPU) で完了します。

常駐要件の一覧に存在する場合、通話の再利用は割り当てでページに自動的に (つまり、ユーザーまたはドライバーが要求されました、割り当てを使用して存在する、 [ *MakeResidentCb* ](https://msdn.microsoft.com/library/windows/hardware/dn906357)呼び出します)。 [ **ReclaimAllocations2Cb**](https://msdn.microsoft.com/library/windows/hardware/dn903528)この操作は非同期で、およびページング フェンスが返されから返されたフェンスと同じ方法を処理する必要があります*MakeResidentCb*. フェンスがシグナルを受け取るされる常駐 GPU 上で使用できるようにするため、割り当てのことが保証されます。

取得した直後に[ **ReclaimAllocationsCb**](https://msdn.microsoft.com/library/windows/hardware/hh451695)/[**ReclaimAllocations2Cb**](https://msdn.microsoft.com/library/windows/hardware/dn903528)、バッキング ストア割り当てを有効にすることが保証され、割り当ては、CPU へのアクセスを使用して下に配置することがあります[ *Lock2Cb*](https://msdn.microsoft.com/library/windows/hardware/dn914483)します。 ドライバーは、そのためにはページング フェンスで待機する必要はありません。

 

 





