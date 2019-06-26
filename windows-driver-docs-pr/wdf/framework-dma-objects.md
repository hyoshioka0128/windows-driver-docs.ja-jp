---
title: フレームワーク DMA オブジェクト
description: フレームワーク DMA オブジェクト
ms.assetid: a5073bb0-a8c9-49fc-b280-e781f9f9c256
keywords:
- DMA 操作 WDK KMDF、オブジェクト
- バス マスター DMA WDK KMDF、オブジェクト
- DMA イネーブラー オブジェクト WDK KMDF
- DMA トランザクション オブジェクト WDK KMDF
- 共通のバッファー オブジェクト WDK KMDF
- framework オブジェクト WDK KMDF、DMA オブジェクト
- WDK KMDF のオブジェクトの有効化
- トランザクション オブジェクト WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60d8c02e326586d098c4e85c2b1b89091c6dc850
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368679"
---
# <a name="framework-dma-objects"></a>フレームワーク DMA オブジェクト


\[KMDF にのみ適用されます。\]




Framework ベースのドライバー、バス マスターとシステム モードの DMA 操作を処理するには、フレームワークは、3 つのオブジェクトを提供します。

<a href="" id="dma-enabler-object"></a>**DMA イネーブラー オブジェクト**  
フレームワークの DMA イネーブラー オブジェクトは、特定のデバイスに対して DMA のフレームワークのサポートを使用するためのドライバーを使用できます。 ドライバーは、DMA 操作をサポートするデバイスの各 DMA イネーブラー オブジェクトを作成する必要があります。

<a href="" id="dma-transaction-object"></a>**DMA トランザクション オブジェクト**  
フレームワークの DMA トランザクション オブジェクトは、1 つの I/O の DMA 操作を表します。 フレームワーク ベースのドライバーは、デバイスでは、DMA を使用して、要求された操作を実行する場合は、通常、受信の I/O 要求ごとの DMA トランザクション オブジェクトを作成します。

<a href="" id="common-buffer-object"></a>**共通のバッファー オブジェクト**  
Framework の共通のバッファー オブジェクトは、ドライバーとデバイスの両方で同時アクセス用にマップされているコンピューターのメモリの領域を表します。 一部のドライバー[一般的なバッファーを使用して、](using-common-buffers.md) DMA デバイスの I/O 操作を設定する際。

これらのオブジェクトをエクスポートするインターフェイスについてを参照してください。

[Framework DMA オブジェクト参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/)

[バッファー オブジェクト参照の一般的なフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcommonbuffer/)

 

 





