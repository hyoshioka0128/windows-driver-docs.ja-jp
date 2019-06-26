---
title: 電源 IRP 処理中の ExSetTimerResolution の呼び出し
description: 電源 IRP 処理中の ExSetTimerResolution の呼び出し
ms.assetid: 999a76ab-1586-4157-bfa7-8cc5dd517c71
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bc726cb698c5a5a6076f53cb78d7ba8c112120f4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385277"
---
# <a name="calling-exsettimerresolution-while-processing-a-power-irp"></a>電源 IRP 処理中の ExSetTimerResolution の呼び出し


処理中に、 [ **IRP\_MJ\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)要求、リソースの電源マネージャが、ロックを保持[ **ExSetTimerResolution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exsettimerresolution)を完了するを取得する必要があります。 その結果、ドライバーが直接的または間接的には、電源の要求の処理中にこのルーチンを呼び出すし、ドライバー、電源の要求の完了を待たずに、ルーチンの呼び出しを待機する場合、デッドロックが発生します。 電源の要求を処理中にドライバーを安全に呼び出す**ExSetTimerResolution**ドライバーは、電源の要求を完了するまでにこのルーチンの呼び出しを待機しない場合にのみです。 たとえば、ドライバーを呼び出すワーカー スレッドを作成できます**ExSetTimerResolution**ドライバーは、このルーチンへの呼び出しが戻るを待たず、電源の要求を完了するし限り、します。

 

 




