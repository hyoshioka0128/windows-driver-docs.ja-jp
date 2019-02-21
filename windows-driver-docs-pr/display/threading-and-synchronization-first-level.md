---
title: スレッド処理との同期の最初のレベル
description: スレッド処理との同期の最初のレベル
ms.assetid: 9fce6a18-2a66-4518-b05b-e85bdaa3951f
keywords:
- WDK の表示をスレッドには、最初のステージします。
- 同期の WDK の表示、最初のレベル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac8e9c989ca46fcfd84b15c3ec2e414bdd6f63eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538660"
---
# <a name="threading-and-synchronization-first-level"></a>スレッド処理との同期の最初のレベル


Windows 表示 Driver Model (WDDM) は、スレッド処理の最初のレベルで行われたディスプレイのミニポート ドライバーへの呼び出しと nonreentrancy クラスを次に同期を分類します。 特定のクラス内で再入が許可されていません。 つまり、1 つのスレッドが、特定のクラス内のドライバーを入力できます。ただし、複数のクラスからの呼び出しと[0 レベル](threading-and-synchronization-zero-level.md)呼び出しを同時に入力することができます。

**注**  が 2 つ以上の異なるクラスからのスレッドし、スレッドから[0 レベル](threading-and-synchronization-zero-level.md)と同時に、ドライバーでの呼び出しを実行できる、2 つのスレッドが 1 つのプロセスに属することができます。

 

**注**  子 I/O クラスの関数が子デバイス (つまり、同時呼び出しを複数の子デバイスが許可されます) ごとに同期されます。 ただし、子デバイス間で内部の依存関係が存在しない場合、ディスプレイのミニポート ドライバーは必要に応じて呼び出しをブロックする必要があります。

 

-   [ポインター クラス](pointer-class.md)

-   [GPU Scheduler クラス](gpu-scheduler-class.md)

-   [スウィズ リング範囲クラス](swizzling-range-class.md)

-   [オーバーレイ クラス](overlay-class.md)

-   [子 I/O クラス](child-i-o-class.md)

-   [クラスを表示します。](display-class.md)

 





