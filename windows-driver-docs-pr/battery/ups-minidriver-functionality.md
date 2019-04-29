---
title: UPS ミニドライバーの機能
description: UPS ミニドライバーの機能
ms.assetid: a93dbada-bcf7-4963-ba57-c6db5922c66b
keywords:
- UPS のミニドライバー WDK、機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 397696d91b29aeb41e00237f9279d408131489c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335057"
---
# <a name="ups-minidriver-functionality"></a>UPS ミニドライバーの機能


## <span id="ddk_ups_minidriver_functionality_kg"></span><span id="DDK_UPS_MINIDRIVER_FUNCTIONALITY_KG"></span>


UPS ミニドライバーは、UPS システム提供サービスによって呼び出される関数の次のセットをエクスポートする必要があります。

-   [**UPSInit**](https://msdn.microsoft.com/library/windows/hardware/ff536313)

-   [**UPSGetState**](https://msdn.microsoft.com/library/windows/hardware/ff536312)

-   [**UPSWaitForStateChange**](https://msdn.microsoft.com/library/windows/hardware/ff536316)

-   [**UPSCancelWait**](https://msdn.microsoft.com/library/windows/hardware/ff536311)

-   [**UPSTurnOff**](https://msdn.microsoft.com/library/windows/hardware/ff536315)

-   [**UPSStop**](https://msdn.microsoft.com/library/windows/hardware/ff536314)

ミニドライバーがさらに、エクスポートする必要があります、 [ **DLLMain** ](https://msdn.microsoft.com/library/windows/desktop/ms682583)関数は、Microsoft Windows SDK のドキュメントで説明されているとします。

これらの関数をエクスポートするだけでなく、ミニドライバーはの初期値を提供する必要があります[UPS レジストリ エントリ](ups-registry-entries.md)および UPS 状態の変更を反映するために必要に応じて、値を変更します。

通常、UPS ミニドライバーと通信する COM ポートを介して UPS ユニットを呼び出して、 [ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)、 [ **ReadFile**](https://msdn.microsoft.com/library/windows/desktop/aa365467)、および[**WriteFile** ](https://msdn.microsoft.com/library/windows/desktop/aa365747)関数 (Windows SDK のドキュメントで説明)。 ミニドライバーはどのような通信プロトコル、UPS 単位のサポートを実装する責任を負います。

 

 




