---
title: SynchCritSection ルーチンの記述
description: SynchCritSection ルーチンの記述
ms.assetid: b02e230e-48f1-43dc-b5aa-368cd7b5436f
keywords:
- SynchCritSection
- クリティカル セクション ルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a932d1ec623a57ed0b52cc9485c2f43697598a2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580287"
---
# <a name="writing-synchcritsection-routines"></a>SynchCritSection ルーチンの記述





ドライバーを使用して、 [ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928) 2 つの基本的な目的のいずれかのルーチン。

[I/O 操作のデバイスのプログラミング](programming-a-device-for-an-i-o-operation.md)

[共有状態の情報にアクセスします。](accessing-shared-state-information.md)

などの ISR、 *SynchCritSection*ルーチンは、デバイス登録の設定または返す前にコンテキストのデータの更新に必要なだけ何が可能な限り早く実行する必要があります。

[ **KeSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff553302)中にデバイス ドライバーの割り込みスピン ロックを保持してその*SynchCritSection*まで、ドライバーの ISR ルーチンの実行を実行できません、*SynchCritSection*ルーチンは、コントロールを返します。

IRP を受信したすべてのデバイス ドライバを行う必要がありますできるだけ多くの I/O 処理のいずれかで IRQL パッシブ\_そのディスパッチ ルーチン内のレベル (または場合によって[デバイス専用のスレッド](device-dedicated-threads.md))、または IRQL ディスパッチ\_レベルにその[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチンと DPC ルーチン。

クリティカル セクションの同期方法の詳細についてを参照してください[ロックを使用して迅速に作成します。たとえば](using-spin-locks--an-example.md)します。

 

 




