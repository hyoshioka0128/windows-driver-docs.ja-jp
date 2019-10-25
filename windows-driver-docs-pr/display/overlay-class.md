---
title: オーバーレイ クラス
description: オーバーレイ クラス
ms.assetid: 698eb8af-ff9a-4c11-b764-6e5773886aaa
keywords:
- オーバーレイクラスの WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cec3b75dd407f3fe4a253a724de87f7110c98885
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826088"
---
# <a name="overlay-class"></a>オーバーレイ クラス


Windows Display Driver Model (WDDM) では、オーバーレイクラス関数のいずれかを再入可能な方法で呼び出すことは許可されていません。 つまり、最大で1つのスレッドは、特定の時点で次のいずれかの関数内で実行できます。

-   [*DxgkDdiCreateOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createoverlay)

-   [*DxgkDdiDestroyOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_destroyoverlay)

-   [*DxgkDdiFlipOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_flipoverlay)

-   [*DxgkDdiUpdateOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updateoverlay)

 

 





