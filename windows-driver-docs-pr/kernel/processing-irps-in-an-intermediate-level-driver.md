---
title: 中間レベル ドライバーでの IRP の処理
description: 中間レベル ドライバーでの IRP の処理
ms.assetid: 7606ab1b-68af-4d27-8668-7662969b85b8
keywords:
- Irp WDK カーネル、処理例
- IoCompletion ルーチン
- Ioset補完ルーチン
- ミラードライバー WDK Irp
- Irp の割り当て
- IoCallDriver
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2612e02918ec2128f1535bd0aa88e25be2a0c7ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838491"
---
# <a name="processing-irps-in-an-intermediate-level-driver"></a>中間レベル ドライバーでの IRP の処理





上位レベルのドライバーは、最下位レベルのデバイスドライバーとは異なる標準ルーチンのセットを備えており、両方の種類のドライバーに共通する標準ルーチンのサブセットが重複しています。

中間レベルと最高レベルのドライバーの一連のルーチンも、次の条件によって異なります。

-   基になる物理デバイスの性質

-   基になるデバイスドライバーが直接またはバッファー内の i/o 用にデバイスオブジェクトを設定するかどうか

-   上位レベルの個々のドライバーの設計

次の図は、前のセクションで説明した最下位レベルのデバイスドライバーのどこかにある中間の*ミラードライバー*の標準ルーチンを使用して、IRP が実行するパスを示しています。

次の図に示すドライバーには、次の特性があります。

-   このドライバーは、複数の物理デバイスと、場合によっては複数のデバイスドライバーによって階層化されます。

-   ドライバーは、入力 IRP で要求された操作に応じて、下位レベルのドライバーに対して追加の Irp を割り当てることがあります。

-   ドライバーには、ファイルシステムドライバーが少なくとも1つ含まれています。また、このファイルシステムドライバーは、より高いレベルの他の中間ドライバーの上に階層化されている可能性があります。

### <a href="" id="irp-path-through-intermediate-driver-routines"></a>

![中間ドライバールーチンによる irp パスを示す図](images/4hiddirp.png)

図に示すように、i/o マネージャーは IRP を作成し、指定された主要な関数コードのドライバーのディスパッチルーチンに送信します。 関数コードが[**IRP\_MJ\_WRITE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)であると仮定すると、ディスパッチルーチンは**DDDispatchWrite**になります。 中間ドライバーの i/o スタックの場所は、中央に表示され、上位レベルと下位レベルのドライバーに対しては不定な数の i/o スタックの場所が表示されます。

### <a href="" id="allocating-irps-"></a>Irp の割り当て

ミラードライバーの目的は、複数の物理デバイスに書き込み要求を送信し、これらのデバイスのドライバーに読み取り要求を送信することです。 書き込み要求の場合、ドライバーは、入力 IRP 内のパラメーターが有効であると仮定して、データが書き込まれる各デバイスに対して重複する Irp を作成します。

前の図は、 [**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)の呼び出しを示していますが、上位レベルのドライバーは他のサポートルーチンを呼び出して下位レベルのドライバーに対して irp を割り当てることができます。 「[下位レベルのドライバーの irp を作成する」を](creating-irps-for-lower-level-drivers.md)参照してください。

ディスパッチルーチンが**Ioallocateirp**を呼び出すと、IRP に必要な i/o スタックの場所の数が指定されます。 ドライバーは、チェーン内の下位のドライバーごとにスタックの場所を指定する必要があります。これにより、各ドライバーのデバイスオブジェクトから、ミラードライバーのすぐ下に適切な値が取得されます。 必要に応じて、ドライバーは**Ioallocateirp**を呼び出すときにこの値に1つを追加して、前の図のドライバーと同じように、割り当てられた各 IRP に対して独自のスタック位置を取得することができます。

この中間ドライバーのディスパッチルーチンは、パラメーターをチェックするために、元の IRP で[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)を呼び出します (非表示)。

