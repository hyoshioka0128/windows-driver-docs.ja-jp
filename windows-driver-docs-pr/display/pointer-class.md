---
title: ポインター クラス
description: ポインター クラス
ms.assetid: c988535a-d218-48de-bdc2-56a620bbe4a2
keywords:
- ポインタークラス WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17075ddeae45ba9c361bc55feef9d821777f8eee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829783"
---
# <a name="pointer-class"></a>ポインター クラス


Windows Display Driver Model (WDDM) では、ポインタークラス関数のいずれかを再入可能な方法で呼び出すことは許可されていません。 つまり、最大で1つのスレッドは、特定の時点で次のいずれかの関数内で実行できます。

-   [*DxgkDdiSetPointerPosition*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setpointerposition)

-   [*DxgkDdiSetPointerShape*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setpointershape)

 

 





