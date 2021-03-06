---
title: IRP を完了するタイミング
description: IRP を完了するタイミング
ms.assetid: 6986b24c-e7e5-43f2-861d-b84e4c131a8a
keywords:
- Irp WDK のカーネルの完了を完了するタイミング
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0174051868ff1bf4c5bdeb1a3b775cd39cfb951
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358075"
---
# <a name="when-to-complete-an-irp"></a>IRP を完了するタイミング





次の条件のいずれかが満たされたときに、ドライバーは IRP の完了を開始する必要があります。

-   ドライバーは IRP の処理は、無効なパラメーターまたはその他の条件のため続行できませんを決定します。

-   ドライバーは IRP がドライバー スタック ダウンを渡さずに、要求された I/O 操作を処理できないと操作が完了します。

-   IRP が取り消されます。 (を参照してください[Irp のキャンセル](canceling-irps.md))。

これらの条件が満たされない場合は、ドライバーのディスパッチ ルーチンは、次の下位ドライバーに IRP を渡す必要があります。 または I/O 要求の処理、処理する必要があります。 いずれかの条件が満たされる場合、ドライバーを呼び出す必要があります[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)します。

ドライバーが処理を進行できない、または通常呼び出して実際には、デバイスにアクセスしなくても、要求された操作を処理することによって、要求が完了すると、ため、要求を完了すると**IoCompleteRequest**のいずれかから、ルーチンをディスパッチします。 詳細については、次を参照してください。[ディスパッチ ルーチン内での Irp の完了](completing-irps-in-dispatch-routines.md)します。

通常、呼び出す場合、ドライバーは、要求を満たすためにデバイスにアクセスする必要があります、 **IoCompleteRequest**から、 [ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)ルーチン。 これらのルーチンが広範に説明した[割り込みサービス](servicing-interrupts.md)します。

 

 




