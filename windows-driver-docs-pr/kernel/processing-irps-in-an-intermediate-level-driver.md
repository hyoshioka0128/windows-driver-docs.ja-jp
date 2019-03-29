---
title: 中間レベル ドライバーでの IRP の処理
description: 中間レベル ドライバーでの IRP の処理
ms.assetid: 7606ab1b-68af-4d27-8668-7662969b85b8
keywords:
- Irp WDK カーネル、処理の例
- IoCompletion ルーチン
- IoSetCompletionRoutine
- ドライバー WDK Irp をミラー化します。
- Irp の割り当てください。
- 保留
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 507c38243eb92aabc1d81daa423eaafa0e52e361
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580921"
---
# <a name="processing-irps-in-an-intermediate-level-driver"></a>中間レベル ドライバーでの IRP の処理





上位レベルのドライバーでは、ドライバーの両方の種類に共通の標準的なルーチンの重複のサブセットを最下位レベルのデバイス ドライバーよりも標準のルーチンのさまざまなセットがあります。

ドライバーの中間と最上位レベルのルーチンのセットは、次の基準に従っても異なります。

-   基になる物理デバイスの種類

-   直接またはバッファー内の I/O のデバイス オブジェクトを基になるデバイスのドライバー設定かどうか

-   個々 のより高度なドライバーの設計

次の図は、中間の標準的なルーチンを IRP がかかる場合がありますパス*ミラー ドライバー*前のセクションで説明されている最下位レベルのデバイス ドライバーのどこかに上層します。

次の図に示すように、ドライバーでは、次の特徴があります。

-   ドライバーは、1 つ以上の物理デバイスおよび場合によっては、複数のデバイス ドライバーを介してに階層化されます。

-   ドライバーは IRP の入力で要求された操作によって、下位レベルのドライバーの場合があります追加 Irp を割り当てます。

-   ドライバーは、上の層に少なくとも 1 つのファイル システム ドライバーと、このより高いレベルでの他の中間ドライバー上層ファイル システム ドライバーがあります。

### <a href="" id="irp-path-through-intermediate-driver-routines"></a>

![中間ドライバー ルーチン経路は irp を示す図](images/4hiddirp.png)

図に示すように、I/O マネージャーは IRP を作成し、特定の主要な関数のコード用のドライバーのディスパッチ ルーチンに送信します。 関数のコードと仮定した場合は、 [ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819)、ディスパッチ ルーチンは**DDDispatchWrite**します。 中間のドライバーの I/O スタックの場所は、不特定数の網掛け表示より高いレベルと下位レベルのドライバーの I/O スタックの場所で、中央に表示されます。

### <a href="" id="allocating-irps-"></a>Irp の割り当てください。

ミラー ドライバーの目的は、いくつかの物理デバイスに書き込み要求を送信して、これらのデバイス ドライバーを代わりに読み取り要求を送信するにです。 書き込み要求の場合は、ドライバーは、IRP の入力パラメーターが有効であると仮定しているデータが書き込まれるデバイスごとに重複する Irp で作成します。

前の図への呼び出しを示しています。 [ **IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257)がより高度なドライバーは Irp を下位レベルのドライバーを割り当てることは、その他のサポート ルーチンを呼び出すことができます。 参照してください[Irp を作成する下位レベルのドライバーの](creating-irps-for-lower-level-drivers.md)します。

ディスパッチ ルーチンを呼び出すと**IoAllocateIrp**IRP の必要な I/O スタックの場所の数を指定します。 ドライバーは、ミラー ドライバーのすぐ下には、各ドライバーのデバイス オブジェクトから適切な値を取得する、一連の各下位のドライバーのスタックの場所を指定する必要があります。 必要に応じて、ドライバーを追加できますこの値を 1 つを呼び出すときに**IoAllocateIrp**前の図に、ドライバーは、割り当てる各の独自の IRP のスタックの場所を取得します。

