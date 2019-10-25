---
title: フィルター ドライバーまたはファンクション ドライバーでのシステム電源クエリ IRP の処理
description: フィルター ドライバーまたはファンクション ドライバーでのシステム電源クエリ IRP の処理
ms.assetid: 81d921d5-6db8-4858-b86e-1484781faba5
keywords:
- クエリ-電源 Irp の WDK 電源管理
- フィルタードライバーの WDK 電源管理
- 関数ドライバー WDK の電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75aa2e3a93acbd6a939feb93c8f40951f99b7ec2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836616"
---
# <a name="handling-a-system-query-power-irp-in-a-filter-or-function-driver"></a>フィルター ドライバーまたはファンクション ドライバーでのシステム電源クエリ IRP の処理





フィルターまたは関数ドライバー (デバイスの電源ポリシー所有者ではない) は、次の手順でシステムクエリ-電源 IRP を次の下位のドライバーに渡す必要があります。

1.  現在の IRP を渡して[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)を呼び出し、ドライバーが PnP\_irp を受信していないことを確認します。これにより、電源 irp の処理中に[ **\_デバイスの要求\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)されます。

    **IoAcquireRemoveLock**がエラー状態を返した場合、ドライバーは IRP の処理を続行しません。 代わりに、Windows Vista 以降では、ドライバーは[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して IRP を完了し、エラー状態を返す必要があります。 Windows Server 2003、Windows XP、および Windows 2000 では、ドライバーは[**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出し、 **IoCompleteRequest**を呼び出して IRP を完了し、エラーの状態を返す必要があります。

2.  クエリを失敗させる必要があるかどうかを判断します。 ガイドラインについては、このセクションで説明されているように、[フィルターまたは関数ドライバーでシステムクエリ-電源 IRP を失敗](failing-a-system-query-power-irp-in-a-filter-or-function-driver.md)させて処理を完了する方法に関するページを参照してください。

3.  [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出します。 (Windows Server 2003、Windows XP、および Windows 2000 のみ)

4.  IRP スタックの場所を設定します ([**Ioskip% Enti\n location**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)または[**Iocopy"enti"** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)を設定します)。 ドライバーでは、IRP に[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定できますが、これを行う必要はほとんどありません。

5.  **IoCallDriver** (windows 7 および windows Vista の場合) または[**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (Windows SERVER 2003、Windows XP、および windows 2000) を呼び出して、IRP を次の下位のドライバーに渡します。

6.  [**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)を呼び出します。 ただし、ドライバーが IRP の*Iocompletion*ルーチンを設定している場合は、代わりに*iocompletion*ルーチンからこの呼び出しを行います。

7.  [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)のルーチンから状態\_PENDING が返されます。

 

 




