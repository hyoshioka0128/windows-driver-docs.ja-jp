---
title: GPU スケジューラ クラス
description: GPU スケジューラ クラス
ms.assetid: 39d38787-588d-483b-9b36-14a3bc16df7c
keywords:
- GPU スケジューラ クラス WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c203c7e97016a344d92f3f85661e21c0ce68eff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379472"
---
# <a name="gpu-scheduler-class"></a>GPU スケジューラ クラス


Windows Display Driver Model (WDDM) には、再入可能な形式での GPU スケジューラ ローダー クラス関数のいずれかへの呼び出しを許可されていません。 つまりが最大で 1 つのスレッド実行できる内で、次の関数のいずれかの特定の時点で。

-   [*DxgkDdiBuildPagingBuffer*](https://msdn.microsoft.com/library/windows/hardware/ff559587)

-   [*DxgkDdiPatch*](https://msdn.microsoft.com/library/windows/hardware/ff559737)

-   [*DxgkDdiPreemptCommand*](https://msdn.microsoft.com/library/windows/hardware/ff559741)

-   [*DxgkDdiSubmitCommand*](https://msdn.microsoft.com/library/windows/hardware/ff560790)

 

 





