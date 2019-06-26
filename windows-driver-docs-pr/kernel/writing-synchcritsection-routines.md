---
title: SynchCritSection ルーチンの記述
description: SynchCritSection ルーチンの記述
ms.assetid: b02e230e-48f1-43dc-b5aa-368cd7b5436f
keywords:
- SynchCritSection
- クリティカル セクション ルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0599e3160188c8f9267132e5afe916c6447d7fe5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374106"
---
# <a name="writing-synchcritsection-routines"></a>SynchCritSection ルーチンの記述





ドライバーを使用して、 [ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine) 2 つの基本的な目的のいずれかのルーチン。

[I/O 操作のデバイスのプログラミング](programming-a-device-for-an-i-o-operation.md)

[共有状態の情報にアクセスします。](accessing-shared-state-information.md)

などの ISR、 *SynchCritSection*ルーチンは、デバイス登録の設定または返す前にコンテキストのデータの更新に必要なだけ何が可能な限り早く実行する必要があります。

[ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)中にデバイス ドライバーの割り込みスピン ロックを保持してその*SynchCritSection*まで、ドライバーの ISR ルーチンの実行を実行できません、*SynchCritSection*ルーチンは、コントロールを返します。

IRP を受信したすべてのデバイス ドライバを行う必要がありますできるだけ多くの I/O 処理のいずれかで IRQL パッシブ\_そのディスパッチ ルーチン内のレベル (または場合によって[デバイス専用のスレッド](device-dedicated-threads.md))、または IRQL ディスパッチ\_レベルにその[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチンと DPC ルーチン。

クリティカル セクションの同期方法の詳細についてを参照してください[ロックを使用して迅速に作成します。たとえば](using-spin-locks--an-example.md)します。

 

 




