---
title: バスドライバーでのデバイスの削除
description: バスドライバーでのデバイスの削除
ms.assetid: f3961c29-02e1-41f0-bb7f-784bcdb57eb0
keywords:
- バスドライバー WDK PnP
- DispatchPnP ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 152f83dca65fe5bad3dfb8c999159e0b16a54614
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838453"
---
# <a name="removing-a-device-in-a-bus-driver"></a>バスドライバーでのデバイスの削除





子デバイス (子 PDO) を削除する場合、親バスドライバーは、デバイスを追加して起動するために実行されたすべての操作を元に戻す必要があります。

バスドライバーは、 [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンで次のような手順で子デバイスを削除します。

1.  ドライバーは、この PDO に対する[**突然の\_削除要求\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal) 、以前の IRP\_処理していますか?

    その場合は、残りのクリーンアップを実行し、手順4に進みます。

    通常、ドライバーはデバイスの拡張機能にフラグを保持します。これは、ドライバーが IRP\_を処理し、デバイスに対する予期しない **\_削除要求\_** 処理したかどうかを示します。

2.  ドライバーでキューに登録されているすべての要求を完了します。

3.  バスドライバーがこの操作を実行できる場合は、デバイスから電力を削除し、 [**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)を呼び出して電源マネージャーに通知します。

    バスドライバーは、可能であれば子デバイスの電源を入れ、電源状態の変化を電源マネージャーに通知します。 バスドライバーは、IRP\_に応答してこれを行い[ **\_デバイスの要求\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)します。デバイスが削除されているときに、デバイスの電源ポリシーの所有者は、 [**IRP\_\_設定\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)要求を送信しません。 詳細については、「[電源管理](implementing-power-management.md)」を参照してください。

4.  バスドライバーが、IRP\_**に対する最新**の応答でこのデバイスを報告した場合[ **\_クエリ\_デバイス\_関係**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)要求を使用して、デバイスは物理的にコンピューター上に存在します。 この場合、バスドライバーは次のようになります。

    -   デバイスが物理的に削除されるまで、デバイスの PDO を保持します。

    -   **Irp&gt;iostatus**を状態\_SUCCESS に設定します。

    -   [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を使用して IRP を完了します。

    -   [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンからを返します。

    バスドライバーは、デバイスが物理的に削除されるまで、**後続の列挙**型 (**IRP\_\_クエリ\_デバイス\_関係**) でこのデバイスの報告を継続する必要があります。 PnP マネージャーは、列挙されたデバイスが追加され、開始されたかどうかを追跡します。

5.  バスドライバーが **\_クエリ\_デバイス\_関係**要求に対する IRP\_**に対する最新**の応答にデバイスが含まれていなかった場合、バスドライバーはデバイスが物理的に削除されると見なします。装置. この場合、バスドライバーは次のことを行います。

    -   デバイス固有の割り当て、メモリ、イベントなどをクリーンアップします。

    -   **Irp&gt;iostatus**を状態\_SUCCESS に設定します。

    -   [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を使用して IRP を完了します。

    -   [**Iodeletedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)を使用して PDO を解放します。

        ドライバーが最新の**Busrelations**リストからデバイスを省略した場合、バスドライバーは PDO を削除する必要があります。 ユーザーがデバイスをコンピューターに再び接続する場合、バスドライバーは次の**Busrelations**クエリに応答して新しい PDO を作成する必要があります。 バスドライバーがデバイスの新しいインスタンスに対して同じ PDO を再利用する場合、マシンは正常に動作しません。

    -   *DispatchPnP*ルーチンからを返します。

PnP マネージャーが、\_デバイスの要求を**削除\_IRP\_** 送信したときにデバイスが存在する場合、バスドライバーは PDO を保持します。 後でデバイスがバスから物理的に削除された場合、PnP マネージャーは **\_デバイスを削除\_\_** 別の IRP を送信します。 その後の remove IRP の受信時に、バスドライバーはデバイスの PDO を削除します。

バスドライバーは、既に削除されていて、PDO が削除対象としてマークされているデバイスの **\_デバイスを削除\_、IRP\_** 処理できる必要があります。 このような IRP への応答として、バスドライバーは IRP または戻り値\_、そのような\_デバイス\_なしで正常に終了することができます。 この場合、デバイスの PDO はまだ削除されていません。これ**は、一部**のコンポーネントにはまだオブジェクトへの参照があるためです。 そのため、2番目の remove IRP を処理するときに、バスドライバーが PDO にアクセスできます。 バスドライバーは、PDO に対して2回目に**Iodeletedevice**を呼び出すことはできません。i/o システムは、参照カウントが0になると PDO を削除します。

バスドライバーは、デバイスに対する **\_デバイスの要求\_削除する IRP\_** を受信するまで、子デバイスのデータ構造を削除しません。 バスドライバーは、デバイスが削除されたことを検出して[**IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)を呼び出すことができますが、デバイスの PDO を削除しないでください。 PnP マネージャーは、 **\_デバイスの要求\_削除する IRP\_** を送信する必要があります。

 

 




