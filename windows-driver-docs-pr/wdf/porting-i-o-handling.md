---
title: I/O の移植
description: I/O の移植
ms.assetid: D65B85C4-401F-4143-9626-5C16E24925A0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a991b3a73d9014e3214c5409869973c238a3de43
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390097"
---
# <a name="porting-io"></a>I/O の移植


KMDF ドライバーでは、1 つまたは複数のキューの作成し、各キューに 1 つまたは複数の I/O イベント コールバック関数を関連付けることによって I/O 要求を処理します。 WDM ドライバーの I/O の処理が KMDF にコードを移植するには。

-   [ポートの I/O キュー](creating-i-o-queues.md)します。

-   [ポートの I/O ディスパッチ ルーチン](porting-i-o-dispatch-routines-to-i-o-event-callback-functions.md)I/O イベント コールバックにします。

-   [改訂コードを処理する要求を完了した](revise-completed-request-logic.md)します。

-   [取り消された要求のロジックを改訂](revise-canceled-request-logic.md)します。

-   [要求を転送するロジックを改訂](revise-forward-request-logic.md)します。

-   [I/O 要求を発行するコードの修正](revise-code-that-issues-i-o-requests.md)します。

 

 





