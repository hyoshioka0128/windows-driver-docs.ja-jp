---
title: ドライバー内での IOCTL 要求の作成
description: ドライバー内での IOCTL 要求の作成
ms.assetid: 155e2577-0e9a-4c0b-a25a-8516ce3de631
keywords:
- 要求の作成、I/O 制御コード WDK カーネル
- 制御コード WDK Ioctl、要求の作成
- Ioctl WDK カーネル、要求の作成
- WDK Irp の同期
- 埋め込みポインター WDK Ioctl
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 883fe8d9b2d45fb88fce154f06eeb6f52f3e6a7d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377156"
---
# <a name="creating-ioctl-requests-in-drivers"></a>ドライバー内での IOCTL 要求の作成





クラス ドライバーまたはその他の高度なドライバーは Irp をコントロールの I/O 要求を割り当てるし、次のように、次の下位ドライバーに送信。

1.  割り当てまたは I/O 要求パケットを再利用 ([**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)) メジャーの関数コードで[ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)または[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)します。 使用することができます、 [ **IoBuildDeviceIoControlRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)ルーチンを具体的には、IOCTL IRP を割り当てます。 など、汎用的な IRP の作成と初期化ルーチンを使用することもできます[ **IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)、 [ **IoReuseIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreuseirp)、または。[**IoInitializeIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializeirp)します。 IRP の割り当ての詳細については、次を参照してください。[下位レベルのドライバーの作成の Irp](creating-irps-for-lower-level-drivers.md)します。

2.  IOCTL で IRP の下位のドライバーの I/O スタックの場所を設定\_*XXX*パラメーターを適切なコードをしています。

3.  IOCTL 要求を非同期的に完了する場合は、呼び出し、 [ **KeInitializeEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializeevent)ルーチンを通知イベントとイベント オブジェクトを初期化します。 ドライバーでは、このイベントを使用して、I/O 操作を完了するまで待ちます。

4.  呼び出す[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine) IRP が上のドライバーが提供できるように、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチン、必要に応じて、実行するには次:

    -   下位のドライバーが、特定の要求を処理する方法を決定します。

    -   IRP 別の送信を要求または下位のドライバーが要求された操作が完了したら破棄 IRP がドライバーを作成、再利用します。 ドライバーは Irp を再利用できませんを[ **IoBuildDeviceIoControlRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)を作成します。 詳細については、次を参照してください。 [Irp の再利用](reusing-irps.md)します。

5.  呼び出す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)から下位のドライバーに要求を渡します。

6.  場合[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)ステータスを返します\_保留中の呼び出し、 [ **kewaitforsingleobject の 1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)ルーチンを現在の配置スレッド待機状態にします。 ドライバーの設定、ルーチンの*オブジェクト*パラメーターへの呼び出しで初期化されたイベント オブジェクトのアドレスを[ **KeInitializeEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializeevent)します。

    **注**ドライバーを呼び出す場合[ **kewaitforsingleobject の 1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)でその*タイムアウト*パラメーターはいずれかに設定**NULL**または、ドライバー、0 以外の値を格納する変数のアドレスは、IRQL で実行する必要があります&lt;APC を =\_nonarbitrary スレッド コンテキストでします。 IRQL でドライバーを実行する必要がありますそれ以外の場合、 &lt;= ディスパッチ\_レベル。




によって、イベントがシグナル状態その[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチン IOCTL 要求が完了するとします。 イベントがシグナル状態のスレッドが実行を再開します。

**重要な**、ドライバーが、スタック上のローカル変数として、イベント オブジェクトを割り当てた場合、ドライバーを呼び出す必要があります[ **kewaitforsingleobject の 1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)でその*WaitMode*パラメーターに設定**kernelmode である**します。 このパラメーターの値は、スタックがページ アウトされていることを防ぎます。




同期の問題と可能なアクセス違反を避けるため、I/O 制御コードのパラメーターには、埋め込みポインターにはほとんどが含まれます。 特定の SCSI の要求でバッファーを除く*Irp*-&gt;**AssociatedIrp**.**SystemBuffer**で*Irp*-&gt;**MdlAddress**、および**パラメーター**.**DeviceIoControl**.**Type3InputBuffer**ドライバーの I/O スタック内の場所にが含まれていないその他のデータ バッファーへのポインターにはも I/O 制御コードのシステム定義のポインターを格納する構造体を格納しないでください。 I/O の Irp でのデータ バッファーの使用方法の詳細については、制御コードを参照してください[I/O 制御コードの説明をバッファー](buffer-descriptions-for-i-o-control-codes.md)します。

それにもかかわらず、内部の I/O 制御コードを定義するクラス/ポート ドライバーのペアは、下位レベルのドライバーにより高度なドライバーから、ドライバーによって割り当てられたメモリに埋め込みポインターを渡すことができます。 クラス/ポート ドライバーのようなペアは、次が true であることを保証します。

-   一度に 1 つだけのドライバーは、データにアクセスできます。

-   プライベート データ バッファーは、ポート ドライバーによって任意のスレッド コンテキストでアクセスできます。

ディスプレイ ドライバーは、GDI 関数を呼び出すことができます[ **EngDeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol)を介してシステム定義されたパブリック I/O 制御要求と同様に、個別に定義されたデバイスに固有の I/O 制御の要求を送信する、対応するアダプター固有のシステムのビデオ ポート ドライバー[ビデオのミニポート ドライバー](https://docs.microsoft.com/windows-hardware/drivers/display/video-miniport-drivers-in-the-windows-2000-display-driver-model)します。

ドライバー パッケージのすべてのユーザー モード コンポーネントを呼び出すことができます[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)ドライバー スタックにコントロールの I/O 要求を送信します。 I/O マネージャーを作成、 [ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)を要求し、最上位レベルのドライバーに配信します。








