---
title: DMA のプログラミング手法
description: DMA のプログラミング手法
ms.assetid: bdd8ffa4-8f09-41ed-b0f8-8edabbe65393
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: da41db80c79a48b7c55f7621b749a869f3f8c676
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387183"
---
# <a name="dma-programming-techniques"></a>DMA のプログラミング手法


ダイレクト メモリ アクセス (DMA) では、中央のプロセッサ (CPU) と特定のデバイス間でメモリ ベースのデータを転送するための最も基本的なハードウェア技術の 1 つです。 コンピューターのシステムでは、これは、CPU、他の操作を許可する、メモリ転送を処理する中間デバイス DMA コント ローラーを使用します。

ドライバーは、DMA コント ローラーを使用して、メモリ ベースのデータを直接転送することができます。 次のトピックでは、入出力のプログラミングに関連する DMA 問題について説明します。

ドライバーには、アダプター オブジェクトに DMA を使用できます。 アダプター オブジェクトの詳細については、次を参照してください。[アダプター オブジェクトと DMA](adapter-objects-and-dma.md)します。

ドライバーがシステム メモリ、およびそのデバイスの間でデータを転送する際、システムの DMA コント ローラーのキャッシュまたは 1 つまたは複数のプロセッサのキャッシュ内のデータをキャッシュできます。 DMA とキャッシュの詳細については、次を参照してください。 [DMA 操作中にキャッシュされたデータをフラッシュ](flushing-cached-data-during-dma-operations.md)します。

DMA 操作をより小さなチャンクに分割する必要がある場合は、次を参照してください。 [DMA の転送要求の分割](splitting-dma-transfer-requests.md)します。

バージョン 3 の DMA 操作インターフェイスでは、Windows 8 以降で使用できます。 このインターフェイスの詳細については、次を参照してください。 [DMA 操作のインターフェイスのバージョン 3](version-3-of-the-dma-operations-interface.md)します。

 

 




