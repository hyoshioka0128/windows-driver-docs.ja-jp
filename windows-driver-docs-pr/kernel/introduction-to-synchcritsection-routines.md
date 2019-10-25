---
title: SynchCritSection ルーチンの概要
description: SynchCritSection ルーチンの概要
ms.assetid: 747f314a-9c7c-427f-bc23-4c6869853852
keywords:
- SynchCritSection
- クリティカルセクションルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52d4573b09243f378b9eb5f6c159404fabcd9708
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838620"
---
# <a name="introduction-to-synchcritsection-routines"></a>SynchCritSection ルーチンの概要





*クリティカルセクション*は、ハードウェアリソースまたはドライバーデータへの排他アクセスを必要とするコードのセクションです。 つまり、同じリソースまたはデータを参照できる他のコードによってコードが中断されることはなく、リソースやデータを一度に複数のプロセッサが参照することはできません。

重要なセクションは、Isr と*SynchCritSection*の値に限定し、スピンロックを取得する必要があります。 *SynchCritSection*ルーチンが戻ると、スピンロックが解放され、プロセッサの IRQL が低下します。

デバイスの DIRQL 値に対してプロセッサの IRQL を上げると、優先順位の高いデバイスを除き、現在のプロセッサが中断されるのを防ぐことができます。 スピンロックを取得すると、そのスピンロックに関連付けられた重要なセクションコードが他のプロセッサによって実行されるのを防ぐことができます。 (このスピンロックは、*割り込みスピンロック*と呼ばれることもあります)。

デバイスドライバーの[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)と[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)または[*customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンは、多くの場合、同じ[ハードウェアリソース](hardware-resources.md)の一部 (デバイスレジスタやその他のバス相対メモリなど) にアクセスする必要があります。または、ドライバーで保持されるデータをドライバーのISR. ドライバーのデバイスまたは設計によっては、ディスパッチ、 [*Adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)、[*コントローラー制御*](https://msdn.microsoft.com/library/windows/hardware/ff542049)、またはタイマールーチンも、ハードウェアリソースまたはドライバーによって管理されるデータにアクセスする場合があります。

ISR 以外の重要なセクションを呼び出すには、ドライバーで[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)ルーチンを使用する必要があります。 このルーチンは、ドライバー定義のコンテキスト情報と割り込みオブジェクトポインターと共に、 *SynchCritSection*ルーチンのアドレスを入力として受け取ります。 システムは、interrupt オブジェクトポインターを使用して、 *SynchCritSection*ルーチンで使用する dirql とスピンロックを決定します。 (ドライバーは、 [**Ioconnectinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)関数の*スピンロック*と*SynchronizeIrql*パラメーターを使用して、これらの値を以前に指定しています)。

 

 




