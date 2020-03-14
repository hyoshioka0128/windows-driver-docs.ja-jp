---
title: 最下位レベル ドライバーでの IRP の処理
description: 最下位レベル ドライバーでの IRP の処理
ms.assetid: 9b8c2586-d47b-49ab-bf65-a298af36304c
keywords:
- Irp WDK カーネル、処理例
- Irp WDK カーネル、i/o 状態ブロック
- I/o ステータスが WDK カーネルをブロックする
- 状態は WDK カーネルをブロックします
- IoStartNextPacket
- IoCompleteRequest
- IoRequestDpc
- AllocateAdapterChannel
- MapTransfer
- IoStartPacket
- IoMarkIrpPending
- Iogetlocation Entiの場所
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26448d746e4e6e729f5cd254a0c3a612fbcdf4f0
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242949"
---
# <a name="processing-irps-in-a-lowest-level-driver"></a>最下位レベル ドライバーでの IRP の処理





最下位レベルの物理ドライバーには、上位レベルのドライバーが必要としない特定の標準ルーチンがあります。 最下位レベルのドライバーの標準ルーチンのセットも、次の条件によって異なります。

-   各ドライバーが制御するデバイスの性質

-   ドライバーが直接またはバッファー内の i/o のためにデバイスオブジェクトを設定するかどうか

-   個々のドライバーの設計

標準のドライバールーチンの役割を説明するために、次の図は、最小レベルの大容量記憶装置ドライバーによって処理されるときに、サンプルの IRP が実行する可能性のあるパスを示しています。 図のドライバーには、次の特性があります。

