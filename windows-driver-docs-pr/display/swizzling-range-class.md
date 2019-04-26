---
title: スウィズリング範囲クラス
description: スウィズリング範囲クラス
ms.assetid: 2f5d5b91-ebd8-4242-8719-8a21bc3e9888
keywords:
- スウィズ リング範囲クラス WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7216397e9518a45acb06d289c7d9f777e37efdd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345503"
---
# <a name="swizzling-range-class"></a>スウィズリング範囲クラス


Windows Display Driver Model (WDDM) は許可されていません、スウィズ リングのいずれかへの呼び出しを範囲クラス関数再入可能な方法で。 つまりが最大で 1 つのスレッド実行できる内で、次の関数のいずれかの特定の時点で。

-   [*DxgkDdiAcquireSwizzlingRange*](https://msdn.microsoft.com/library/windows/hardware/ff559582)

-   [*DxgkDdiReleaseSwizzlingRange*](https://msdn.microsoft.com/library/windows/hardware/ff559786)

 

 





