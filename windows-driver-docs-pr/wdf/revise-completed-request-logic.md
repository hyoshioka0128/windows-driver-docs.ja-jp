---
title: ハンドルが要求を完了しているコードを修正します。
description: ハンドルが要求を完了しているコードを修正します。
ms.assetid: 0DD48424-A728-4887-9F26-46B7004CB12C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f73fadbd243ff0361b558d66ceab1176220cb4c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530091"
---
# <a name="revise-code-that-handles-completed-requests"></a>ハンドルが要求を完了しているコードを修正します。


Windows Driver Frameworks (WDF) は、I/O 要求を完了する 3 つのメソッドを提供します。

-   [**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
-   [**WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)
-   [**WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949) (KMDF のみ)

これらのメソッドの使用方法の詳細については、次を参照してください。 [I/O 要求の完了](completing-i-o-requests.md)します。

 

 