-   デバイスは各 i/o 操作の終了時に割り込みを生成するため、このドライバーには ISR ルーチンと[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチンがあります。

-   このドライバーには、Irp の内部キューを設定し、独自のキューを管理するのではなく、 [*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンがあります。

-   ドライバーはシステム DMA を使用するので、デバイスオブジェクトの**フラグ**をダイレクト i/o 用に設定し、 [*adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンを持っています。

![下位レベルのドライバールーチンを使用した irp パスを示す図](images/4loddirp.png)

この図に示すように、i/o マネージャーは IRP を作成し、指定された主要な関数コードのドライバーのディスパッチルーチンに送信します。 関数コードが[**irp\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)または[**irp\_MJ\_WRITE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)のいずれかであると仮定すると、ディスパッチルーチンは**DDDispatchReadWrite**です。

### <a name="calling-iogetcurrentirpstacklocation"></a>Iogetを呼び出しています。

IRP パラメーターを必要とするドライバールーチンでは、 [**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)を呼び出して、ドライバーの[i/o スタックの場所](i-o-stack-locations.md)を取得する必要があります。 このようなルーチンには、複数の主要 i/o 関数コード (<strong>IRP\_MJ\_* XXX</strong>) を処理するディスパッチルーチンが含まれ<em>ます。副関数 (</em><em>irp\_\_</em>XXX) をサポートしている関数、<strong><em>またはデバイス[</em>の I/O 制御要求 (* Irp\_MJ\_デバイス\_コントロール</strong>](<https://msdn.microsoft.com/library/windows/hardware/ff550744>)または[**irp\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)\_コントロール) を処理し、その他のすべてのドライバールーチンを irp を処理する関数を処理します。\_\_

このドライバーの i/o スタックの場所は、最も低いものであり、より高レベルのドライバーの i/o スタックの場所が影付きで表示されます。 わかりやすくするために、 [*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、 *StartIo*、 *adaptercontrol*、および[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)の各ルーチンから**ioget**を呼び出すための呼び出しは、前の図には記載されていません。

### <a name="calling-iomarkirppending-and-iostartpacket"></a>IoMarkIrpPending と IoStartPacket を呼び出しています

サンプルドライバーは、そのディスパッチルーチンで IRP を完了するのではなく、代わりに*StartIo*ルーチンで irp を処理します。 これを行う前に、ディスパッチルーチンは[**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出して、IRP がまだ完了していないことを示します。 次に、 [**Iostartpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)を呼び出して、ドライバーの*StartIo*ルーチンによる後続の処理のために IRP をキューに追加します。 また、ディスパッチルーチンは、NTSTATUS 値の状態\_PENDING を返します。

次の図は、 **Iostartpacket**の呼び出しを示しています。

![iostartpacket の呼び出しを示す図](images/4strtpak.png)

ドライバーがデバイス上の別の IRP を処理しているときに、デバイスオブジェクトに関連付けられているデバイスキューに IRP**が挿入さ**れます。 ドライバーは、必要に応じて**Iostartpacket**のパラメーターとして*キー*値を指定して、ドライバーによってデバイスキュー内の irp に対して順序を決定することができます。

ドライバーがビジーでなく、デバイスキューが空の場合、i/o マネージャーはすぐに*StartIo*ルーチンを呼び出し、入力 IRP を渡します。

大容量記憶装置の場合、最低レベルのドライバーでは、次の2つの理由で**Iostartpacket**を呼び出すときに[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンを指定する必要はありません。

1.  通常、このようなドライバーで階層化されたファイルシステムは、ファイル i/o 要求のキャンセルを処理します。

2.  大容量記憶装置ドライバーは、Irp を迅速に処理します。

通常、階層化されたドライバーのチェーンの最上位レベルのドライバーは、Irp のキャンセルを処理します。

### <a name="calling-allocateadapterchannel-and-maptransfer"></a>AllocateAdapterChannel と MapTransfer の呼び出し

下の図に示すように、最下位レベルのドライバールーチンを介した IRP パスを示す*StartIo*ルーチンが、転送要求を1つの DMA 操作で実行できることを確認した場合、 *StartIo*ルーチンは、ドライバーの*adaptercontrol*ルーチンと IRP のエントリポイントを使用して[**allocateadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)を呼び出します。

システム DMA コントローラーが使用可能な場合は、i/o マネージャーがドライバーの*Adaptercontrol*ルーチンを呼び出して転送操作を設定します。 *Adaptercontrol*ルーチンは、システム DMA コントローラーを設定するために[**maptransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)を呼び出します。 次に、ドライバーは DMA 操作用にデバイスをプログラムし、を返します。 (DMA とアダプタオブジェクトの使用方法の詳細については、「[入出力技法](i-o-programming-techniques.md)」を参照してください)。

### <a name="calling-iorequestdpc-from-the-drivers-isr"></a>ドライバーの ISR から IoRequestDpc を呼び出しています

転送操作が完了したことを示すためにデバイスが中断した場合、ドライバーの ISR は、デバイスが割り込みを生成しないようにし、 [**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc)を呼び出します。図に示すように、下位レベルのドライバールーチンによる IRP パスを示しています。

この呼び出しは、ドライバーの*DpcForIsr*ルーチンをキューに置いて、できるだけ低いハードウェア優先度 (IRQL) で、可能な限り多くの転送操作を完了します。

### <a name="calling-iostartnextpacket-and-iocompleterequest"></a>IoStartNextPacket と IoCompleteRequest を呼び出しています

*DpcForIsr*ルーチンが転送の処理を完了すると、デバイスキュー内の次の IRP でドライバーの*StartIo*ルーチンが呼び出されるように、 [**iostartnextpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)が即座に呼び出されます (キューに登録されている場合)。 また、 *DpcForIsr*ルーチンは、完了した irp の i/o 状態ブロックも設定し、Irp の[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出します。

次の図は、このドライバーによる**Iostartnextpacket**と**IoCompleteRequest**の呼び出しを示しています。

![iostartnextpacket と iocompleterequest を呼び出しています](images/4snxtpak.png)

ドライバーは、次に要求された i/o 操作をできるだけ早く開始するために、 **Iostartnextpacket**または[**Iostartnextpacketbykey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacketbykey)を呼び出す必要があります。可能であれば、 **IoCompleteRequest**を呼び出す前に行う必要があります。

デバイスの Irp がキューに登録されている場合、 **Iostartnextpacket**は[**Keremovedevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovedevicequeue)を呼び出して、キューから次の irp を削除します。 次に、i/o マネージャーは、デキューされた IRP を渡して、ドライバーの*StartIo*ルーチンを呼び出します。 現在デバイスキューに Irp が存在しない場合、 **Iostartnextpacket**は単に呼び出し元に戻ります。

### <a href="" id="ddk-setting-the-i-o-status-block-in-an-irp-kg"></a>IRP での i/o 状態ブロックの設定

すべての最下位レベルのドライバーは、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出す前に、IRP の[i/o 状態ブロック](i-o-status-blocks.md)を設定する必要があります。 (前の図では、2番目の影付き領域は状態ブロックを表しています)。I/o 状態ブロックは、上位レベルのドライバーに情報を提供し、最終的には i/o 操作の元の要求元に情報を渡します。 前の図のドライバーの上にある上位レベルのドライバーは、このドライバーによって設定された i/o 状態ブロックを読み取る[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定している可能性があります。 上位レベルのドライバーは、通常、デバイスドライバーによって完了された IRP 内の i/o 状態ブロックを変更しません。ただし、上位レベルのドライバーが IRP を再試行している場合は、i/o 状態ブロックが再初期化されます。

次に低いドライバーに送信せずに IRP を完了するすべての上位レベルのドライバーでは、 **IoCompleteRequest**を呼び出す前に、その irp の i/o 状態ブロックも設定する必要があります。 全体的な i/o スループットを向上させるには、上位レベルのドライバーで各 IRP の専用の i/o スタックの場所にあるパラメーターを確認し、パラメーターが無効な場合は i/o 状態ブロックを設定して要求自体を完了する必要があります。 可能な限り、ドライバーは、チェーン内の下位のドライバーに対して無効な要求を渡すことを避ける必要があります。

前の図の転送操作が成功したと仮定した場合、図に示されている*DpcForIsr*ルーチンは、最下位レベルのドライバールーチンを介した IRP パスを示しています **。状態が**[成功] に設定され、irp の I/o 状態ブロックの**情報**に転送されたバイト数が\_設定されます。

標準ドライバールーチンの多くは、NTSTATUS 型の値も返します。 ステータス\_成功などの NTSTATUS 定数の詳細については、「[ログエラー](logging-errors.md)」を参照してください。

 

 