新たに作成された各 IRP と[**Iogetcompletion Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)に独自のスタックの場所が割り当てられ、後で[*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンで使用されるコンテキストが作成されるため、 [**iosetnextiシャー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetnextirpstacklocation)ドの場所を呼び出します。

次に、新しく作成された各 IRP で[**Iogetnextiシャー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)ドの場所を呼び出します。これにより、割り当てられた irp で次の下位レベルのドライバーの i/o スタックの場所を設定できるようになります。 ミラードライバーのディスパッチルーチンによって、IRP 関数のコードとパラメーター ( **irp\_MJ\_書き込み**用に転送されるバイト数) が、次に低いドライバーの i/o スタックの場所にコピーされます。 これらのドライバーは、そのすぐ下にあるドライバーの i/o スタックの場所を設定します (存在する場合)。

### <a name="calling-iosetcompletionroutine-and-iocalldriver"></a>IosetIoCallDriver ルーチンとの呼び出し

前の図のディスパッチルーチンは、割り当てられた各 IRP に対して[**Ioset補完ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出します。 前の図のドライバーは、割り当てられた Irp を破棄する必要があるため、このドライバーは、低いドライバーが Irp を完了したとき、i/o 操作が正常に完了したか、失敗したか、取り消されたかにかかわらず、その*Iocompletion*ルーチンが呼び出されるように設定します。

前の図のドライバーは並列でミラー化されているため、ミラー化されたパーティションを表すターゲットデバイスオブジェクトごとに1回、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を2回呼び出して、次の下位レベルのドライバーに割り当てられた両方の irp を渡します。

### <a name="processing-irps-in-the-drivers-iocompletion-routine"></a>ドライバーの IoCompletion ルーチンでの Irp の処理

下位レベルのドライバーのいずれかのセットで要求された操作が完了すると、i/o マネージャーは中間ミラードライバーの*Iocompletion*ルーチンを呼び出します。 ミラードライバーでは、元の IRP に対する専用の i/o スタック位置にカウントが保持されます。これにより、下位のドライバーが複製されたすべての Irp を完了したことが追跡されます。

I/o 状態ブロックによって、[前の図](#irp-path-through-intermediate-driver-routines)に示した複製された IRP が、下位のドライバーの1つのセットによって完了したことが示された場合、ミラードライバーの*iocompletion*ルーチンはそのカウントをデクリメントしますが、元の irp を完了できません。カウントを0にデクリメントします。 デクリメントされたカウントがまだゼロでない場合、 *Iocompletion*ルーチンは、ドライバーによって割り当てられた最初に返された IRP (前の図では DupIRP1) を使用\_\_して[**Iofreeirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)を呼び出し\_必須。

前の図に示されている DupIRP2 を使用して、ミラードライバーの*Iocompletion*ルーチンが再度呼び出されると、 *iocompletion*ルーチンは元の IRP のカウントをデクリメントし、下位レベルのドライバーの両方のセットが実行されていることを確認します。要求された操作。

DupIRP2 の i/o 状態ブロックも STATUS\_SUCCESS に設定されていると仮定した場合、 *Iocompletion*ルーチンは DupIRP2 から元の IRP に i/o 状態ブロックをコピーし、DupIRP2 を解放します。 元の IRP を使用して[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出し、\_必要な\_処理をより多くの状態\_返します。 この状態を返すと、i/o マネージャーは、DupIRP2 でそれ以上の完了処理を試行できなくなります。IRP はスレッドに関連付けられていないため、完了処理は、それを作成したドライバーで終了する必要があります。

下位レベルのドライバーのいずれかのセットがミラードライバーの Irp を正常に完了しない場合、ミラードライバーの*Iocompletion*ルーチンはエラーをログに記録し、適切なミラー化されたデータの回復を実行します。 詳細については、「[エラーのログ記録](logging-errors.md)」を参照してください。

 

 




