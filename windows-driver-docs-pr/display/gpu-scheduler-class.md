---
title: GPU Scheduler クラス
description: GPU Scheduler クラス
ms.assetid: 39d38787-588d-483b-9b36-14a3bc16df7c
keywords:
- GPU スケジューラ クラス WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c203c7e97016a344d92f3f85661e21c0ce68eff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529162"
---
# <a name="gpu-scheduler-class"></a>GPU Scheduler クラス


Windows Display Driver Model (WDDM) には、再入可能な形式での GPU スケジューラ ローダー クラス関数のいずれかへの呼び出しを許可されていません。 つまりが最大で 1 つのスレッド実行できる内で、次の関数のいずれかの特定の時点で。

-   [*DxgkDdiBuildPagingBuffer*](https://msdn.microsoft.com/library/windows/hardware/ff559587)

-   [*DxgkDdiPatch*](https://msdn.microsoft.com/library/windows/hardware/ff559737)

-   [*DxgkDdiPreemptCommand*](https://msdn.microsoft.com/library/windows/hardware/ff559741)

-   [*DxgkDdiSubmitCommand*](https://msdn.microsoft.com/library/windows/hardware/ff560790)

 

 





