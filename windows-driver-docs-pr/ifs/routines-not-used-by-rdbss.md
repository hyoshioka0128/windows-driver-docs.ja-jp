---
title: ルーチン RDBSS では使用されません。
description: ルーチン RDBSS では使用されません。
ms.assetid: bf3e2936-05c9-4012-a55b-40022844f5db
keywords:
- ミニ-リダイレクター WDK、RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccdc6dc02d32e4916320c15136b250dcfa4009e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536451"
---
# <a name="routines-not-used-by-rdbss"></a>ルーチン RDBSS では使用されません。


多くのルーチン、MINIRDR に記載\_ディスパッチ構造が呼び出されるか RDBSS で使用できません。 呼び出されないために、これらのルーチンのいずれかを実装するために、ネットワーク ミニ リダイレクターの必要はありません。 ネットワークのミニ リダイレクターを設定する必要があります、 **NULL** 、MINIRDR でこれらすべてのルーチンへのポインター\_に渡された構造体のディスパッチ[ **RxRegisterMinirdr** ](https://msdn.microsoft.com/library/windows/hardware/ff554693)その[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチン。

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

 

 




