---
title: タイマー オブジェクト
description: すべてのドライバーは、タイマーを使用できます、ドライバーでの操作のタイムアウトを nonarbitrary スレッド コンテキスト内でオブジェクトの他のルーチンでは、操作を定期的に実行をスケジュールしたりできます。
ms.assetid: A4844F19-3BEC-48C0-A5BF-E17CCEEC1601
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0d96b63cdf5d312a7edc0a760ee5d3a7dde09a85
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382958"
---
# <a name="timer-objects"></a>タイマー オブジェクト


すべてのドライバーは、タイマーを使用できます、ドライバーでの操作のタイムアウトを nonarbitrary スレッド コンテキスト内でオブジェクトの他のルーチンでは、操作を定期的に実行をスケジュールしたりできます。 Windows 2000 以降、タイマー オブジェクトに基づいて、 [ **KTIMER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体がで使用できる[ **KeSetTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettimer)と、その他**Ke*Xxx*タイマー**ルーチン。 Windows 8.1 以降、タイマー オブジェクトに基づいて、 [ **EX\_タイマー** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体がで使用できる[ **ExSetTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exsettimer)と、その他の**Ex*Xxx*タイマー**ルーチン。 タイマー オブジェクトをベースに、 **KTIMER**と**EX\_タイマー**構造体が[カーネルのディスパッチャー オブジェクト](kernel-dispatcher-objects.md)タイマーの期限が切れたときはシグナル状態です。 タイマーの有効期限は、定期的または 1 回限り (非連続)。

このセクションでは、次のトピックについて説明します。

-   [KTIMER オブジェクト、および Dpc を KeXxxTimer ルーチン](timer-objects-and-dpcs.md)

-   [ExXxxTimer ルーチンと EX\_タイマー オブジェクト](exxxxtimer-routines-and-ex-timer-objects.md)

 

 




