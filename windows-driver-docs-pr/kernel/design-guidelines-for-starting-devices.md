---
title: デバイスの開始に関する設計ガイドライン
description: デバイスの開始に関する設計ガイドライン
ms.assetid: fbdde107-f3a5-4713-a4ac-1c9bafa3c634
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c17ccdc84c49db59cd4024171ad4b8f8da88b83f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377089"
---
# <a name="design-guidelines-for-starting-devices"></a>デバイスの開始に関する設計ガイドライン





-   PnP マネージャーが失敗するまで、デバイスの要求の作成、 [ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device) IRP が完了したことを示すデバイスのすべてのドライバー開始操作を実行しています。

-   [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch) IRQL パッシブにシステム スレッドのコンテキストで実行されるルーチン\_レベルでメモリが割り当てられた[ **exallocatepoolwithtag に** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)ドライバーがシステムのページング ファイルを保持するデバイスを制御しない限り、ページ プールからの初期化中にのみ使用があることができます。 このようなメモリの割り当てを解放する必要があります[ **ExFreePool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)する前に、 *DispatchPnP*ルーチンは、コントロールを返します。

-   WDM デバイス ドライバーの ISR でのデバイスのスタートアップ中にも不正な割り込みで呼び出されたかどうかを決定できる必要があります。 呼び出しから返された場合[ **IoConnectInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterrupt)を処理するコード パスで**IRP\_MN\_開始\_デバイス**、ISR呼び出せるすぐに割り込みがデバイスで有効な場合です。

 

 




