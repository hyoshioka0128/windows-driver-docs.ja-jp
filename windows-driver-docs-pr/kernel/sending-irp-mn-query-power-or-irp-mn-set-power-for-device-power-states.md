---
title: デバイス電源状態についての IRP_MN_QUERY_POWER または IRP_MN_SET_POWER の送信
description: デバイス電源状態についての IRP_MN_QUERY_POWER または IRP_MN_SET_POWER の送信
ms.assetid: 58f65138-abb9-4bb8-bf9b-14f17347e309
keywords:
- IRP_MN_SET_POWER
- IRP_MN_QUERY_POWER
- デバイスの電源状態 WDK カーネル
- クエリ-電源 Irp の WDK 電源管理
- 電源 Irp WDK カーネル、デバイスクエリ
- 電源状態のクエリ
- キューの Irp
- デバイスクエリの電源 Irp WDK カーネル
- 電源状態 Irp の送信
- パワー Irp WDK カーネル
- デバイスセットの電源 Irp WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bacf191fd94b5eea0aaf70e64e9da48029b9f07
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836365"
---
# <a name="sending-irp_mn_query_power-or-irp_mn_set_power-for-device-power-states"></a>IRP\_\_クエリ\_電力または\_IRP に送信し、デバイスの電源状態に\_電力を設定する





デバイスの電源ポリシー所有者は、デバイスクエリ-電源 IRP ([**irp\_\_クエリ\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)) を送信して、下位のドライバーがデバイスの電源状態の変化に対応できるかどうかを判断し、デバイスセット-電源 Irp ([**irp\_の\_セット\_電力**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)) デバイスの電源状態を変更します。 (このドライバーは、待機/ウェイク IRP を送信して、外部信号に応答してデバイスをウェイクアップできるようにすることもできます。詳細については、「[ウェイクアップ機能のあるデバイスのサポート](supporting-devices-that-have-wake-up-capabilities.md)」を参照してください)。

次のいずれかに該当する場合は、ドライバーが[**IRP\_\_クエリ\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)要求を送信する必要があります。

-   ドライバーはシステムクエリ-電源 IRP を受信します。

-   ドライバーは、アイドル状態のデバイスをスリープ状態にする準備をしています。そのため、それが可能であるかどうかを確認するために、下位のドライバーに対してクエリを実行する必要があります。

次のいずれかに該当する場合は、ドライバーが[**IRP\_\_設定\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)要求を送信する必要があります。

-   ドライバーは、デバイスがアイドル状態で、スリープ状態になる可能性があると判断しました。

-   デバイスはスリープ状態であり、待機中の i/o を処理するために作業中の状態に再入力する必要があります。

-   ドライバーはシステムセット-電源 IRP を受信します。

ドライバーは独自の電源 IRP を割り当てることはできません。この目的のために、電源マネージャーには[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)ルーチンが用意されています。 [電源 irp を処理するためのルール](rules-for-handling-power-irps.md)として、 **PoRequestPowerIrp**は IRP を割り当てて送信します。また、 **IoCallDriver** (windows 7 と windows Vista の場合) または**POCALLDRIVER** (windows Server 2003、windows XP、および) を組み合わせて送信します。Windows 2000) では、すべての電源要求が正しく同期されていることを確認します。 **PoRequestPowerIrp**の呼び出し元は、IRQL &lt;= ディスパッチ\_レベルで実行されている必要があります。

このルーチンのプロトタイプを次に示します。

```cpp
NTSTATUS
PoRequestPowerIrp (
    IN PDEVICE_OBJECT DeviceObject,
    IN UCHAR MinorFunction,
    IN POWER_STATE PowerState,
    IN PREQUEST_POWER_COMPLETE CompletionFunction,
    IN PVOID Context,
    OUT PIRP *Irp OPTIONAL
    );
```

IRP を送信するために、ドライバーは**PoRequestPowerIrp**を呼び出し、 *DeviceObject*内のターゲットデバイスオブジェクトへのポインターを指定します。また、マイナー irp コード IRP\_\_設定\_電力または IRP を\_ *\_します。MinorFunction*,、値**DevicePowerState** 、 <em>PowerState</em>**です。** <em>PowerState</em>のデバイスの電源状態を入力し**ます。状態**。 Windows 98/Me では、 *DeviceObject*は、基になるデバイスの PDO を指定する必要があります。windows 2000 以降のバージョンの Windows では、この値は、同じデバイススタック内の PDO または FDO のいずれかを指すことができます。

