---
title: GPU スケジューラクラス
description: GPU スケジューラクラス
ms.assetid: 39d38787-588d-483b-9b36-14a3bc16df7c
keywords:
- GPU スケジューラクラス WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 752a168d0ed4dc6cd43130d353281c4196c6cc0b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838927"
---
# <a name="gpu-scheduler-class"></a>GPU スケジューラクラス


Windows Display Driver Model (WDDM) では、GPU スケジューラローダークラス関数のいずれかを再入可能な方法で呼び出すことは許可されていません。 つまり、最大で1つのスレッドは、特定の時点で次のいずれかの関数内で実行できます。

-   [*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)

-   [*DxgkDdiPatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)

-   [*DxgkDdiPreemptCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_preemptcommand)

-   [*DxgkDdiSubmitCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)

 

 





