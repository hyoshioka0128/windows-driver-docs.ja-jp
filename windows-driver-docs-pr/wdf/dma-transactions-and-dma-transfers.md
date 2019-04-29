---
title: DMA トランザクションと DMA 転送
description: DMA トランザクションと DMA 転送
ms.assetid: afcbe756-1a45-410b-8260-2c2c611e6a70
keywords:
- DMA トランザクション WDK KMDF
- DMA 操作 WDK KMDF、トランザクション
- バス マスター DMA WDK KMDF、トランザクション
- DMA 操作 WDK KMDF、転送
- バス マスター DMA WDK KMDF の転送
- DMA は、WDK KMDF を転送します。
- DMA トランザクション WDK KMDF、DMA トランザクションについて
- DMA では、WDK の KMDF を転送 DMA 転送について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38b52b071fc939380b40b9c386798088f95ab348
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327870"
---
# <a name="dma-transactions-and-dma-transfers"></a>DMA トランザクションと DMA 転送


\[KMDF にのみ適用されます。\]




フレームワークがバス マスターとシステム モードの DMA 操作を処理する方法を理解しておく必要があります、次の 2 つの用語。

<a href="" id="dma-transaction"></a>**DMA トランザクション**  
DMA トランザクションは、1 つの読み取りまたは書き込みをアプリケーションからの要求などの I/O 操作を完了するには、です。

<a href="" id="dma-transfer"></a>**DMA の転送**  
DMA 転送は、デバイスにコンピューターのメモリから、またはコンピューターのメモリをデバイスからデータを転送する 1 つのハードウェア操作です。

常に 1 つの DMA トランザクションは、少なくとも 1 つの DMA 転送ので構成されますが、トランザクションは、多くの転送で構成できます。

フレームワーク ベースのドライバーが、I/O 要求を受け取ったときに、ドライバーは通常、要求を表す 1 つの DMA トランザクション オブジェクトを作成します。 トランザクションをサービス フレームワークの開始時に、デバイスが 1 つの転送にトランザクション全体を処理できるかどうかを決定します。 トランザクションが大きすぎる場合、フレームワークは、トランザクションを複数の転送に分割します。

 

 





