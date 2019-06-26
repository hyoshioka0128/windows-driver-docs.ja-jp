---
title: RDBSS が使用しないルーチン
description: RDBSS が使用しないルーチン
ms.assetid: bf3e2936-05c9-4012-a55b-40022844f5db
keywords:
- ミニ-リダイレクター WDK、RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 114552f3848f9da5b0b440436681dcd58e6f9356
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371932"
---
# <a name="routines-not-used-by-rdbss"></a>RDBSS が使用しないルーチン


多くのルーチン、MINIRDR に記載\_ディスパッチ構造が呼び出されるか RDBSS で使用できません。 呼び出されないために、これらのルーチンのいずれかを実装するために、ネットワーク ミニ リダイレクターの必要はありません。 ネットワークのミニ リダイレクターを設定する必要があります、 **NULL** 、MINIRDR でこれらすべてのルーチンへのポインター\_に渡された構造体のディスパッチ[ **RxRegisterMinirdr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxregisterminirdr)その[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン。

次は RDBSS では使用されませんルーチンの完全な一覧です。

-   **MRxCancel**

-   **MRxCancelCreateSrvCall**

-   **MRxClosedFcbTimeOut**

-   **MRxClosedSrvOpenTimeOut**

-   **MRxClosePrintFile**

-   **MRxEnumeratePrintQueue**

-   **MRxLowIOSubmit\[LOWIO\_OP\_で\]**

-   **MRxOpenPrintFile**

-   **MRxUpdateNetRootState**

-   **MRxWritePrintFile**

 

 




