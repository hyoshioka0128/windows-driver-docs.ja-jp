---
title: SynchCritSection ルーチンの概要
description: SynchCritSection ルーチンの概要
ms.assetid: 747f314a-9c7c-427f-bc23-4c6869853852
keywords:
- SynchCritSection
- クリティカル セクション ルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 613adf65a581022ea20557ae465b85f40c4b55d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386587"
---
# <a name="introduction-to-synchcritsection-routines"></a>SynchCritSection ルーチンの概要





*クリティカル セクション*はハードウェア リソースまたはドライバーのデータへの排他アクセスを必要とするコードのセクションです。 同じリソースまたはデータを参照できる他のコードによって、コードが中断しない、リソースまたはデータする必要がありますいない参照は、複数のプロセッサによって一度に。

重要なセクションは、Isr に限定する必要がありますと*SynchCritSection*値とスピン ロックを取得します。 後に、 *SynchCritSection*ルーチンを返します、システムは、スピン ロックを解放して、プロセッサの IRQL が低くなります。

デバイスの DIRQL 値に、プロセッサの IRQL を発生させると、現在のプロセッサが中断されるできなく優先順位の高いデバイスを除きます。 スピン ロックを取得すると、他のプロセッサはそのスピン ロックに関連付けられている、クリティカル セクションのコードを実行できなくなります。 (このスピン ロックとも呼ばれます、*スピン ロックを中断*)。

デバイス ドライバーの[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)と[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)または[ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)ルーチン頻繁にする必要がありますの一部にアクセス同じ[ハードウェア リソース](hardware-resources.md)(デバイスの登録やその他のバスの相対メモリ) またはドライバーの ISR. としてドライバーが保持するデータ ドライバーのデバイスまたはそのディスパッチ、設計に応じて[ *AdapterControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control)、 [ *ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)、またはタイマーのルーチンもハードウェア リソースまたはドライバーが保持するデータにアクセスします。

任意の非 ISR クリティカル セクションを呼び出すには、ドライバーを使用する必要があります、 [ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)ルーチン。 このルーチンのアドレスを受け入れる、 *SynchCritSection*ドライバー定義のコンテキスト情報と共に、入力と割り込みオブジェクト ポインターとルーチン。 システムで使用する DIRQL、スピン ロックを判断する割り込みオブジェクトへのポインターを使用して、 *SynchCritSection*ルーチン。 (ドライバーを使用して、これらの値を指定、 [ **IoConnectInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterrupt)関数の*スピンロック*と*SynchronizeIrql*パラメーター。)

 

 




