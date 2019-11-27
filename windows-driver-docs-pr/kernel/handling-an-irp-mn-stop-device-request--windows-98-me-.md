---
title: IRP_MN_STOP_DEVICE 要求の処理 (Windows 98/Me)
description: IRP_MN_STOP_DEVICE 要求の処理 (Windows 98/Me)
ms.assetid: 8e44561a-f494-48ce-ab61-aa47cd4e1c64
keywords:
- IRP_MN_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5154f9951f37df26a992adcad1efb63ed5e249e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838659"
---
# <a name="handling-an-irp_mn_stop_device-request-windows-98me"></a>\_デバイスの要求を停止\_IRP\_処理する (Windows 98/Me)





Windows 98/Me では、通常、PnP マネージャーは、クエリの停止が成功した後に、\_デバイスの要求を[**停止\_\_、IRP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)を送信します。 ただし、デバイススタックが以前に\_デバイスの要求を開始\_たときに[**irp\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)失敗した場合、PnP マネージャーは、前のクエリを使用せずに\_デバイスの要求を**停止\_\_** を送信します。

**\_デバイス要求\_停止する IRP\_** は、デバイススタックの上位のドライバーによって最初に処理され、次に下位のドライバーごとに処理されます。 ドライバーは、 [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンで停止 irp を処理します。

ドライバーは、次のような手順を使用して、 **\_デバイスの要求\_停止する IRP\_** を処理します。

1.  デバイスが一時停止されていることを確認します。

    IRP\_に応答してデバイスを完全に一時停止しなかった場合は[ **\_クエリ\_停止**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)要求を実行する必要があります。

    デバイスが停止している間、デバイスの電源が切断され、デバイスの状態が失われる可能性があります。 デバイスのドライバーは、デバイスの状態に関する情報を保存し、後続の IRP\_を受信したときにその情報を復元して **\_デバイスの要求\_開始**する必要があります。

2.  デバイスのハードウェアリソースを解放します。

    関数ドライバーでは、正確な操作はデバイスとドライバーによって異なりますが、割り込みの切断、 [**io切った割り込み**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterrupt)の切断、 [**Mmunmapiospace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace)を使用した物理アドレス範囲の解放、i/o ポートの解放などを行うことができます。

    フィルターまたはバスドライバーによってデバイスのハードウェアリソースが取得された場合、そのドライバーは IRP\_に応答してリソースを解放し、 **\_デバイスの要求\_停止**する必要があります。

3.  **Irp-&gt;iostatus. status**を STATUS\_SUCCESS に設定します。

4.  IRP を次の下位のドライバーに渡すか、または IRP を完了します。

    -   関数またはフィルタードライバーで、次のスタックの場所を[**IoskipIoCallDriver Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)で設定します。次に、IRP を[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を使用して次の下位のドライバーに渡し、 **IoCallDriver**から状態を*DispatchPnP*ルーチンからのリターンステータスとして返します。 IRP を完了しないでください。

    -   バスドライバーでは、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を使用して IRP を完了します。 IO\_は\_インクリメントを行わず、 *DispatchPnP*ルーチンからを返します。

デバイスが停止している間に、デバイスにアクセスする Irp を開始することはできません。 ドライバーは、このような Irp を失敗する必要があります。

 

 




