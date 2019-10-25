---
title: タイマー オブジェクト
description: 任意のドライバーは、任意のスレッドコンテキスト内のタイマーオブジェクトを使用して、ドライバーのその他のルーチンのタイムアウト操作を実行したり、定期的に実行される操作をスケジュールしたりすることができます。
ms.assetid: A4844F19-3BEC-48C0-A5BF-E17CCEEC1601
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2b7b9bfa2d8fe9503d1c96a46d0df0b5e5a78d42
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836117"
---
# <a name="timer-objects"></a>タイマー オブジェクト


任意のドライバーは、任意のスレッドコンテキスト内のタイマーオブジェクトを使用して、ドライバーのその他のルーチンのタイムアウト操作を実行したり、定期的に実行される操作をスケジュールしたりすることができます。 Windows 2000 以降では、 [**Ktimer**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造に基づくタイマーオブジェクトを[**KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer)およびその他の**Ke*Xxx*タイマー**ルーチンと共に使用できます。 Windows 8.1 以降では、 [**ex\_timer**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造に基づくタイマーオブジェクトを、 [**ExSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimer)およびその他の**ex*Xxx*タイマー**ルーチンで使用できます。 **Ktimer**および**EX\_timer**構造に基づくタイマーオブジェクトは、タイマーの有効期限が切れたときに通知される[カーネルディスパッチャーオブジェクト](kernel-dispatcher-objects.md)です。 タイマーの有効期限は、周期的またはワンショット (定期的ではない) にすることができます。

このセクションでは、次のトピックについて説明します。

-   [KeXxxTimer ルーチン、KTIMER オブジェクト、および Dpc](timer-objects-and-dpcs.md)

-   [Exxxx Timer ルーチンおよび EX\_TIMER オブジェクト](exxxxtimer-routines-and-ex-timer-objects.md)

 

 




