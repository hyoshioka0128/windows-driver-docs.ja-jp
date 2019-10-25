---
title: WMI の移植
description: WMI の移植
ms.assetid: 10843A15-3F6F-4DB5-A43B-4D9964DD3312
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94dce4edc0e10a58e701060d0ed5f721c7d86d26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842246"
---
# <a name="porting-wmi"></a>WMI の移植


\[は KMDF にのみ適用され\]

[**IRP\_MJ\_SYSTEM\_CONTROL**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)要求は、WMI データの要求を表します。 WDM ドライバーは、 [*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)関数を実装し、WMI データプロバイダーとして登録することで、このような要求を処理します。 このような要求に応答しない WDM ドライバーは、Irp を次の下位のドライバーに渡すだけの*DispatchSystemControl*ルーチンを実装します。

KMDF ドライバーの場合、フレームワークは、 [**IRP\_MJ\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)の既定の処理を提供します。 Wmi データを提供しないドライバーは、WMI 関連のコードを含める必要はありません。 代わりに、フレームワークはドライバーに代わって、次の下位のドライバーに要求を渡します。

実装の詳細については、「 [KMDF ドライバーでの WMI のサポート](supporting-wmi-in-kmdf-drivers.md)」を参照してください。

 

 





