---
title: 完了した要求を処理するコードを修正する
description: 完了した要求を処理するコードを修正する
ms.assetid: 0DD48424-A728-4887-9F26-46B7004CB12C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5871d27f47daa0267843b3f88b97ff733104738a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376222"
---
# <a name="revise-code-that-handles-completed-requests"></a>完了した要求を処理するコードを修正する


Windows Driver Frameworks (WDF) は、I/O 要求を完了する 3 つのメソッドを提供します。

-   [**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)
-   [**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)
-   [**WdfRequestCompleteWithPriorityBoost** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost) (KMDF のみ)

これらのメソッドの使用方法の詳細については、次を参照してください。 [I/O 要求の完了](completing-i-o-requests.md)します。

 

 





