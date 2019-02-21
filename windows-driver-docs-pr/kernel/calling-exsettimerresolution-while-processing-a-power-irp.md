---
title: 電源 IRP の処理中に呼び出す ExSetTimerResolution
description: 電源 IRP の処理中に呼び出す ExSetTimerResolution
ms.assetid: 999a76ab-1586-4157-bfa7-8cc5dd517c71
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6192ccde5d916080620a6180b89055adfe6c5aac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529191"
---
# <a name="calling-exsettimerresolution-while-processing-a-power-irp"></a>電源 IRP の処理中に呼び出す ExSetTimerResolution


処理中に、 [ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)要求、リソースの電源マネージャが、ロックを保持[ **ExSetTimerResolution** ](https://msdn.microsoft.com/library/windows/hardware/ff545614)を完了するを取得する必要があります。 その結果、ドライバーが直接的または間接的には、電源の要求の処理中にこのルーチンを呼び出すし、ドライバー、電源の要求の完了を待たずに、ルーチンの呼び出しを待機する場合、デッドロックが発生します。 電源の要求を処理中にドライバーを安全に呼び出す**ExSetTimerResolution**ドライバーは、電源の要求を完了するまでにこのルーチンの呼び出しを待機しない場合にのみです。 たとえば、ドライバーを呼び出すワーカー スレッドを作成できます**ExSetTimerResolution**ドライバーは、このルーチンへの呼び出しが戻るを待たず、電源の要求を完了するし限り、します。

 

 




