---
title: フレームワーク DMA オブジェクト
description: フレームワーク DMA オブジェクト
ms.assetid: a5073bb0-a8c9-49fc-b280-e781f9f9c256
keywords:
- DMA 操作 WDK KMDF、オブジェクト
- バスマスタ DMA WDK KMDF、オブジェクト
- DMA イネーブラーオブジェクト WDK KMDF
- DMA トランザクションオブジェクト WDK KMDF
- 共通バッファーオブジェクト WDK KMDF
- フレームワークオブジェクト WDK KMDF、DMA オブジェクト
- enabler オブジェクト WDK KMDF
- トランザクションオブジェクト WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33892679104e73c60c3e3a1e93dd5621ecf2a74b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843181"
---
# <a name="framework-dma-objects"></a>フレームワーク DMA オブジェクト


\[は KMDF にのみ適用され\]




フレームワークベースのドライバーでバスマスターとシステムモードの DMA 操作を処理するために、フレームワークには次の3つのオブジェクトが用意されています。

<a href="" id="dma-enabler-object"></a>**DMA イネーブラーオブジェクト**  
フレームワークの DMA イネーブラーオブジェクトを使用すると、ドライバーは特定のデバイスに対してフレームワークの DMA サポートを使用できます。 ドライバーは、DMA 操作をサポートする各デバイスの DMA イネーブラーオブジェクトを作成する必要があります。

<a href="" id="dma-transaction-object"></a>**DMA トランザクションオブジェクト**  
フレームワークの DMA トランザクションオブジェクトは、単一の DMA i/o 操作を表します。 フレームワークベースのドライバーは、通常、デバイスが DMA を使用して要求された操作を実行する場合に、受信する各 i/o 要求に対して DMA トランザクションオブジェクトを作成します。

<a href="" id="common-buffer-object"></a>**共通バッファーオブジェクト**  
フレームワークの共通バッファーオブジェクトは、ドライバーとデバイスの両方によって同時にアクセスできるようにマップされたコンピューターメモリの領域を表します。 一部のドライバーでは、DMA デバイスの i/o 操作を設定するときに[共通のバッファーを使用](using-common-buffers.md)します。

これらのオブジェクトがエクスポートするインターフェイスの詳細については、次を参照してください。

[フレームワークの DMA オブジェクトリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/)

[フレームワーク共通バッファーオブジェクト参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcommonbuffer/)

 

 





