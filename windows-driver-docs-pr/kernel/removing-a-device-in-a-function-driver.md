---
title: ファンクション ドライバーでのデバイスの削除
description: ファンクション ドライバーでのデバイスの削除
ms.assetid: 46a75647-e72a-4194-be9d-070e3ac95650
keywords:
- 関数ドライバー WDK PnP
- DispatchPnP ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e0b688d60db56844778c4c201c9499c1dc65583
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838455"
---
# <a name="removing-a-device-in-a-function-driver"></a>ファンクション ドライバーでのデバイスの削除





デバイスを削除する場合、関数ドライバーは、デバイスを追加して起動するために実行されたすべての操作を元に戻す必要があります。 この説明には、周辺機器用の関数ドライバーと、バスデバイス用の機能ドライバーが含まれています。

関数ドライバーは、 [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンで次のような手順を使用して、デバイスを削除します。

1. これはバスデバイス用の関数ドライバーですか。

   その場合は、バス上のデバイスの未処理の子 PDOs を削除する可能性があります。

   バスドライバーが以前の Irp を処理した\_、子デバイスに対して予期しない[ **\_削除要求\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)したが、ドライバーがそれ以降の irp を受信していない場合\_デバイス要求を[**削除\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)では、バスドライバーは子 PDO をそのまま残します。 後で、子デバイスへのすべてのハンドルが閉じられると、PnP マネージャーが子デバイスの削除 IRP を送信し、その時点で、バスドライバーが子 PDO を削除します。

   バスドライバーが以前の Irp を処理し、デバイスのデバイスの要求を**削除\_\_** していて、その後の**irp\_\_の\_突然の削除**要求がない場合は、バスドライバーが子を削除します。PDO.\_ この場合、PnP マネージャーは、親バスデバイスに remove IRP を送信する前に、すべての関数とフィルタードライバーが子デバイスから削除されている (FDO とフィルター DOs が削除されている) ことを確認します。 子 PDO がまだ存在している可能性があるため、バスドライバーは、バスデバイスを削除する前に、子 PDO を削除する必要があります。

2. ドライバーは、この FDO の予期しない **\_削除要求\_** 、以前の IRP\_処理していますか?

   その場合は、残りのクリーンアップを実行し、手順 8. [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)に進みます。

   通常、ドライバーはデバイスの拡張機能にフラグを保持します。これは、ドライバーが IRP\_を処理し、デバイスに対する予期しない **\_削除要求\_** 処理したかどうかを示します。

3. ドライバーで事前にデバイスのウェイクアップが有効になっている場合は、 [**IRP\_完了\_待ち\_ウェイク**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)要求をキャンセルします。

4. デバイスが非アクティブであることを確認します。

   以前の IRP\_に応答してデバイスがまだ非アクティブになっていない場合は **\_クエリ\_\_デバイスを削除**します。ドライバーは、デバイスが新しい要求を受け入れていないとマークし、このドライバーでキューに登録されているすべての要求を完了する必要があります。 ドライバーは、デバイスへのアクセスを必要とするすべての未処理の要求を失敗させる必要があります。

   ドライバーは、 **Io*Xxx*removelock<em>Xxx</em>** ルーチンを使用して未処理 i/o をカウントし、削除処理を続行できることを示すイベントを設定できます。

5. 電源を切る操作を実行します。

   デバイスの各ドライバーは、\_IRP を受信したときに、 **\_デバイス要求\_削除**することによって、そのデバイスの電源ダウン操作を実行します。 デバイスの電源ポリシー所有者 (通常は関数ドライバー) は、個別の IRP\_を送信しません。[**電源要求\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)して、デバイスの電源状態を D3 に設定\_ます。 通常、親バスドライバーはスロットを電源オフにし、バスドライバーが remove IRP を取得すると、 [**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)を使用して電源マネージャーに通知します。 詳細については、「[電源管理](implementing-power-management.md)」を参照してください。

6. [**Iosetdeviceinterfacestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)を呼び出すことによって、すべてのデバイスインターフェイスを無効にします。

7. ドライバーによって使用されているデバイスのすべてのハードウェアリソースを解放します。

   正確な操作は、デバイスとドライバーによって異なりますが、 [**Io切る割り込み**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterrupt)による割り込みの切断、 [**Mmunmapiospace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace)を使用した物理アドレス範囲の解放、および i/o ポートの解放を含むことができます。

8. IRP\_次のドライバーに\_デバイスの要求を**削除\_** 渡します。

   [**IoskipIoCallDriver Enti Stacklocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を使用して、次に低いドライバーの irp スタックの場所を設定し、irp を次[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)のドライバーに渡します。

   ドライバーは、削除操作を続行する前に、基になるドライバーが削除操作を完了するのを待つ必要はありません。

9. [**IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodetachdevice)を使用して、デバイススタックからデバイスオブジェクトを削除します。

   *ほか*パラメーターとして、次に小さいデバイスオブジェクトへのポインターを指定します。 ドライバーは、ドライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンで[**Ioattachdevicetodevicestack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)の呼び出しからこのようなポインターを受け取ります。

10. デバイス固有の割り当て、メモリ、イベントなどをクリーンアップします。

11. [**Iodeletedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)で FDO を解放します。

12. **IoCallDriver**から戻り値の状態を反映して、 [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンからを返します。

関数ドライバーでは、remove IRP の[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンが指定されていません。また、irp も完了しません。 Irp の削除は、親バスドライバーによって完了します。

 

 




