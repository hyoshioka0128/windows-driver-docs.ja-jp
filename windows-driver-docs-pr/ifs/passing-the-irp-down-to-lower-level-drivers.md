---
title: IRP を下位レベルのドライバーに渡す
description: IRP を下位レベルのドライバーに渡す
ms.assetid: 9a8e72fb-b0a8-4026-8606-57fa03344146
keywords:
- IRP ディスパッチルーチン WDK ファイルシステム、IRP を渡す
- Irp をデバイススタック WDK に渡す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a78b3a0a11f554e1fd77c94992e438ffa20a73da
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841042"
---
# <a name="passing-the-irp-down-to-lower-level-drivers"></a>IRP を下位レベルのドライバーに渡す


## <span id="ddk_passing_the_irp_down_to_lower_level_drivers_if"></span><span id="DDK_PASSING_THE_IRP_DOWN_TO_LOWER_LEVEL_DRIVERS_IF"></span>


既定では、IRP のターゲットデバイスオブジェクトを確認した後、は[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出すことによって、irp を次の下位レベルのデバイスドライバーに渡す必要があります。 フィルタードライバーは、単純に失敗するのではなく、認識されないすべての Irp をパススルーすることが重要です。 不明な Irp に失敗すると、オペレーティングシステム自体が予期しない方法で失敗する可能性があります。 たとえば、ファイルシステムフィルタードライバーで IRP\_MJ\_PNP 要求が失敗した場合、システム休止状態を防ぐことによって電源管理が妨げられる可能性があります。 これは、ファイルシステムフィルタードライバーが電源管理に含まれておらず、 [**IRP\_MJ\_の電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)要求を受信していない場合にも当てはまります。

 

 




