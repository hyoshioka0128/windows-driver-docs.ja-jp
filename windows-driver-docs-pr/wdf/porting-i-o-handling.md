---
title: I/O の移植
description: I/O の移植
ms.assetid: D65B85C4-401F-4143-9626-5C16E24925A0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a991b3a73d9014e3214c5409869973c238a3de43
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552268"
---
# <a name="porting-io"></a>I/O の移植


KMDF ドライバーでは、1 つまたは複数のキューの作成し、各キューに 1 つまたは複数の I/O イベント コールバック関数を関連付けることによって I/O 要求を処理します。 WDM ドライバーの I/O の処理が KMDF にコードを移植するには。

-   [ポートの I/O キュー](creating-i-o-queues.md)します。

-   [ポートの I/O ディスパッチ ルーチン](porting-i-o-dispatch-routines-to-i-o-event-callback-functions.md)I/O イベント コールバックにします。

-   [改訂コードを処理する要求を完了した](revise-completed-request-logic.md)します。

-   [取り消された要求のロジックを改訂](revise-canceled-request-logic.md)します。

-   [要求を転送するロジックを改訂](revise-forward-request-logic.md)します。

-   [I/O 要求を発行するコードの修正](revise-code-that-issues-i-o-requests.md)します。

 

 





