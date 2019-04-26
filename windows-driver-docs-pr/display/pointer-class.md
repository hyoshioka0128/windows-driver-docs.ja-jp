---
title: ポインター クラス
description: ポインター クラス
ms.assetid: c988535a-d218-48de-bdc2-56a620bbe4a2
keywords:
- ポインター クラス WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 969e92d6642e483a9e4f57f0fc262cf847e1f6c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358446"
---
# <a name="pointer-class"></a>ポインター クラス


Windows Display Driver Model (WDDM) は、再入可能な方法で、ポインター クラス関数のいずれかへの呼び出しを許可されていません。 つまりが最大で 1 つのスレッド実行できる内で、次の関数のいずれかの特定の時点で。

-   [*DxgkDdiSetPointerPosition*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setpointerposition)

-   [*DxgkDdiSetPointerShape*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setpointershape)

 

 





