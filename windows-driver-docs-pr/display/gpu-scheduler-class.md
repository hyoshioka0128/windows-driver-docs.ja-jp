---
title: GPU スケジューラ クラス
description: GPU スケジューラ クラス
ms.assetid: 39d38787-588d-483b-9b36-14a3bc16df7c
keywords:
- GPU スケジューラ クラス WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74242c096240e08832d73a81f16766f73cf5783c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379947"
---
# <a name="gpu-scheduler-class"></a>GPU スケジューラ クラス


Windows Display Driver Model (WDDM) には、再入可能な形式での GPU スケジューラ ローダー クラス関数のいずれかへの呼び出しを許可されていません。 つまりが最大で 1 つのスレッド実行できる内で、次の関数のいずれかの特定の時点で。

-   [*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)

-   [*DxgkDdiPatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)

-   [*DxgkDdiPreemptCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_preemptcommand)

-   [*DxgkDdiSubmitCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)

 

 





