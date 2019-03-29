---
title: C28648
description: 警告 C28648 PulseEvent は、信頼性の低い関数です。
ms.assetid: 6132e35c-f1ae-44cc-9a6c-b61d6e7f8c57
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28648
ms.openlocfilehash: 3d171485cf2515030799d95b466c4f73d2831be5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572595"
---
# <a name="c28648"></a>C28648


C28648 を警告します。PulseEvent は信頼性のない関数です。

同期オブジェクトで待機しているスレッドを一時的に、カーネル モード APC が待機状態から削除し、APC が完了したら待機状態に返されます。 場合に呼び出し**PulseEvent**が発生した期間中は、スレッドが待機状態から削除されたときに、スレッドは解放されません、「ハング」永久にします。 これは、ため**PulseEvent**呼び出された時点で待機しているスレッドのみを解放します。

使用を修正する方法のいくつか**PulseEvent**:

-   のみが解放される必要があるイベントで待機するスレッドの 1 ついて、イベントは、手動リセット イベント、変更、自動リセット イベントと呼び出しに**SetEvent**の代わりに**PulseEvent**します。

-   リリースする必要があるイベントで待機するスレッドの 1 つ、イベントは、自動リセット イベントの呼び出しのみが**SetEvent**の代わりに**PulseEvent**します。

-   場合は、イベントを待機しているすべてのスレッドを解放する必要が、イベントは、手動リセット イベント、同期オブジェクト (セマフォ) などのさまざまな種類を使用するコードを再設計します。

-   イベントを待機しているすべてのスレッドを解放する必要があるいて、イベントは、自動リセット イベント、呼び出し**SetEvent**の代わりに**PulseEvent** (、元の呼び出し**PulseEvent**スレッドを解放 1 つだけです)。

 

 





