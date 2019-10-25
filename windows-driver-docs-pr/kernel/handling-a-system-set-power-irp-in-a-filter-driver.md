---
title: フィルター ドライバーでのシステム電源設定 IRP の処理
description: フィルター ドライバーでのシステム電源設定 IRP の処理
ms.assetid: a6e364fc-f173-47ce-b36b-84f802cefcc3
keywords:
- パワー Irp WDK 電源管理の設定
- フィルタードライバーの WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5a8eeb3550ffe44a933ca5812c5d034b8e33bf6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838671"
---
# <a name="handling-a-system-set-power-irp-in-a-filter-driver"></a>フィルター ドライバーでのシステム電源設定 IRP の処理





すべてのフィルタードライバーと、そのデバイススタックの電源ポリシーを所有していないすべての関数ドライバーは、次の手順でシステム設定-電源 IRP を次の下位のドライバーに渡すだけで済みます。

1.  現在の IRP を渡して[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)を呼び出し、ドライバーが PnP\_irp を受信していないことを確認します。これにより、電源 irp の処理中に[ **\_デバイスの要求\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)されます。

    **IoAcquireRemoveLock**がエラー状態を返した場合、ドライバーは IRP の処理を続行しません。 代わりに、Windows Vista 以降では、ドライバーは[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して IRP を完了し、エラー状態を返す必要があります。 Windows Server 2003、Windows XP、および Windows 2000 では、ドライバーはまず[**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出し、 **IoCompleteRequest**を呼び出して IRP を完了してから、エラー状態を返します。

2.  **Postartnextpowerirp**を呼び出して、次の電源 IRP を開始します。 (Windows Server 2003、Windows XP、および Windows 2000 のみ)。

3.  IRP スタックの場所を設定します ([**Ioskip% Enti\n location**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)または[**Iocopy"enti"** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)を設定します)。 ドライバーでは、IRP に[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定できますが、これを行う必要はほとんどありません。

4.  [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) (windows 7 および windows Vista の場合) または[**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (Windows SERVER 2003、Windows XP、および windows 2000) を呼び出して、IRP を次の下位のドライバーに渡します。

5.  [**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)を呼び出します。 ただし、ドライバーが IRP の[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定している場合は、代わりに*iocompletion*ルーチンからこの呼び出しを行います。

6.  [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)のルーチンから状態\_PENDING が返されます。

 

 




