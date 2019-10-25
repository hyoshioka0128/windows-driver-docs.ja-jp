---
title: 完了した要求を処理するコードを修正する
description: 完了した要求を処理するコードを修正する
ms.assetid: 0DD48424-A728-4887-9F26-46B7004CB12C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ddcc18ccbd5f1806f9b2677f3189abd5f4bad32
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842200"
---
# <a name="revise-code-that-handles-completed-requests"></a>完了した要求を処理するコードを修正する


Windows ドライバーフレームワーク (WDF) には、i/o 要求を完了するための3つの方法が用意されています。

-   [**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)
-   [**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)
-   [**Wdfrequestcompletewithの優先順位ブースト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)(kmdf のみ)

これらのメソッドの使用方法の詳細については、「 [I/o 要求の完了](completing-i-o-requests.md)」を参照してください。

 

 





