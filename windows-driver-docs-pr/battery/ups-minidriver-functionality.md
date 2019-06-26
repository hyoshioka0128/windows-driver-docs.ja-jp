---
title: UPS ミニドライバーの機能
description: UPS ミニドライバーの機能
ms.assetid: a93dbada-bcf7-4963-ba57-c6db5922c66b
keywords:
- UPS のミニドライバー WDK、機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14acc80101a87b3ed0e614bd81b1288458969699
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364710"
---
# <a name="ups-minidriver-functionality"></a>UPS ミニドライバーの機能


## <span id="ddk_ups_minidriver_functionality_kg"></span><span id="DDK_UPS_MINIDRIVER_FUNCTIONALITY_KG"></span>


UPS ミニドライバーは、UPS システム提供サービスによって呼び出される関数の次のセットをエクスポートする必要があります。

-   [**UPSInit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/upssvc/nf-upssvc-upsinit)

-   [**UPSGetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/upssvc/nf-upssvc-upsgetstate)

-   [**UPSWaitForStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/upssvc/nf-upssvc-upswaitforstatechange)

-   [**UPSCancelWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/upssvc/nf-upssvc-upscancelwait)

-   [**UPSTurnOff**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/upssvc/nf-upssvc-upsturnoff)

-   [**UPSStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/upssvc/nf-upssvc-upsstop)

ミニドライバーがさらに、エクスポートする必要があります、 [ **DLLMain** ](https://docs.microsoft.com/windows/desktop/Dlls/dllmain)関数は、Microsoft Windows SDK のドキュメントで説明されているとします。

これらの関数をエクスポートするだけでなく、ミニドライバーはの初期値を提供する必要があります[UPS レジストリ エントリ](ups-registry-entries.md)および UPS 状態の変更を反映するために必要に応じて、値を変更します。

通常、UPS ミニドライバーと通信する COM ポートを介して UPS ユニットを呼び出して、 [ **CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)、 [ **ReadFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)、および[**WriteFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile)関数 (Windows SDK のドキュメントで説明)。 ミニドライバーはどのような通信プロトコル、UPS 単位のサポートを実装する責任を負います。

 

 




