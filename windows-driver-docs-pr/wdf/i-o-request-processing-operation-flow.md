---
title: I/O 要求処理の操作フロー
description: I/O 要求処理の操作フロー
ms.assetid: 3a7162d2-0a8c-4748-b320-bfe64ec93c9d
keywords:
- 操作フロー WDK UMDF
- I/o 要求 WDK UMDF、操作フロー
- 要求の処理 WDK UMDF、操作フロー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6bc896e4aa505a703345e375290d461bac2b349
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209894"
---
# <a name="io-request-processing-operation-flow"></a>I/O 要求処理の操作フロー


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

すべての i/o 操作は、ファイルオブジェクトのコンテキストで実行されます (つまり、アプリケーションが Microsoft Win32 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)および**CloseHandle**関数に対して行った呼び出しの間ですべての i/o 操作が行われます)。 I/o 操作は、Win32 の**ReadFileEx**、**た writefileex**、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)などの関数に対してアプリケーションが行う呼び出しです。

次のトピックでは、ユーザー i/o トランザクションが開始、処理し、1つのデバイススタックとダブルデバイススタックで終了する際に、UMDF ドライバーとの間で発生する操作の流れを示します。

-   [1つのデバイススタックを持つ操作フロー](operation-flow-with-single-device-stack.md)

-   [デバイススタックがダブルの操作フロー](operation-flow-with-double-device-stack.md)

**注  :** アプリケーションによって開始されるすべての i/o は、「I/o 要求処理操作フロー」セクションの図に示されているように、カーネルモードによってルーティングされます。ただし、「I/o Request Processing Operation Flow [」セクションの](https://docs.microsoft.com/previous-versions/ff554461(v=vs.85))図には、このような状況は表示されません。

 

 

 





