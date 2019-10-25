---
title: SynchCritSection ルーチンの記述
description: SynchCritSection ルーチンの記述
ms.assetid: b02e230e-48f1-43dc-b5aa-368cd7b5436f
keywords:
- SynchCritSection
- クリティカルセクションルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8b6ddf7ac5b9c4808db7d06dd3a375ff3cfdaab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838291"
---
# <a name="writing-synchcritsection-routines"></a>SynchCritSection ルーチンの記述





ドライバーは、次の2つの基本的な目的のいずれかで、 [*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンを使用します。

[I/o 操作用のデバイスのプログラミング](programming-a-device-for-an-i-o-operation.md)

[共有状態情報へのアクセス](accessing-shared-state-information.md)

ISR と同様に、 *SynchCritSection*ルーチンはできるだけ迅速に実行する必要があります。これを行うには、デバイスレジスタを設定したり、コンテキストデータを更新してから制御を戻す必要があります。

[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)は*SynchCritSection*ルーチンの実行中にデバイスドライバーの割り込みスピンロックを保持するため、 *SynchCritSection*ルーチンから制御が返されるまで、ドライバーの ISR は実行できません。

受信した IRP の場合、デバイスドライバーは、ディスパッチルーチン (または[デバイス専用スレッド](device-dedicated-threads.md)) の irql パッシブ\_レベル、または[*STARTIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンの irql ディスパッチ\_レベルのいずれかで、可能な限り多くの i/o 処理を実行する必要があります。および DPC ルーチン。

クリティカルセクションの同期方法の詳細については、「[スピンロックの使用: 例](using-spin-locks--an-example.md)」を参照してください。

 

 