この中間ドライバーのディスパッチ ルーチンの呼び出し[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174) (非表示) パラメーターをチェックする、元の IRP にします。

呼び出す[ **IoSetNextIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550321)それぞれに独自スタックの場所を新しく割り当てられたため、IRP を作成し、 [ **IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)自体で後で使用されるコンテキストを作成する、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチン。

次に、呼び出す[ **IoGetNextIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549266)各に新しく作成された IRP が割り当てた Irp では [次へ] の下位のドライバーの I/O スタックの場所を設定できるようにします。 ミラー ドライバーのディスパッチ ルーチン IRP 関数のコードとパラメーターのコピー (転送バッファーへのポインターの転送をバイト単位で長さ**IRP\_MJ\_書き込み**) に、I/O スタックの場所次の下位のドライバーです。 これらのドライバーでは、さらは設定のすぐ下に、ドライバー、I/O スタックの場所を存在する場合。

### <a name="calling-iosetcompletionroutine-and-iocalldriver"></a>呼び出し IoSetCompletionRoutine および保留

前の図の呼び出しのディスパッチ ルーチン[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)が割り当てた各 IRP の。 このドライバーの設定が割り当てた Irp の前の図に、ドライバーを破棄する必要があります、ため、その*IoCompletion*が正常に完了した I/O 操作に失敗するかどうか、下位のドライバーの Irp では、完了時に呼び出されるルーチンか、取り消されました。

[次へ] の下位レベルのドライバーに呼び出すことによって割り当てられた両方の Irp を渡すため、前の図に、ドライバーは、並列でミラー化[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336) 2 回、各ターゲット デバイスに 1 回ミラー化されたパーティションを表すオブジェクト。

### <a name="processing-irps-in-the-drivers-iocompletion-routine"></a>ドライバーの IoCompletion ルーチンに Irp の処理

I/O マネージャーが、中間のミラー ドライバーを呼び出してドライバーの下位レベルの両方のセットには、要求された操作が完了すると、 *IoCompletion*ルーチン。 ミラー ドライバーは下位のドライバーには、すべての重複する Irp が完了した時点を追跡するために、元の IRP の独自 I/O スタックの場所でカウントを保持します。

状態の I/O ブロックでは、1 つ下位のドライバーのセットでに示すように重複する IRP が完了したことを示します、[前の図](#irp-path-through-intermediate-driver-routines)、ミラー ドライバーの*IoCompletion*日常的なデクリメントのカウント完了できません。 元の IRP までデクリメントが、カウントがゼロにします。 減少数がまだ 0 でない場合、 *IoCompletion*ルーチンの呼び出し[ **IoFreeIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549113)最初に返された IRP に (前の図の DupIRP1) をドライバー割り当てられているし、ステータスを返します\_詳細\_処理\_必要な作業です。

ときに、ミラー ドライバーの*IoCompletion*ルーチンは、前の図に示す DupIRP2 でもう一度呼び出されます、 *IoCompletion*日常的なデクリメント IRP が元の数が判断したと両方要求された操作の下位レベルのドライバー セットが実行されます。

ステータスの設定も DupIRP2 で I/O のステータスのブロックと仮定すると\_成功した場合、 *IoCompletion*ルーチンが DupIRP2 から元の IRP に状態の I/O ブロックをコピーし、DupIRP2 を解放します。 呼び出す[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)元 IRP と状態を返します。\_詳細\_処理\_必須。 この状態を返すしないように I/O マネージャー DupIRP2; で処理をさらに補完IRP はスレッドに関連付けられていないため、それを作成したドライバーを使用した完了処理を終了する必要があります。

下位レベルのドライバーの両方のセットがミラー ドライバーの Irp を正常に完了しない場合、ミラー ドライバーの*IoCompletion*ルーチンがエラーと試行の適切なのミラー化されたデータ回復にログインする必要があります。 詳細については、次を参照してください。[ログ エラー](logging-errors.md)します。

 

 




