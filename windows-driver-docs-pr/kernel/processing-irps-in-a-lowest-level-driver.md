---
title: 最下位レベル ドライバーでの IRP の処理
description: 最下位レベル ドライバーでの IRP の処理
ms.assetid: 9b8c2586-d47b-49ab-bf65-a298af36304c
keywords:
- Irp WDK カーネル、処理の例
- Irp WDK カーネルでは、I/O の状態のブロック
- I/O 状態ブロック WDK カーネル
- 状態ブロックの WDK カーネル
- います
- IoCompleteRequest
- IoRequestDpc
- AllocateAdapterChannel
- MapTransfer
- IoStartPacket
- IoMarkIrpPending
- IoGetCurrentIrpStackLocation
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2af990ffb007eaa2070157c3864de358198ac32c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378829"
---
# <a name="processing-irps-in-a-lowest-level-driver"></a>最下位レベル ドライバーでの IRP の処理





最下位レベルの物理的なドライバーより高度なドライバーが不要な特定の標準的なルーチンがあります。 最下位レベルのドライバーに対して標準的なルーチンのセットは、次の基準に従っても異なります。

-   各ドライバーを制御するデバイスの種類

-   直接またはバッファー内の I/O オブジェクトをそのデバイス ドライバーを設定するかどうか

-   個々 のドライバーの設計

標準のドライバーのルーチンのロールを示すためには、次の図は、パスを IRP が最下位レベルの大容量記憶装置ドライバーでは、処理にかかる場合があるサンプルに示します。 図に、ドライバーでは、次の特徴があります。

-   デバイスには、各 I/O 操作の最後に割り込みが生成されるので、このドライバーは ISR と[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)ルーチン。

