---
title: I/O 要求処理の操作フロー
description: I/O 要求処理の操作フロー
ms.assetid: 3a7162d2-0a8c-4748-b320-bfe64ec93c9d
keywords:
- 操作フロー WDK UMDF
- I/O 要求の WDK UMDF、操作フロー
- 要求の WDK UMDF、操作のフローの処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79377468a59511c59a79c3069ea1a49974e21b15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538325"
---
# <a name="io-request-processing-operation-flow"></a>I/O 要求処理の操作フロー


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ファイル オブジェクトのコンテキストで発生するすべての I/O 操作 (つまり、すべての I/O 操作はアプリケーションによる Microsoft Win32 呼び出しを間に発生[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)と**CloseHandle**関数)。 I/O 操作は、アプリケーションには、Win32 などを行う呼び出し**ReadFileEx**、 **WriteFileEx**、および[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)関数。

次のトピックと行われる UMDF ドライバーとの間ユーザー I/O トランザクション、プロセスを開始します。 1 つのデバイス スタックと double デバイス スタックを終了する操作の流れを示しています。

-   [スタックの 1 つのデバイスでの操作フロー](operation-flow-with-single-device-stack.md)

-   [二重デバイス スタックでの操作フロー](operation-flow-with-double-device-stack.md)

**注**  の図に示すように、カーネル モードでアプリケーションによって開始されるすべての I/O がルーティングされます、 [、UMDF のアーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/ff554461)セクション場合でも、I/O 要求処理の図操作フローのセクションでは、このような状況は表示されません。

 

 

 





