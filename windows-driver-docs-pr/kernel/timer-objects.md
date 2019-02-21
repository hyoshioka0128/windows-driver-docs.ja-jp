---
title: タイマー オブジェクト
description: すべてのドライバーは、タイマーを使用できます、ドライバーでの操作のタイムアウトを nonarbitrary スレッド コンテキスト内でオブジェクトの他のルーチンでは、操作を定期的に実行をスケジュールしたりできます。
ms.assetid: A4844F19-3BEC-48C0-A5BF-E17CCEEC1601
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5eef0b3ec915c14f85488b3f0a84710ed9febaec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531136"
---
# <a name="timer-objects"></a>タイマー オブジェクト


すべてのドライバーは、タイマーを使用できます、ドライバーでの操作のタイムアウトを nonarbitrary スレッド コンテキスト内でオブジェクトの他のルーチンでは、操作を定期的に実行をスケジュールしたりできます。 Windows 2000 以降、タイマー オブジェクトに基づいて、 [ **KTIMER** ](https://msdn.microsoft.com/library/windows/hardware/ff554250)構造体がで使用できる[ **KeSetTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff553286)と、その他**Ke*Xxx*タイマー**ルーチン。 Windows 8.1 以降、タイマー オブジェクトに基づいて、 [ **EX\_タイマー** ](https://msdn.microsoft.com/library/windows/hardware/dn265199)構造体がで使用できる[ **ExSetTimer** ](https://msdn.microsoft.com/library/windows/hardware/dn265188)と、その他の**Ex*Xxx*タイマー**ルーチン。 タイマー オブジェクトをベースに、 **KTIMER**と**EX\_タイマー**構造体が[カーネルのディスパッチャー オブジェクト](kernel-dispatcher-objects.md)タイマーの期限が切れたときはシグナル状態です。 タイマーの有効期限は、定期的または 1 回限り (非連続)。

このセクションには、次のトピックが含まれています。

-   [KTIMER オブジェクト、および Dpc を KeXxxTimer ルーチン](timer-objects-and-dpcs.md)

-   [ExXxxTimer ルーチンと EX\_タイマー オブジェクト](exxxxtimer-routines-and-ex-timer-objects.md)

 

 




