---
title: KMDF ドライバーで DMA 操作の処理
description: ダイレクト メモリ アクセス (DMA) 操作に、KMDF ドライバーが I/O 要求を変換する方法について説明します。 システム モードの DMA および KMDF サポート バス マスターします。
ms.assetid: 1ca8ba66-201d-42f2-a6f1-6184a9d7c2a6
keywords:
- カーネル モード ドライバー WDK KMDF、DMA 操作
- KMDF WDK、DMA 操作
- カーネル モード ドライバー フレームワーク WDK、DMA 操作
- フレームワーク ベースのドライバー WDK KMDF、DMA 操作
- DMA 操作 WDK KMDF
- バス マスター DMA WDK KMDF
- ダイレクト メモリ アクセスの WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 609be5b5f3c7b4f286dd5dc5e8eaf7540a7d0d2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549822"
---
# <a name="handling-dma-operations-in-kmdf-drivers"></a>KMDF ドライバーで DMA 操作の処理


\[KMDF にのみ適用されます。\]

このセクションでは、ダイレクト メモリ アクセス (DMA) 操作に、カーネル モード ドライバー フレームワーク (KMDF) ドライバーが I/O 要求を変換する方法について説明します。 システム モードの DMA および KMDF サポート バス マスターします。




## <a name="in-this-section"></a>このセクションの内容


-   [Windows Driver framework DMA の概要](introduction-to-dma-in-windows-driver-framework.md)
-   [Framework DMA オブジェクト](framework-dma-objects.md)
-   [DMA トランザクションと DMA の転送](dma-transactions-and-dma-transfers.md)
-   [Framework DMA を使用しているサンプル ドライバー](sample-drivers-that-use-framework-dma.md)
-   [KMDF ドライバーでは、バス マスター DMA デバイスの I/O 要求の処理](handling-i-o-requests-in-a-kmdf-driver-for-a-bus-master-dma-device.md)
-   [システム モード DMA をサポートしています。](supporting-system-mode-dma.md)
-   [DMA のトランザクションのキャンセル](canceling-dma-transactions.md)
-   [DMA のリソースを予約](reserving-dma-resources.md)
-   [KMDF ドライバーで DMA のテスト](testing-dma-in-kmdf-drivers.md)

詳細については、WDM ドライバーで DMA 操作をサポートを参照してください[DMA プログラミング手法](https://msdn.microsoft.com/library/windows/hardware/ff544074)します。

 

 