他のすべてのドライバーが IRP を完了した後に、ドライバーが追加のタスクを実行する必要がある場合は、入力候補の関数にポインターを渡す必要が*あります。* I/o マネージャーは、ドライバーが IRP をスタックに渡したときに、ドライバーによって設定されたすべての*Iocompletion*ルーチンを呼び出した後に、completion*関数*を呼び出します。

デバイスの電源ポリシー所有者がデバイスの power query IRP を送信するたびに、 **PoRequestPowerIrp**への呼び出しで指定されたコールバックルーチン (*補完機能*) からデバイスセット-電源 irp を送信する必要があります。 クエリが成功した場合、set-power IRP はクエリされた電源の状態を指定します。 クエリが失敗した場合、set-power IRP は現在のデバイスの電源状態を再アサートします。 ドライバーがクエリに応答して i/o をキューに置いているため、現在の状態を再アサートすることが重要です。ポリシーの所有者は、キューに入っている i/o 要求の処理を開始するために、デバイススタックでドライバーに通知するために set-power IRP を送信する必要があります。

デバイスのポリシー所有者は、デバイスの電源 IRP を送信するだけでなく、デバイススタックに渡されるときにも IRP を処理することに注意してください。 そのため、このようなドライバーでは、通常、デバイスの電源が入っているときに、IRP 処理コードの一部として*Iocompletion*ルーチン ( [**iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)) を設定します。 *Iocompletion*ルーチンは、他のドライバーによって設定された*iocompletion*ルーチンと、入力候補*機能*の前に順番に呼び出されます。 詳細については、「[デバイスの電源 irp の Iocompletion ルーチン](iocompletion-routines-for-device-power-irps.md)」を参照してください。

入力関数が呼び出されたときに、すべての*ドライバーが irp*を完了しているため、 **IoCallDriver**、 **Pocalldriver**、または**postartnextpowerirp**を呼び出し元の irp で呼び出す*ことはでき*ません。 (ただし、別の電源 IRP に対してこれらのルーチンを呼び出すこともできます)。代わりに、このルーチンは、IRP を発信したドライバーに必要な追加の操作を実行します。 ドライバーがシステムの irp に応答してデバイスの IRP を送信した場合、*補完機能*はシステムの irp を完了する可能性があります。 詳細については、「[デバイスの電源ポリシー所有者におけるシステムセット-電源 IRP の処理](handling-a-system-set-power-irp-in-a-device-power-policy-owner.md)」を参照してください。

**PoRequestPowerIrp**への呼び出しに応答して、電源管理者は電源 IRP を割り当てて、デバイスのデバイススタックの一番上に送信します。 電源マネージャーは、割り当てられた IRP へのポインターを返します。

エラーが発生しなかった場合、 **PoRequestPowerIrp**は STATUS\_PENDING を返します。 この状態は、IRP が正常に送信され、完了待ちになっていることを意味します。 電源マネージャーが IRP を割り当てられない場合、または呼び出し元が無効なマイナー電源 IRP コードを指定した場合、呼び出しは失敗します。

デバイスの電源投入要求は、まず、デバイスの基盤となるバスドライバーによって処理され、次にスタック内の上位のドライバーごとに処理される必要があります。 そのため、 **PowerDeviceD0**要求を送信する場合、ドライバーは、IRP の完了後にデバイスの電源がオンになった後に、必要なタスク*を実行する*ようにドライバーに要求します。

デバイス (**PowerDeviceD3**) の電源をオフにする場合、デバイススタック内の各ドライバーは、IRP を次の下位のドライバーに送信する前に、必要なすべてのコンテキストを保存し、必要なクリーンアップを実行する必要があります。 コンテキスト情報とクリーンアップの範囲は、ドライバーの種類によって異なります。 関数ドライバーは、ハードウェアコンテキストを保存する必要があります。フィルタードライバーでは、独自のソフトウェアコンテキストを保存することが必要になる場合があります。 この状況で設定された入力*関数*は、完了した電源 IRP に関連する操作を実行できますが、ドライバーはデバイスにアクセスできません。

 

 




