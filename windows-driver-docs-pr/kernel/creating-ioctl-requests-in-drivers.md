---
title: ドライバー内での IOCTL 要求の作成
description: ドライバー内での IOCTL 要求の作成
ms.assetid: 155e2577-0e9a-4c0b-a25a-8516ce3de631
keywords:
- I/o 制御コード WDK カーネル、要求の作成
- コントロールコード WDK Ioctl、要求の作成
- Ioctl WDK カーネル、要求の作成
- WDK Irp の同期
- 埋め込みポインター WDK Ioctl
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2538af4d6cb85ecbabb7eff5b22e03e3a28424d2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828452"
---
# <a name="creating-ioctl-requests-in-drivers"></a>ドライバー内での IOCTL 要求の作成





クラスドライバーまたはその他の上位レベルのドライバーは、i/o 制御要求に対して Irp を割り当てて、次のように次の下位のドライバーに送信できます。

1.  主要な関数コード[**irp\_MJ\_device\_CONTROL**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)または[**IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)を使用して、I/o 要求パケット ([**irp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)) を割り当てたり再利用したりします。 [**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)ルーチンを使用して、IOCTL IRP を具体的に割り当てることができます。 また、 [**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)、 [**IoReuseIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp)、 [**ioinitialization EIRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeirp)など、汎用の IRP 作成ルーチンと初期化ルーチンを使用することもできます。 IRP 割り当ての詳細については、「[下位レベルのドライバー用の irp の作成](creating-irps-for-lower-level-drivers.md)」を参照してください。

2.  IOCTL\_*XXX*コードと適切なパラメーターを使用して、IRP 用の下位ドライバーの i/o スタックの場所を設定します。

3.  IOCTL 要求が非同期に完了する場合は、 [**Keinitializeevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeevent)ルーチンを呼び出して、イベントオブジェクトを通知イベントとして初期化します。 ドライバーは、このイベントを使用して i/o 操作が完了するまで待機します。

4.  IRP を使用して[**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出し、次の操作を実行するために上位ドライバーが[*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを指定できるようにします。

    -   下位のドライバーが特定の要求を処理した方法を確認します。

    -   低いドライバーが要求された操作を完了した後に、IRP を再利用して、別の要求を送信したり、ドライバーによって作成された IRP を破棄したりします。 ドライバーは、 [**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)によって作成された irp を再利用することはできません。 詳細については、「Irp の再[利用](reusing-irps.md)」を参照してください。

5.  [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、要求を下位のドライバーに渡します。

6.  [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)が STATUS\_PENDING を返した場合は、 [**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)ルーチンを呼び出して、現在のスレッドを待機状態にします。 ドライバーは、 [**Keinitializeevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeevent)への呼び出しで初期化されたイベントオブジェクトのアドレスにルーチンの*オブジェクト*パラメーターを設定します。

    **メモ** ドライバーが*Timeout*パラメーターを**NULL**または0以外の値を含む変数のアドレスに設定して[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)を呼び出す場合、ドライバーは IRQL &lt;= APC\_レベルで実行されている必要があります。スレッドコンテキスト。 それ以外の場合、ドライバーは IRQL &lt;= ディスパッチ\_レベルで実行されている必要があります。




イベントは、IOCTL 要求が完了したときに[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンによって通知されます。 イベントがシグナル状態になると、スレッドは実行を再開します。

**重要** ドライバーがイベントオブジェクトをスタック上のローカル変数として割り当てる場合、ドライバーは、 *Waitmode*パラメーターを**kernelmode で**に設定して[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)を呼び出す必要があります。 このパラメーター値を指定すると、スタックがページアウトされなくなります。




同期の問題やアクセス違反の可能性を回避するために、i/o 制御コードのパラメーターには、埋め込みポインターが含まれることはほとんどありません。 特定の SCSI 要求を除き、 *Irp*-のバッファー&gt;**AssociatedIrp**です。**Systembuffer**、 *Irp*-&gt;**Mdladdress**、at**パラメーター**。**DeviceIoControl**。ドライバーの i/o スタックの場所の**Type3InputBuffer**には、他のデータバッファーへのポインターが含まれていません。また、システム定義の i/o 制御コードのポインターを含む構造体も含まれていません。 I/o 制御コードを含む Irp でデータバッファーを使用する方法の詳細については、「 [I/o 制御コードのバッファーの説明](buffer-descriptions-for-i-o-control-codes.md)」を参照してください。

それにもかかわらず、内部 i/o 制御コードを定義するクラス/ポートドライバーのペアは、ドライバーによって割り当てられたメモリへの埋め込みポインターを上位レベルのドライバーから下位レベルのドライバーに渡すことができます。 このようなクラス/ポートドライバーのペアは、次の条件を満たすことを保証する役割を担います。

-   データにアクセスできるドライバーは一度に1つだけです。

-   プライベートデータバッファーには、ポートドライバーによって任意のスレッドコンテキストでアクセスできます。

ディスプレイドライバーは、GDI 関数[**EngDeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol)を呼び出して、システムで定義されている、デバイス固有の i/o 制御要求、およびシステムで定義されているパブリック i/o 制御要求を、システムのビデオポートドライバーを介して、対応するアダプター固有の[ビデオミニポートドライバー](https://docs.microsoft.com/windows-hardware/drivers/display/video-miniport-drivers-in-the-windows-2000-display-driver-model)。

ドライバーパッケージのユーザーモードコンポーネントは、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)を呼び出して、ドライバースタックに i/o 制御要求を送信できます。 I/o マネージャーは、 [**IRP\_MJ\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求を作成し、それを最上位レベルのドライバーに配信します。








