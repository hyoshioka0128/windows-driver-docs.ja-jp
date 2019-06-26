---
title: 重複した I/O 操作の処理
description: 重複した I/O 操作の処理
ms.assetid: d13a9fa2-9f68-4c35-af79-dd3f8cec2805
keywords:
- 遅延プロシージャ呼び出しの WDK カーネル
- Dpc WDK カーネル
- DpcForIsr
- CustomDpc
- オーバー ラップ I/O WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d8899a618b7bc75f4b9f39a831505b286236c22
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375224"
---
# <a name="handling-overlapped-io-operations"></a>重複した I/O 操作の処理





[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)または[ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)一対一のデバイス上での操作と重複するドライバーのルーチンは使用できません入力要求の間の通信、 [ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチンと ISR の呼び出しを[ **IoRequestDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iorequestdpc)または[ **KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertqueuedpc)します。 このようなドライバーの*DpcForIsr*または*CustomDpc* IRP を ISR によって提供されるコンテキストでは、入力ポインターを使用することはできませんとは限りませんまたは**CurrentIrp**ターゲット内のポインターデバイス オブジェクト、その IRP のみを完了します。

特定の時点では、同じ DPC オブジェクトを 2 回繰り返すことはできません。 ISR を呼び出す場合**IoRequestDpc**または**KeInsertQueueDpc** 、対応する前に 2 回以上*DpcForIsr*または*CustomDpc*を実行します、プロセッサの IRQL がディスパッチを下回ったときに 1 回だけ、DPC ルーチンが実行される\_レベル。 その一方、ISR から呼び出す場合**IoRequestDpc**または**KeInsertQueueDpc** 、対応するときに*DpcForIsr*または*CustomDpc*は別のプロセッサで実行されている、DPC ルーチン 2 つのプロセッサで同時に実行できます。

そのため、そのデバイス上の I/O 操作の割り込み駆動と重複するドライバーは、次が必要です。

-   A *DpcForIsr*または*CustomDpc*ルーチンの一部を実行できるドライバーで維持されるたびに未処理の要求の数が呼び出されます

-   渡されるコンテキスト情報が上書きされない ISR、 *DpcForIsr*または*CustomDpc*ルーチン、そのルーチンがコンテキスト情報を使用し、する IRP を完了するまで、コンテキスト情報が属しています。

-   A *SynchCritSection*ルーチンの代わりに、ISR コンテキストの領域にアクセスする、 *DpcForIsr*または*CustomDpc*ルーチン

 

 




