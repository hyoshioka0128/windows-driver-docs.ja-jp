---
title: WMI の移植
description: WMI の移植
ms.assetid: 10843A15-3F6F-4DB5-A43B-4D9964DD3312
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77fab706be9335b7bbbe811e40dba799934ec99a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379644"
---
# <a name="porting-wmi"></a>WMI の移植


\[KMDF にのみ適用されます。\]

[ **IRP\_MJ\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)要求は、WMI データの要求を表します。 WDM ドライバーが実装することでこのような要求を処理する[ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)関数と WMI データ プロバイダーとして登録します。 このような要求に応答しない WDM ドライバーの実装を*DispatchSystemControl*ルーチン [次へ] の下のドライバー Irp を渡すだけです。

KMDF ドライバーでは、フレームワークには、既定の処理が用意されて[ **IRP\_MJ\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)します。 WMI データを提供しないドライバーは、WMI に関連するコードを含める必要はありません。 代わりに、フレームワークは、ドライバーの代わり、[次へ] の下のドライバーに要求を渡します。

実装の詳細については、次を参照してください。 [KMDF ドライバーでサポートしている WMI](supporting-wmi-in-kmdf-drivers.md)します。

 

 