-   ドライバーは、 [ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチンではなく Irp の内部キューの設定と、独自のキューを管理します。

-   そのデバイス オブジェクトを設定するため、ドライバーはシステム、DMA を使用して**フラグ**ダイレクト i/o であり、 [ *AdapterControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control)ルーチン。

![最下位レベルのドライバーのルーチンを irp のパスを示す図](images/4loddirp.png)

この図に示す、I/O マネージャーは IRP を作成し、特定の主要な関数のコード用のドライバーのディスパッチ ルーチンに送信します。 いずれかと仮定すると、関数コードが[ **IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)または[ **IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)、ディスパッチ ルーチンは**DDDispatchReadWrite**します。

### <a name="calling-iogetcurrentirpstacklocation"></a>IoGetCurrentIrpStackLocation を呼び出す

IRP パラメーターが必要なドライバーのルーチンを呼び出す必要があります[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)ドライバーの入手[I/O スタックの場所](i-o-stack-locations.md)します。 このようなルーチンには、1 つ以上の主要な I/O 関数コードを処理するディスパッチ ルーチン (<strong>IRP\_MJ\_* XXX</strong><em>)、マイナー機能をサポートする関数の処理 (</em> <em>IRP\_MN\_</em>XXX<strong><em>)、またはデバイス I/O 制御要求の処理 ([</em>* IRP\_MJ\_デバイス\_制御</strong>](<https://msdn.microsoft.com/library/windows/hardware/ff550744>)や[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control))、と共にすべてIRP の処理の他のドライバー ルーチンです。

このドライバーの I/O スタックの場所は、最低 1 つの不特定数の上位レベルのドライバーの網掛け表示 I/O スタックの場所を使用します。 わかりやすくするため、呼び出し**IoGetCurrentIrpStackLocation**から、 [ *DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)、 *StartIo*、 *AdapterControl*、および[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)ルーチンは、上記の図に表示されません。

### <a name="calling-iomarkirppending-and-iostartpacket"></a>IoMarkIrpPending および IoStartPacket の呼び出し

サンプル ドライバーは、ディスパッチ ルーチン内の IRP が完了しないが、代わりにで IRP を処理、 *StartIo*ルーチン。 これを行う前に、ディスパッチ ルーチンを呼び出す[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)を IRP が完了していないことを示します。 呼び出して[ **IoStartPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket) IRP がドライバーのによってさらに処理をキューに*StartIo*ルーチン。 ディスパッチ ルーチンも NTSTATUS 値の状態を返します\_保留します。

次の図への呼び出しを示しています。 **IoStartPacket**します。

![iostartpacket への呼び出しを示す図](images/4strtpak.png)

ドライバーが、デバイス上の別の IRP の処理でビジー状態の場合**IoStartPacket** IRP をデバイス オブジェクトに関連付けられているデバイスのキューに挿入します。 必要に応じて、ドライバーを指定できます、*キー*へのパラメーターとして値**IoStartPacket**デバイスのキューの Irp でのドライバーにより決定された順序を強制します。

I/O マネージャーがすぐに呼び出し、ドライバーがビジー状態ではなく、デバイスのキューが空場合は、その*StartIo*ルーチン、IRP の入力を渡します。

大容量記憶装置デバイスの場合は、最下位レベルのドライバーを指定する必要ありません、 [*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)ルーチンを呼び出すときに**IoStartPacket** 2 つの理由。

1.  このようなドライバーの上層に通常のファイル システムでは、ファイル I/O 要求のキャンセルを処理します。

2.  大容量記憶装置デバイス ドライバーは Irp を迅速に処理します。

通常、複数層のドライバーのチェーンの最上位レベルのドライバーは Irp のキャンセルを処理します。

### <a name="calling-allocateadapterchannel-and-maptransfer"></a>AllocateAdapterChannel および MapTransfer の呼び出し

仮定すると、 *StartIo*最下位レベルのドライバーのルーチンを IRP のパスを示すには、転送要求を 1 つの DMA 操作を行うことが決定しますの図のように、日常的な*StartIo*ルーチンの呼び出し[ **AllocateAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel)ドライバーのエントリ ポイントで*AdapterControl*ルーチンと IRP します。

システムの DMA コント ローラーを使用できる I/O マネージャー呼び出し、ドライバーの*AdapterControl*転送操作で転送を設定するルーチン。 *AdapterControl*ルーチンの呼び出し[ **MapTransfer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pmap_transfer)システム DMA コント ローラーを設定します。 ドライバーはそのデバイス DMA 操作をプログラムし、返します。 (詳細については、DMA とアダプター オブジェクトを使用して、次を参照してください[入力/出力手法](i-o-programming-techniques.md)。)。

### <a name="calling-iorequestdpc-from-the-drivers-isr"></a>ドライバーから IoRequestDpc を呼び出す ISR

デバイスの割り込みをその転送操作の完了を示すために、ドライバーの ISR 停止、デバイスからの割り込みおよび呼び出し生成[ **IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iorequestdpc)図の説明のように、最下位レベルのドライバーのルーチンを IRP のパス。

この呼び出しはキュー、ドライバーの*DpcForIsr*ルーチンをできるだけ低いハードウェア優先順位 (IRQL) で転送操作の多くの部分を完了します。

### <a name="calling-iostartnextpacket-and-iocompleterequest"></a>いますおよび IoCompleteRequest の呼び出し

ときに、 *DpcForIsr*ルーチンには、転送の処理が完了しました、呼び出す[**います**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)迅速にできるように、ドライバーの*StartIo*いずれかがキューに置かれた場合にそのルーチンがデバイスのキューで [次へ] の IRP で呼び出されます。 *DpcForIsr*ルーチンも完了したばかりの IRP の I/O の状態のブロックを設定し、呼び出します[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) IRP の。

次の図は、このドライバーの呼び出しを**います**と**IoCompleteRequest**します。

![呼び出し元のいます、iocompleterequest](images/4snxtpak.png)

ドライバーを呼び出す必要があります**います**または[ **IoStartNextPacketByKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacketbykey) [次へ] を開始する要求された I/O 操作をできるだけ早く可能であれば呼び出しの前に**IoCompleteRequest**します。

デバイスの任意の Irp がキューに置かれた場合**います**呼び出し[ **KeRemoveDeviceQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keremovedevicequeue) IRP が [次へ] をキューから削除します。 I/O マネージャーを呼び出してドライバーの*StartIo*ルーチン、キューから取り出された IRP を渡します。 Irp 現在存在しない場合、デバイスのキューで**います**だけで、呼び出し元に返します。

### <a href="" id="ddk-setting-the-i-o-status-block-in-an-irp-kg"></a>IRP の状態の I/O ブロックの設定

最下位レベルのすべてのドライバーは IRP を設定する必要があります[状態の I/O ブロック](i-o-status-blocks.md)呼び出す前に[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)します。 (前の図に、2 つ目の網掛けを表します状態ブロック。)状態の I/O ブロックより高度なドライバーと、最終的は、I/O 操作の元の要求者の情報を提供します。 前の図に、ドライバーの上に配置されたより高度なドライバーを設定することがありますが、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)状態の I/O ブロックを読み取るルーチンは、このドライバーで設定します。 通常より高度なドライバーにはデバイス ドライバーによって完了されたより高度なドライバーはで、再試行の IRP では、その場合はしない限り、状態の I/O ブロックを再初期化する IRP の I/O 状態ブロック変更しません。

[次へ] の下位のドライバーに送信する I/O の状態を設定する必要がありますもせずに IRP が完了するとすべての高度なドライバーを呼び出す前にその IRP でブロック**IoCompleteRequest**します。 全体的な I/O スループットの高いより高度なドライバー各 IRP の独自 I/O スタックの場所では、パラメーターを確認する必要があり場合パラメーターが有効でない必要があります状態の I/O ブロックの設定自体、要求を完了します。 可能であれば、ドライバーは、チェーン内の下位のドライバーに無効な要求を渡すことを避ける必要があります。

前の図の転送操作が成功したと仮定すると、 *DpcForIsr*の図のように、日常的な状態を設定最下位レベルのドライバーのルーチンからの IRP パスを示す、\_で成功**状態**で転送されたバイト数と**情報**IRP の I/O の状態のブロックにします。

標準のドライバーのルーチンの多くも NTSTATUS 型の値を返します。 NTSTATUS 定数状態などの詳細については\_成功するを参照してください[ログ エラー](logging-errors.md)します。

 

 




