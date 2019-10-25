---
title: IoCallDriver の呼び出しと PoCallDriver の呼び出し
description: IoCallDriver の呼び出しと PoCallDriver の呼び出し
ms.assetid: a47e2310-e89b-4552-bbe3-d4984ae8b564
keywords:
- PoCallDriver
- アクティブな電源 Irp WDK カーネル
- 電源 Irp WDK カーネル、IoCallDriver 対 PoCallDriver
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0656f9c6c8e1d6d390c3a0933783d61a1c49b93b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828624"
---
# <a name="calling-iocalldriver-versus-calling-pocalldriver"></a>IoCallDriver の呼び出しと PoCallDriver の呼び出し





Windows Vista 以降では、ドライバーは[**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)ではなく[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、電源 irp を次の下位のドライバーに渡す必要があります。 Windows Server 2003、Windows XP、および Windows 2000 では、ドライバーは**IoCallDriver**ではなく**pocalldriver**を呼び出して、電源 irp を次の下位のドライバーに渡す必要があります。 ただし、同じコードを使用して Windows Vista と以前のバージョンの Windows で実行するドライバーは、 **IoCallDriver**ではなく**pocalldriver**を呼び出す必要があることに注意してください。

Windows Vista 以降では、 [**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)と**IoCallDriver**によって、電源マネージャーがシステム全体の電源 irp を適切に同期していることを確認します。 Windows Server 2003、Windows XP、および Windows 2000、 **PoRequestPowerIrp**、 **Pocalldriver**、および[**postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)では、電源マネージャーがシステム全体の電源 irp を適切に同期していることを確認します。

システムによって、アクティブな電源 Irp の数が次のように制限されます。

-   任意の時点で、1つのシステム電源 IRP (**irp\_\_に\_電力**) が設定されていません。

-   1つ以上のデバイスセットがありません-電源 IRP (**irp\_\_セット\_電力)** は、特定の時点で各 PDO に対してアクティブにすることができます。

-   突入電流の電源を必要とするデバイスの電源 IRP を、システム内の任意の時点でアクティブにすることはできません。

2つの突入電流デバイスが同時に電源をオンにしないようにするため、電源マネージャーは、システム全体でアクティブな突入電流の電源 Irp を追跡し、一度に1つのアクティブにすることのみを許可します。 アクティブな突入電流 IRP が完了するまで、追加の突入電流 IRP を開始することはできません。

突入電流 Irp に対するこれらの制限により、別のデバイスの突入電流 IRP の完了中にデバイスの電源 IRP がブロックされることがあります。 ドライバーの作成者は、デバッグ中にこの動作に注意する必要があります。

 

 




