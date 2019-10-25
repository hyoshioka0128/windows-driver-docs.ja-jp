---
title: システムの電源 IRP
description: システムの電源 IRP
ms.assetid: a37e8dda-af7a-4f28-bf04-908a74bb5b2f
keywords:
- 電源 Irp WDK カーネル、システム
- システム電源 Irp WDK カーネル
- IRP_MJ_POWER
- IRP_MN_SET_POWER
- IRP_MN_QUERY_POWER
- 突入電流 power WDK カーネル
- system 突入電流 power WDK カーネル
- 電源状態の変更 WDK カーネル
- 電源状態の再確定
- アイドルタイムアウトの WDK 電源管理
- 期限切れのバッテリ WDK 電源管理
- バッテリの有効期限 WDK 電源管理
- ユーザーが要求した電力の変更 (WDK カーネル)
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 473688bc5545d77a0b877a79289a6dc8f318436d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827638"
---
# <a name="power-irps-for-the-system"></a>システムの電源 IRP





*システム電源 irp*は、 [**MJ\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)、次に示す**マイナー電源 IRP**コードの1つ、および irp スタックの SystemPowerState メンバーの値を指定して、主な irp コード irp を\_します。 このような IRP を送信できるのは電源マネージャーだけです。ドライバーがシステム電源 IRP を送信できません。

電源マネージャーは、次のいずれかの理由でシステム電源 IRP を送信します。

-   アイドルタイムアウトに応じてシステムの電源状態を変更するには、システムの利用状況、ユーザーの要求、またはバッテリの有効期限が切れている ([**IRP\_\_設定\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power))

-   システムがスリープ状態になるかどうかを判断するためにデバイスを照会するには ([**IRP\_完了\_クエリ\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power))

-   クエリの後で現在のシステムの電源状態を reaffirm するには (**IRP\_\_設定\_電源**)

電源マネージャーは、システムに代わって電源要求 **\_設定**された **\_\_クエリ**\_を実行し、irp\_を送信します。 ドライバーが Irp\_に失敗する可能性があり **\_クエリ\_電源**要求が発生しても、 **irp\_** \_電力を設定\_に失敗することはできません。

たとえば、システムの電源状態を変更するために、電源マネージャーは、デバイスツリーの各デバイスノードで、スタック内の最上位のドライバーにシステム電源の IRP を送信します。 次の図は、1つのデバイススタック内のドライバーがシステム電源 IRP を処理する方法を示しています。

![システム電源 irp のパスを示す図](images/s2dirp.png)

前の図に示すように、次のようになります。

1.  電源マネージャーは、i/o マネージャーを呼び出して、デバイスツリー内の各リーフノードにシステム電源 IRP を送信します。

2.  ドライバーは、可能であれば IRP を処理し、必要に応じて[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定し、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) (Windows 7 および windows Vista) または[**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (windows Server 2003、windows XP、および windows 2000) を呼び出して、irp をスタックに転送します。 ドライバーが IRP を失敗させる必要がある場合、ドライバーはすぐにそれを実行し、IRP を完了します。 ドライバーは、 **irp\_異常\_クエリ\_電源**irp に失敗する可能性がありますが、システムの電源状態を設定する **\_電源 irp\_設定**された irp\_に失敗しないようにする必要があります。

3.  デバイスの電源ポリシーを所有するドライバーが IRP を受信すると、そのドライバーはシステム IRP の*Iocompletion*ルーチンを設定し、irp を転送します。

4.  スタック内の他のすべてのドライバーは、可能であれば IRP を処理し、必要に応じて*Iocompletion*ルーチンを設定し、次の下位のドライバーに irp を転送します (手順 2.)。

5.  最終的には、バスドライバーはシステムの IRP を受信し、完了します。

6.  I/o マネージャーは、ドライバーとして設定されたすべての*Iocompletion*ルーチンを呼び出し、デバイススタックをシステム IRP に渡します。

7.  *Iocompletion*ルーチンでは、デバイスの電源ポリシー所有者は、 [**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)を呼び出して、システムの irp 内のシステム電源の状態に対して有効なデバイスの電源状態を指定して、デバイスの電源 IRP を送信します。 ドライバーは、デバイスの電源 IRP の完了時に呼び出されるコールバックルーチンを設定します。

    必要に[応じて、](reporting-device-power-capabilities.md)ドライバーは[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)構造のキャッシュされたコピーの**devicestate**メンバーを調べて、システムに対応するデバイスの電源状態を特定します。IRP 内の電源の状態。

8.  デバイスの IRP が完了し、デバイスの IRP 完了ルーチンが実行されると、電源ポリシー所有者のコールバックルーチンが呼び出されます。 コールバックルーチンでは、ドライバーは返された状態をシステムの IRP にコピーします。 Windows Server 2003、Windows XP、および Windows 2000 では、コールバックは[**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出して次の電源 IRP を開始します。 ただし、Windows 7 と Windows Vista では、 **Postartnextpowerirp**を呼び出す必要はなく、このような呼び出しは電源管理操作を実行しません。 最後に、コールバックは[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して、システムの IRP を完了します。

詳細については、「[システム電源状態要求の処理](handling-system-power-state-requests.md)」を参照してください。

一部のデバイスは電源オン時に突入電流を必要とするため、システム突入電流の電源 Irp はシステム全体で同期的に処理されます。 このような IRP は一度に1つしかアクティブにできません。 詳細については、「 [IoCallDriver の呼び出しと PoCallDriver の呼び出し](calling-iocalldriver-versus-calling-pocalldriver.md)」を参照してください。

 

 




