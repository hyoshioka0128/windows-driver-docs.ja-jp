---
title: タイマーのサービス提供
description: タイマーのサービス提供
ms.assetid: 6a80a55b-4c7e-4a48-8903-0a1fb28af153
keywords:
- タイマーサービス WDK NDIS
- NDIS タイマーサービス WDK
- NDIS タイマーの取り消し
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3276ec663f4a69761510e305df2578abac0c2cc1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841954"
---
# <a name="servicing-timers"></a>タイマーのサービス提供





Ndis は、NDIS 6.0 タイマーが発生したときに[**Nettimercallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_timer_function)関数を呼び出します。 この関数の*Functioncontext*パラメーターには、ドライバーによって提供されるコンテキスト領域へのポインターが含まれています。 *Functioncontext*の既定値は、 [**NDIS\_TIMER\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_timer_characteristics)の構造体で指定されます。 ドライバーは、 [**NdisAllocateTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatetimerobject)関数に構造体を渡して、関連付けられているタイマーオブジェクトを割り当て、初期化します。

ドライバーが、 [**NdisSetTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject)関数に渡される*FUNCTIONCONTEXT*パラメーターに NULL 以外の値を指定した場合、NDIS は*Nettimercallback*関数の*functioncontext*パラメーターにその値を渡します。 それ以外の場合、NDIS は、NDIS\_TIMER\_特性の構造に指定されている既定値を渡します。

どの NDIS ドライバーにも、複数の*Nettimercallback*関数を含めることができます。 これらの各*Nettimercallback*関数は、ドライバーによって割り当てられた別のタイマーオブジェクトに関連付けられている必要があります。

[**NdisSetTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject)関数を呼び出すと、タイマーオブジェクトに関連付けられている*nettimercallback*関数が、指定された間隔または定期的に実行されます。

*Nettimercallback*関数の呼び出しを停止するには、 [**NdisCancelTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceltimerobject)関数を呼び出します。 **NdisCancelTimerObject**の呼び出しの前にタイムアウトが既に期限切れになっている場合、NDIS は*nettimercallback*を呼び出す可能性があります。

*Nettimercallback*関数が他のドライバー関数とリソースを共有する場合、ドライバーは、スピンロックを使用してリソースへのアクセスを同期する必要があります。

 

 





