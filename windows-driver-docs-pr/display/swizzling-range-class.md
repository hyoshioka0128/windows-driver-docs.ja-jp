---
title: スウィズ リング範囲クラス
description: スウィズ リング範囲クラス
ms.assetid: 2f5d5b91-ebd8-4242-8719-8a21bc3e9888
keywords:
- スウィズ リング範囲クラス WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7216397e9518a45acb06d289c7d9f777e37efdd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559609"
---
# <a name="swizzling-range-class"></a>スウィズ リング範囲クラス


Windows Display Driver Model (WDDM) は許可されていません、スウィズ リングのいずれかへの呼び出しを範囲クラス関数再入可能な方法で。 つまりが最大で 1 つのスレッド実行できる内で、次の関数のいずれかの特定の時点で。

-   [*DxgkDdiAcquireSwizzlingRange*](https://msdn.microsoft.com/library/windows/hardware/ff559582)

-   [*DxgkDdiReleaseSwizzlingRange*](https://msdn.microsoft.com/library/windows/hardware/ff559786)

 

 





