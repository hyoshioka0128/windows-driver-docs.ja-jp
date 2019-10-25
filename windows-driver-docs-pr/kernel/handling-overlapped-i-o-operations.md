---
title: 重複した I/O 操作の処理
description: 重複した I/O 操作の処理
ms.assetid: d13a9fa2-9f68-4c35-af79-dd3f8cec2805
keywords:
- 遅延プロシージャ呼び出し WDK カーネル
- Dpc WDK カーネル
- DpcForIsr
- CustomDpc
- 重複 i/o WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0472de766928ce711d81b98c2731281621e4c2df
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838658"
---
# <a name="handling-overlapped-io-operations"></a>重複した I/O 操作の処理





デバイス上で操作が重複するドライバーの[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)または[*customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンは、 [*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンへの要求入力と、ISR による[**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc) [**への呼び出しの間に1対1の対応に依存することはできません。KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)。 このようなドライバーの*DpcForIsr*または*customdpc*は、必ずしも irp および ISR によって提供されるコンテキストへの入力ポインター、またはターゲットデバイスオブジェクトの中**entirp**ポインターを使用して、その irp だけを完了することはできません。

特定の時点で、同じ DPC オブジェクトを2回キューに入れることはできません。 ISR が**IoRequestDpc**または**KeInsertQueueDpc**を2回以上呼び出す前に、対応する*DpcForIsr*または*customdpc*を実行すると、プロセッサの IRQL がディスパッチ\_レベルを下回ると、DPC ルーチンは1回だけ実行されます。 一方、ISR が**IoRequestDpc**または**KeInsertQueueDpc**を呼び出し、対応する*DpcForIsr*または*customdpc*が別のプロセッサで実行されている場合、DPC ルーチンは2つのプロセッサで同時に実行できます。

そのため、デバイス上の割り込みドリブン i/o 操作と重複するドライバーには、次のものが必要です。

-   *DpcForIsr*または*customdpc*ルーチン。呼び出されるたびに、ドライバーによって保持される未処理の要求の数を完了できます。

-   *DpcForIsr*または*customdpc*ルーチンに渡すコンテキスト情報を、ルーチンがコンテキスト情報を使用し、コンテキスト情報が属する IRP を完了するまで上書きしない ISR。

-   *DpcForIsr*または*customdpc*ルーチンの代わりに ISR のコンテキスト領域にアクセスする*SynchCritSection*ルーチン

 

 




