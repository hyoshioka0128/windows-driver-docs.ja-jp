---
title: RDBSS が使用しないルーチン
description: RDBSS が使用しないルーチン
ms.assetid: bf3e2936-05c9-4012-a55b-40022844f5db
keywords:
- ミニリダイレクター WDK、RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 183069f6d22ce2d5c6c390a9a42d115fa4732d8c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840980"
---
# <a name="routines-not-used-by-rdbss"></a>RDBSS が使用しないルーチン


MINIRDR\_ディスパッチ構造体に示されている多くのルーチンが、RDBSS で呼び出されていないか、使用されていません。 ネットワークミニリダイレクターは呼び出されないため、これらのルーチンを実装する必要はありません。 ネットワークミニリダイレクターは、その[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンから[**RxRegisterMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)に渡された minirdr\_ディスパッチ構造に含まれるすべてのルーチンに**NULL**ポインターを設定する必要があります。

RDBSS によって使用されていないルーチンの完全な一覧を次に示します。

-   **MRxCancel**

-   **MRxCancelCreateSrvCall**

-   **MRxClosedFcbTimeOut**

-   **MRxClosedSrvOpenTimeOut**

-   **MRxClosePrintFile**

-   **MRxEnumeratePrintQueue**

-   **MRxLowIOSubmit\[LOWIO\_OP\_CLEAROUT\]**

-   **MRxOpenPrintFile**

-   **MRxUpdateNetRootState**

-   **MRxWritePrintFile**

 

 




