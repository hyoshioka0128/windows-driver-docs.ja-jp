---
title: SynchCritSection ルーチンの概要
description: SynchCritSection ルーチンの概要
ms.assetid: 747f314a-9c7c-427f-bc23-4c6869853852
keywords:
- SynchCritSection
- クリティカル セクション ルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c7e02b17f51039231c2a986978e1e26983590f5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327236"
---
# <a name="introduction-to-synchcritsection-routines"></a>SynchCritSection ルーチンの概要





*クリティカル セクション*はハードウェア リソースまたはドライバーのデータへの排他アクセスを必要とするコードのセクションです。 同じリソースまたはデータを参照できる他のコードによって、コードが中断しない、リソースまたはデータする必要がありますいない参照は、複数のプロセッサによって一度に。

重要なセクションは、Isr に限定する必要がありますと*SynchCritSection*値とスピン ロックを取得します。 後に、 *SynchCritSection*ルーチンを返します、システムは、スピン ロックを解放して、プロセッサの IRQL が低くなります。

デバイスの DIRQL 値に、プロセッサの IRQL を発生させると、現在のプロセッサが中断されるできなく優先順位の高いデバイスを除きます。 スピン ロックを取得すると、他のプロセッサはそのスピン ロックに関連付けられている、クリティカル セクションのコードを実行できなくなります。 (このスピン ロックとも呼ばれます、*スピン ロックを中断*)。

デバイス ドライバーの[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)と[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)または[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)ルーチン頻繁にする必要がありますの一部にアクセス同じ[ハードウェア リソース](hardware-resources.md)(デバイスの登録やその他のバスの相対メモリ) またはドライバーの ISR. としてドライバーが保持するデータ ドライバーのデバイスまたはそのディスパッチ、設計に応じて[ *AdapterControl*](https://msdn.microsoft.com/library/windows/hardware/ff540504)、 [ *ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)、またはタイマーのルーチンもハードウェア リソースまたはドライバーが保持するデータにアクセスします。

任意の非 ISR クリティカル セクションを呼び出すには、ドライバーを使用する必要があります、 [ **KeSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff553302)ルーチン。 このルーチンのアドレスを受け入れる、 *SynchCritSection*ドライバー定義のコンテキスト情報と共に、入力と割り込みオブジェクト ポインターとルーチン。 システムで使用する DIRQL、スピン ロックを判断する割り込みオブジェクトへのポインターを使用して、 *SynchCritSection*ルーチン。 (ドライバーを使用して、これらの値を指定、 [ **IoConnectInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff548371)関数の*スピンロック*と*SynchronizeIrql*パラメーター。)

 

 




