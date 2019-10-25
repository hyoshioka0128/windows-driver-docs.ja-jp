---
title: スウィズリング範囲クラス
description: スウィズリング範囲クラス
ms.assetid: 2f5d5b91-ebd8-4242-8719-8a21bc3e9888
keywords:
- スウィズリング範囲クラスの WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dc6ffabc3a670520d5aa889f70f1a33a4b1936b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829540"
---
# <a name="swizzling-range-class"></a>スウィズリング範囲クラス


Windows Display Driver Model (WDDM) では、スウィズリング range クラス関数のいずれかを再入可能な方法で呼び出すことは許可されていません。 つまり、最大で1つのスレッドは、特定の時点で次のいずれかの関数内で実行できます。

-   [*DxgkDdiAcquireSwizzlingRange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_acquireswizzlingrange)

-   [*DxgkDdiReleaseSwizzlingRange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_releaseswizzlingrange)

 

 





