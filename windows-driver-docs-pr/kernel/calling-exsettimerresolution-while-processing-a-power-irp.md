---
title: 電源 IRP 処理中の ExSetTimerResolution の呼び出し
description: 電源 IRP 処理中の ExSetTimerResolution の呼び出し
ms.assetid: 999a76ab-1586-4157-bfa7-8cc5dd517c71
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a0e7e496b46ad506e72791139948aab13ad9b086
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837173"
---
# <a name="calling-exsettimerresolution-while-processing-a-power-irp"></a>電源 IRP 処理中の ExSetTimerResolution の呼び出し


[**IRP\_MJ\_の電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)要求の処理中に、power manager は、 [**Exsettimerresolution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimerresolution)を完了するために取得する必要があるリソースのロックを保持します。 その結果、ドライバーが電源要求の処理中にこのルーチンを直接または間接的に呼び出し、その後、ルーチンへの呼び出しが完了するのを待ってから、ドライバーが電源要求を完了するまでの間、デッドロックが発生します。 ドライバーは、電源要求の処理中に、このルーチンへの呼び出しが戻るのを待たずに電源要求を完了する場合にのみ、 **Exsettimerresolution**を安全に呼び出すことができます。 たとえば、ドライバーは、このルーチンへの呼び出しが返されるのを待たずに、ドライバーが電源要求を完了するまで、 **Exsettimerresolution**を呼び出すワーカースレッドを作成できます。

 

 




