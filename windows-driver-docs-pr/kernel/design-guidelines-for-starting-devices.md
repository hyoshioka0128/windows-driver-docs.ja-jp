---
title: デバイスの開始に関する設計ガイドライン
description: デバイスの開始に関する設計ガイドライン
ms.assetid: fbdde107-f3a5-4713-a4ac-1c9bafa3c634
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 429e61e8ecd9b7ff172d60efed4c8765fa38a081
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836942"
---
# <a name="design-guidelines-for-starting-devices"></a>デバイスの開始に関する設計ガイドライン





-   PnP マネージャーがデバイスの要求の作成に失敗するのは、 [**irp\_が\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)の irp が完了し、デバイスのすべてのドライバーが開始操作を実行したことを示します。

-   [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、IRQL パッシブ\_レベルのシステムスレッドのコンテキストで実行されるため、初期化時にのみ使用するために[**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)で割り当てられたメモリは、ドライバーがページプールを使用しない限り、システムページファイルを保持するデバイスを制御します。 このようなメモリ割り当ては、 *DispatchPnP*ルーチンが制御を返す前に、 [**exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)を使用して解放する必要があります。

-   WDM デバイスドライバーの ISR は、デバイスの起動時に、擬似的な割り込みで呼び出されたかどうかを判断できる必要があります。 デバイスで割り込みが有効になっている場合に **\_デバイスで IRP の\_\_が実行**されたときに、IRP がすぐに呼び出されるようにするコードパスでの[**ioconnectinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)呼び出しから制御が戻ったときに、ISR を直ちに呼び出すことができます。

 

 




