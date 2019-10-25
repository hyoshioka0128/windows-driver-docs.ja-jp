---
title: IoTimer ルーチン
description: IoTimer ルーチン
ms.assetid: bc69c7b5-ce63-435e-b5b4-0d65ee153d31
keywords:
- 同期 WDK カーネル、タイマー
- IoTimer
- デバイスのタイムアウト WDK カーネル
- タイムアウト WDK カーネル
- タイミング操作の WDK カーネル
- デバイス i/o 操作のタイムアウト (WDK カーネル)
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4aa68224a0af2a5c1e0600a445e36c8540bcac57
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828157"
---
# <a name="iotimer-routines"></a>IoTimer ルーチン





デバイスの操作がタイムアウトしたかどうかを判断したり、ドライバーで定義された変数 (カウンターなど) を更新したり、小さな時間間隔が不要な操作を実行したりするために、 [*Iotimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)ルーチンを使用できるようにするために定期的に呼び出す必要があるドライバー。 *Iotimer*ルーチンは、実際にはデバイスオブジェクトに関連付けられている DPC ルーチンで、i/o マネージャーは1秒間に1回呼び出します。 ドライバーは、作成するデバイスオブジェクトごとに*Iotimer*ルーチンを持つことができます。

一般に、ドライバーでは、通常の1秒間隔を必要とする時間操作に*Iotimer*ルーチンを使用する必要があります。 1秒間に1回の間隔または間隔を短縮する必要がある時間操作には、ドライバーがタイマーオブジェクトを割り当てる必要があります。 詳細については、「 [Timer オブジェクトと dpc](timer-objects-and-dpcs.md)」を参照してください。

このセクションでは、次のトピックについて説明します。

[IoTimer ルーチンの登録と有効化](registering-and-enabling-an-iotimer-routine.md)

[IoTimer コンテキスト情報の提供](providing-iotimer-context-information.md)

[IoTimer ルーチンの使用](using-an-iotimer-routine.md)

 

 




