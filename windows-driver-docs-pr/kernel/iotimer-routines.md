---
title: IoTimer ルーチン
description: IoTimer ルーチン
ms.assetid: bc69c7b5-ce63-435e-b5b4-0d65ee153d31
keywords:
- 同期の WDK カーネル、タイマー
- IoTimer
- デバイスのタイムアウトの WDK カーネル
- タイムアウトの WDK カーネル
- タイミング操作 WDK カーネル
- タイムアウトのデバイスの I/O 操作の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4b3f1c9d838d7a7b0d1c143301a30c2fc56c906
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381676"
---
# <a name="iotimer-routines"></a>IoTimer ルーチン





判断 (カウンター) などのドライバーの定義の変数を更新するか、どの短い時間の間隔で必須ではありませんすべての操作にかかる時間をデバイスの操作がタイムアウトしてかどうかに、定期的に呼び出される必要のあるドライバーを使用できます、 [ *IoTimer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_timer_routine)ルーチン。 *IoTimer*ルーチンは、DPC ルーチンでは実際には、I/O マネージャーが 1 秒あたり 1 回呼び出し、デバイス オブジェクトに関連付けられています。 ドライバーが持つことができます、 *IoTimer*ルーチンが作成する各デバイス オブジェクトにします。

一般に、ドライバーを使用する必要があります、 *IoTimer*ルーチンを 1 秒間の一定の間隔を必要とする時の操作をします。 変数を必要とする時の操作を間隔または毎秒 1 回よりも短い間隔では、ドライバーは、タイマー オブジェクトを割り当てる必要があります。 詳細については、次を参照してください。[タイマー オブジェクトと Dpc](timer-objects-and-dpcs.md)します。

このセクションでは、次のトピックについて説明します。

[登録して、IoTimer ルーチンを有効にします。](registering-and-enabling-an-iotimer-routine.md)

[IoTimer コンテキスト情報を提供します。](providing-iotimer-context-information.md)

[IoTimer ルーチンを使用します。](using-an-iotimer-routine.md)

 

 




