---
title: WMI の移植
description: WMI の移植
ms.assetid: 10843A15-3F6F-4DB5-A43B-4D9964DD3312
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dac2952f884cf89be0ac9a1a4074c9827cf06a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557952"
---
# <a name="porting-wmi"></a>WMI の移植


\[KMDF にのみ適用されます。\]

[ **IRP\_MJ\_システム\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550813)要求は、WMI データの要求を表します。 WDM ドライバーが実装することでこのような要求を処理する[ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)関数と WMI データ プロバイダーとして登録します。 このような要求に応答しない WDM ドライバーの実装を*DispatchSystemControl*ルーチン [次へ] の下のドライバー Irp を渡すだけです。

KMDF ドライバーでは、フレームワークには、既定の処理が用意されて[ **IRP\_MJ\_システム\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550813)します。 WMI データを提供しないドライバーは、WMI に関連するコードを含める必要はありません。 代わりに、フレームワークは、ドライバーの代わり、[次へ] の下のドライバーに要求を渡します。

実装の詳細については、次を参照してください。 [KMDF ドライバーでサポートしている WMI](supporting-wmi-in-kmdf-drivers.md)します。

 

 





