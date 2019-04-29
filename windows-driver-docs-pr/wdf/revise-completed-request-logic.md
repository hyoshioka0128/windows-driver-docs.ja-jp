---
title: 完了した要求を処理するコードを修正する
description: 完了した要求を処理するコードを修正する
ms.assetid: 0DD48424-A728-4887-9F26-46B7004CB12C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f73fadbd243ff0361b558d66ceab1176220cb4c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325165"
---
# <a name="revise-code-that-handles-completed-requests"></a>完了した要求を処理するコードを修正する


Windows Driver Frameworks (WDF) は、I/O 要求を完了する 3 つのメソッドを提供します。

-   [**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
-   [**WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)
-   [**WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949) (KMDF のみ)

これらのメソッドの使用方法の詳細については、次を参照してください。 [I/O 要求の完了](completing-i-o-requests.md)します。

 

 





