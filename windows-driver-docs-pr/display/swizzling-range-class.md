---
title: スウィズリング範囲クラス
description: スウィズリング範囲クラス
ms.assetid: 2f5d5b91-ebd8-4242-8719-8a21bc3e9888
keywords:
- スウィズ リング範囲クラス WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8a4babc427745f13fe736227da9cd6a53f877c0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372056"
---
# <a name="swizzling-range-class"></a>スウィズリング範囲クラス


Windows Display Driver Model (WDDM) は許可されていません、スウィズ リングのいずれかへの呼び出しを範囲クラス関数再入可能な方法で。 つまりが最大で 1 つのスレッド実行できる内で、次の関数のいずれかの特定の時点で。

-   [*DxgkDdiAcquireSwizzlingRange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_acquireswizzlingrange)

-   [*DxgkDdiReleaseSwizzlingRange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_releaseswizzlingrange)

 

 





