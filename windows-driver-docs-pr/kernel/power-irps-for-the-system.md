---
title: システムの電源 IRP
description: システムの電源 IRP
ms.assetid: a37e8dda-af7a-4f28-bf04-908a74bb5b2f
keywords:
- システム電源 Irp WDK カーネル
- システム電源の Irp WDK カーネル
- IRP_MJ_POWER
- IRP_MN_SET_POWER
- IRP_MN_QUERY_POWER
- 突入 power WDK カーネル
- システム突入 power WDK カーネル
- 電源の状態の WDK カーネルを変更します。
- 電源状態のアポイントメント
- アイドル タイムアウト WDK の電源管理
- 有効期限が切れたバッテリ WDK の電源管理
- バッテリ切れ WDK の電源管理
- ユーザーが要求した電源変更 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dde0771ddcec4c9f09e737c9d6170e10daefc521
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369677"
---
# <a name="power-irps-for-the-system"></a>システムの電源 IRP





A*システム電源 IRP* IRP の主要なコードを指定します[ **IRP\_MJ\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)、1 つ以下に示すマイナー power IRP コードと値**SystemPowerState**で、 **Power.Type** IRP スタックのメンバー。 電源マネージャーのみがこのような IRP を送信できます。ドライバーは IRP のシステムの電源を送信できません。

電源マネージャーは、次の理由の 1 つのシステム電源 IRP を送信します。

-   アイドル タイムアウトをシステムの使用状況の変更、ユーザーの要求、または期限切れ間近のバッテリへの応答でシステムの電源状態を変更する ([**IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power))

-   システムがスリープ状態に移動できるかどうかを判断するデバイスのクエリを ([**IRP\_MN\_クエリ\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power))

-   クエリの後に現在のシステム電源の状態のことを再確認する (**IRP\_MN\_設定\_POWER**)

電源マネージャー送信**IRP\_MN\_クエリ\_POWER**と**IRP\_MN\_設定\_POWER**の代わりに要求システム。 ドライバーが失敗することが、 **IRP\_MN\_クエリ\_POWER**要求しますが、失敗することはできません**IRP\_MN\_設定\_POWER**します。

たとえば、システムの電源状態を変更する電源マネージャーを送信しますシステム電源 IRP で各デバイス、デバイス ツリーのノードでのスタック上のドライバー。 次の図は、1 つのデバイス スタック内のドライバーが IRP のシステムの電源を処理する方法を示します。

![システム電源の irp のパスを示す図](images/s2dirp.png)

: 前の図に示す

1.  電源マネージャーは、システム電源 IRP をデバイス ツリー内の各リーフ ノードに送信するマネージャー、I/O を呼び出します。

2.  IRP が設定可能な場合は、ドライバー ハンドル[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチン、必要に応じて、呼び出し[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) (Windows 7 および WindowsVista) または[ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver) (Windows Server 2003、Windows XP、および Windows 2000) IRP が下位のスタックを転送するようにします。 場合は、ドライバーは IRP を失敗する必要があります、ドライバーはすぐにはし、IRP を完了します。 ドライバーが失敗することが**IRP\_MN\_クエリ\_POWER** Irp で失敗する必要がありますが、 **IRP\_MN\_設定\_POWER** Irp をシステム電源の状態を設定します。

3.  設定した場合、デバイスが IRP を受信するは、電源ポリシーを所有しているドライバー、ドライバー、 *IoCompletion* IRP のシステムと、転送、IRP ルーチン。

4.  IRP スタック ハンドルで他のすべてのドライバーが設定可能であれば、 *IoCompletion*必要に応じて、ルーチンで、手順 2 のように、次の下位のドライバーに IRP を転送します。

5.  最終的には、バス ドライバーでは、受信し、システムの IRP を完了します。

6.  I/O マネージャーを呼び出し、 *IoCompletion*ドライバーに渡される IRP のシステムとして設定されたルーチンがデバイス スタックをダウンします。

7.  その*IoCompletion*日常的なデバイスの電源ポリシー所有者呼び出し[ **PoRequestPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)デバイスの電源が有効であるデバイスの電源状態を指定する、IRP を送信する、システムの IRP でシステム電源の状態。 ドライバーは、デバイスの電源 IRP の完了時に呼び出されるコールバック ルーチンを設定します。

    かどうか、必要に応じて、ドライバーを参照して、 **DeviceState**のキャッシュされたコピー内のメンバー、 [**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)構造 (を参照してください[デバイスの電源機能の報告](reporting-device-power-capabilities.md)) の電源状態が IRP のシステム電源の状態に対応するデバイスを決定します。

8.  IRP のデバイスが完了し、あらゆるデバイス IRP の完了ルーチンを実行した後、電源ポリシー所有者のコールバック ルーチンが呼び出されます。 コールバック ルーチンで、ドライバーは IRP のシステムに返される状態をコピーします。 コールバックの呼び出しでは、Windows Server 2003、Windows XP、および Windows 2000、 [ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp) IRP の [次へ] のパワーを開始します。 ただしで Windows 7 および Windows Vista では、呼び出す**PoStartNextPowerIrp**は必要ありませんし、このような呼び出しには電源管理操作は実行されません。 最後に、コールバックを呼び出す[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)システム IRP を完了します。

詳細については、次を参照してください。[システム電源の状態要求の処理](handling-system-power-state-requests.md)します。

一部のデバイスは、電源をオンにする突入電流の必要があるために、システム突入 power Irp は、システム全体で同期的に、順番が処理されます。 一度にアクティブにできるこのような IRP の 1 つだけです。 詳細については、次を参照してください。[保留を呼び出すとします。呼び出す PoCallDriver](calling-iocalldriver-versus-calling-pocalldriver.md)します。

 

 




