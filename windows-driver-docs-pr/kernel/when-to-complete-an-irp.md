---
title: IRP を完了するタイミング
description: IRP を完了するタイミング
ms.assetid: 6986b24c-e7e5-43f2-861d-b84e4c131a8a
keywords:
- Irp WDK カーネルを完了すると完了するタイミング
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91dda582bc5e149acaecf379710269f286f67d86
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835729"
---
# <a name="when-to-complete-an-irp"></a>IRP を完了するタイミング





次のいずれかの条件が満たされた場合、ドライバーは IRP の完了を開始する必要があります。

-   パラメーターまたはその他の条件が無効であるために、IRP 処理を実行できないことがドライバーによって判断されます。

-   ドライバーは、IRP をドライバースタックに渡すことなく、要求された i/o 操作を処理できるようになり、操作が完了しました。

-   IRP は取り消されています。 (「 [Irp のキャンセル](canceling-irps.md)」を参照してください)。

これらの条件が満たされない場合、ドライバーのディスパッチルーチンは、IRP を次の下位のドライバーに渡すか、i/o 要求の処理を処理する必要があります。 いずれかの条件が満たされた場合、ドライバーは[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出す必要があります。

処理を続行できないためにドライバーが要求を完了した場合、またはデバイスに実際にアクセスせずに要求された操作を処理して要求を完了した場合は、通常、ディスパッチルーチンの1つから**IoCompleteRequest**が呼び出されます。 詳細については、「[ディスパッチルーチンでの irp の完了](completing-irps-in-dispatch-routines.md)」を参照してください。

ドライバーは、要求を満たすためにデバイスにアクセスする必要がある場合、通常は[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチンから**IoCompleteRequest**を呼び出します。 これらのルーチンについては、「[割り込み](servicing-interrupts.md)の処理」で詳しく説明します。

 

 




