---
title: PnP Irp をデバイススタックに渡す
description: PnP Irp をデバイススタックに渡す
ms.assetid: 339ef4b4-1b4f-42ac-ab57-c53b83120f0d
keywords:
- PnP WDK カーネル、Irp をデバイススタック下に渡す
- WDK カーネルをプラグアンドプレイし、Irp をデバイススタックに渡す
- Irp WDK PnP
- I/o 要求パケットの WDK PnP
- Irp をデバイススタック WDK に渡す
- IoCompletion ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d76dd93e9d875c315ec4649e2238b8b414b298d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838518"
---
# <a name="passing-pnp-irps-down-the-device-stack"></a>PnP Irp をデバイススタックに渡す





PnP マネージャーは、Irp を使用して、デバイスを開始、停止、および削除し、デバイスに関するドライバーを照会するようにドライバーに指示します。 すべての PnP Irp には、主要な関数コード[**IRP\_MJ\_pnp**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)があり、すべての pnp ドライバーは、この関数コードを処理するために[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンを提供する必要があります。 PnP マネージャーは、irp **&gt;iostatus を初期化します。状態**は、irp を送信したときにサポート\_されない状態\_に初期化されます。 詳細については、「 [DispatchPnP ルーチン](dispatchpnp-routines.md)」を参照してください。

PnP のマイナー Irp の一覧については、「[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)」を参照してください。

スタック内のドライバーが IRP に障害を発生させる場合を除き、デバイスのすべてのドライバーが PnP IRP に応答する機会を持つ必要があります。 (次の図を参照してください)。

![プラグアンドプレイ irp をデバイススタックに渡す方法を示す図](images/passpnp.png)

1つのデバイスに対して、PnP IRP に応答する唯一のドライバーであるとは限りません。 たとえば、Irp\_に応答する関数ドライバーが[ **\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)を要求し、それを次の下位のドライバーに渡さずに irp を完了するとします。 下位のドライバーでサポートされている機能 (一意のインスタンス ID や、親バスドライバーでサポートされている電源管理機能など) は報告されません。

親バスドライバーが[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出し、i/o マネージャーが関数ドライバーまたはフィルタードライバーによって登録された[*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを呼び出すと、PnP IRP はデバイススタックをバックアップします。

関数またはフィルタードライバーは、PnP IRP を受信するときに次の操作を行う必要があります。

-   ドライバーが IRP に応答してアクションを実行する場合は、次のようになります。
    1.  適切な操作を実行します。
    2.  [ **Irp-&gt;iostatus** ] を適切な状態 (STATUS\_SUCCESS など) に設定します。 Irp に該当する場合は、 **irp&gt;IoStatus. 情報を設定します。**
    3.  [**Ioskipで**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)次のスタックの場所を設定します。この場所または[**Iocopy"enti"** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)を設定します。 *Iocompletion*ルーチンを設定する場合は、後者のルーチンを呼び出します。
    4.  必要に応じて、 *Iocompletion*ルーチンを設定します。
    5.  IRP を完了しないでください。 ( **IoCompleteRequest**を呼び出さないでください)。親バスドライバーが IRP を完了します。
-   ドライバーがこの IRP に対するアクションを実行しない場合は、IRP を次のドライバーに渡すように準備するだけです。
    1.  **Ioskipの場所**を呼び出して、IRP からスタック位置を削除します。
    2.  **Irp&gt;IoStatus**のフィールドは設定しないでください。
    3.  *Iocompletion*ルーチンを設定しないでください。
    4.  IRP を完了しないでください。 ( **IoCompleteRequest**を呼び出さないでください)。親バスドライバーが IRP を完了します。

関数またはフィルタードライバーが IRP に失敗しなかった場合、IRP は[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を使用して次の下位のドライバーに渡されます。 ドライバーには、次に低いドライバーへのポインターがあります。このポインターは、より上位のドライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンで[**Ioattachdevicetodevicestack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)呼び出しから返されました。

親バスドライバーは、IRP に応答するタスクを実行した後に、IRP を完了します。 バスドライバーが**IoCompleteRequest**を呼び出した後、i/o マネージャーは、そのデバイスの関数またはフィルタードライバーによって登録された*iocompletion*ルーチンを呼び出します。

 

 




