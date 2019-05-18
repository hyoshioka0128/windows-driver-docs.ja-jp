---
title: SerCx2 システム-DMA-送信トランザクション
description: 一部のコント ローラーのシリアル ドライバーのサポートを実装するシステムの DMA コント ローラーを使用するトランザクションを送信します。
ms.assetid: 8569E76F-CAFF-4A2C-8052-62B340C5ADED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6173739032750c41945190fc86e2f33745dea019
ms.sourcegitcommit: 6a0636c33e28ce2a9a742bae20610f0f3435262c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2019
ms.locfileid: "65836321"
---
# <a name="sercx2-system-dma-transmit-transactions"></a>SerCx2 システム-DMA-送信トランザクション

一部のコント ローラーのシリアル ドライバーのサポートを実装するシステムの DMA コント ローラーを使用するトランザクションを送信します。 このようなサポートは任意ですが、長い形式のデータ転送に下手順 I/O (PIO) を使用する必要があるメイン プロセッサを削減してパフォーマンスを向上させることができます。 SerCx2 では、システムの DMA コント ローラーを設定し、コント ローラーのシリアル ドライバーの代わりに必要な DMA 転送を開始してシステム DMA 送信トランザクションを実行します。

シリアル コント ローラー ドライバーがシステム DMA 送信オブジェクトを作成する場合、ドライバーは SerCx2 がシステム DMA 送信トランザクション システム DMA アダプターの設定に使用するパラメーターを提供します。

シリアル コント ローラー ドライバーでは、トランザクションの開始前に、シリアル コント ローラーのハードウェアまたはトランザクションに必要な可能性のある DMA アダプターのすべての特別な設定を行うオプションがあります。 ドライバーに送信、FIFO のドレインを実行するためのオプションは、トランザクションが完了後し、必要に応じて、シリアル コント ローラーのハードウェアの状態をクリーンアップします。

## <a name="creating-the-system-dma-transmit-object"></a>システム DMA 送信オブジェクトを作成します。

SerCx2 がコント ローラーのシリアル ドライバーを呼び出す前に*EvtSerCx2SystemDmaTransmit*Xxx * * 関数の場合、ドライバーが呼び出す必要があります、 [ **SerCx2SystemDmaTransmitCreate** ](https://msdn.microsoft.com/library/windows/hardware/dn265288)SerCx2 をこれらの関数を登録するメソッド。 このメソッドは、入力パラメーターとしてへのポインターを[ **SERCX2\_システム\_DMA\_送信\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/dn265344)を含む構造体ドライバーへのポインター *EvtSerCx2SystemDmaTransmit*Xxx * * 関数。

オプションとして、ドライバーは、次の関数の一部またはすべてを実装できます。

- [*EvtSerCx2SystemDmaTransmitInitializeTransaction*](https://msdn.microsoft.com/library/windows/hardware/dn265237)
- [*EvtSerCx2SystemDmaTransmitCleanupTransaction*](https://msdn.microsoft.com/library/windows/hardware/dn265234)
- [*EvtSerCx2SystemDmaTransmitConfigureDmaChannel*](https://msdn.microsoft.com/library/windows/hardware/dn265235)

オプションとして、ドライバーは、次の関数を実装できます。

- [*EvtSerCx2SystemDmaTransmitDrainFifo*](https://msdn.microsoft.com/library/windows/hardware/dn265236)
- [*EvtSerCx2SystemDmaTransmitCancelDrainFifo*](https://msdn.microsoft.com/library/windows/hardware/dn265233)
- [*EvtSerCx2SystemDmaTransmitPurgeFifo*](https://msdn.microsoft.com/library/windows/hardware/dn265238)

上記の一覧で任意の関数を実装するドライバーは、3 つすべてを実装する必要があります。

**SerCx2SystemDmaTransmitCreate**メソッドは、システム DMA 送信オブジェクトを作成し、呼び出し元のドライバーを提供する[ **SERCX2SYSTEMDMATRANSMIT** ](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-object-handles#sercx2systemdmatransmit-object-handle)これへのハンドルオブジェクト。 ドライバーの*EvtSerCx2SystemDmaTransmit*Xxx * * すべての関数は、最初のパラメーターとしてこのハンドルを受け取ります。 次の SerCx2 メソッドは、最初のパラメーターとして、このハンドルを受け取ります。

- [**SerCx2SystemDmaTransmitDrainFifoComplete**](https://msdn.microsoft.com/library/windows/hardware/dn265289)
- [**SerCx2SystemDmaTransmitPurgeFifoComplete**](https://msdn.microsoft.com/library/windows/hardware/dn265307)
- [**SerCx2SystemDmaTransmitInitializeTransactionComplete**](https://msdn.microsoft.com/library/windows/hardware/dn265306)
- [**SerCx2SystemDmaTransmitCleanupTransactionComplete**](https://msdn.microsoft.com/library/windows/hardware/dn265286)
- [**SerCx2SystemDmaTransmitGetDmaEnabler**](https://msdn.microsoft.com/library/windows/hardware/dn265305)

## <a name="hardware-initialization-and-clean-up"></a>ハードウェアの初期化とクリーンアップ

シリアル コント ローラーのドライバーによっては、システム DMA 送信トランザクションの開始時シリアル コント ローラーのハードウェアを初期化するために、またはトランザクションの最後に、シリアル コント ローラーのハードウェアの状態をクリーンアップする必要があります。

ドライバーが実装されている場合、 [ *EvtSerCx2SystemDmaTransmitInitializeTransaction* ](https://msdn.microsoft.com/library/windows/hardware/dn265237)イベント コールバック関数、SerCx2 がシリアル コント ローラーを最初の DMA を開始する前に初期化するには、この関数を呼び出すトランザクションで転送します。 実装されている場合、 *EvtSerCx2SystemDmaTransmitInitializeTransaction*関数を呼び出す必要があります、 [ **SerCx2SystemDmaTransmitInitializeTransactionComplete** ](https://msdn.microsoft.com/library/windows/hardware/dn265306)ドライバーでは、シリアル コント ローラーの初期化が完了すると、SerCx2 を通知するメソッドです。

ドライバーが実装されている場合、 [ *EvtSerCx2SystemDmaTransmitCleanupTransaction* ](https://msdn.microsoft.com/library/windows/hardware/dn265234)イベント コールバック関数では、SerCx2 が最終的な DMA 転送の終了後にハードウェアの状態をクリーンアップするには、この関数を呼び出すトランザクション。 実装されている場合、 *EvtSerCx2SystemDmaTransmitInitializeTransaction*関数を呼び出す必要があります、 [ **SerCx2SystemDmaTransmitCleanupTransactionComplete** ](https://msdn.microsoft.com/library/windows/hardware/dn265286)メソッドドライバーでは、シリアル コント ローラーのクリーンアップが完了すると、SerCx2 を通知します。

システムの DMA コント ローラー システム DMA 送信トランザクションの開始時の特別な構成を行う必要があるシリアル コント ローラー ドライバーが実装する必要があります、 [ *EvtSerCx2SystemDmaTransmitConfigureDmaChannel*](https://msdn.microsoft.com/library/windows/hardware/dn265235)イベント コールバック関数。 この関数を呼び出すことができます、 [ **SerCx2SystemDmaTransmitGetDmaEnabler** ](https://msdn.microsoft.com/library/windows/hardware/dn265305)トランザクションに使用されるシステム DMA アダプターの DMA イネーブラーを取得します。 SerCx2 は、トランザクションの最初の DMA 転送を開始する前に、この関数を呼び出します。 DMA イネーブラーに関する詳細については、次を参照してください。 [DMA のトランザクションを有効にする](https://msdn.microsoft.com/library/windows/hardware/ff540818)します。

## <a name="draining-and-purging-the-transmit-fifo"></a>ドレインと送信の FIFO の削除

システム DMA 送信トランザクションをサポートしているシリアル コント ローラー ドライバーが実装する必要があります、 [ *EvtSerCx2SystemDmaTransmitDrainFifo* ](https://msdn.microsoft.com/library/windows/hardware/dn265236)ときに、ドライバーが検出された場合に、イベント コールバック関数、FIFO 空のデータを送信します。 実装されている場合、SerCx2 は、FIFO の送信にシステムの DMA-送信トランザクション内のデータの最後のバイトが書き込まれた後、この関数を呼び出します。 この呼び出し中に、 *EvtSerCx2SystemDmaTransmitDrainFifo*関数は割り込み送信 FIFO を空に、ときにトリガーされると返しますを通常使用すると、割り込みを待つことがなく。 FIFO を空に、ドライバーが呼び出し、 [ **SerCx2SystemDmaTransmitDrainFifoComplete** ](https://msdn.microsoft.com/library/windows/hardware/dn265289) SerCx2 に通知するメソッド。 この通知を受信した後にのみが SerCx2 完了保留中の書き込み ([**IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff546904))、システムの DMA の転送に関連付けられている要求トランザクションです。

シリアル コント ローラー ドライバーが実装していない場合、 *EvtSerCx2SystemDmaTransmitDrainFifo*関数、SerCx2 する必要があります保留中の書き込みの要求を完了せず、送信 FIFO を空にすることを確認しています。 大幅な遅延なし、FIFO に書き込まれたデータが送信されることの保証はできません。 送信できる前に、書き込み要求が完了した後、FIFO に残っているすべてのデータは失われます。 この予期しないデータの損失を正常に完了した書き込み要求では、要求を送信した周辺のドライバーの信頼性の問題を作成できます。

実装するドライバー、 *EvtSerCx2SystemDmaTransmitDrainFifo*関数を実装する必要がありますも[ *EvtSerCx2SystemDmaTransmitCancelDrainFifo* ](https://msdn.microsoft.com/library/windows/hardware/dn265233)と[ *EvtSerCx2SystemDmaTransmitPurgeFifo* ](https://msdn.microsoft.com/library/windows/hardware/dn265238)イベント コールバック関数。

*EvtSerCx2SystemDmaTransmitCancelDrainFifo*関数が完了する前に、実行中の FIFO ドレイン操作をキャンセルする SerCx2 を有効にします。 SerCx2 は、書き込み要求が取り消された場合、またはシリアル コント ローラーを低電力状態に入ろう D0 デバイスの電源状態を終了する場合、この操作を取り消すことがあります。 場合、 *EvtSerCx2SystemDmaTransmitCancelDrainFifo* FIFO ドレイン操作が正常にキャンセルする関数と、この関数を返します**TRUE**します。 戻り値**TRUE**に必ず、 *EvtSerCx2SystemDmaTransmitDrainFifo*関数は、先に呼び出すことがなく返します**SerCx2SystemDmaTransmitDrainFifoComplete**. 戻り値**FALSE**ことを示します、 *EvtSerCx2SystemDmaTransmitDrainFifo*関数が呼び出されてまたは呼び出す**SerCx2SystemDmaTransmitDrainFifoComplete**します。

システム DMA 送信トランザクションに関連付けられた書き込み要求が取り消されたまたは時刻を完了前に SerCx2 を呼び出す場合、 *EvtSerCx2SystemDmaTransmitPurgeFifo*関数を実装すると、すべての未送信を破棄する場合データ送信 FIFO が残る可能性があります。 FIFO が削除されたとき、 *EvtSerCx2SystemDmaTransmitPurgeFifo*関数呼び出し、 [ **SerCx2SystemDmaTransmitPurgeFifoComplete** ](https://msdn.microsoft.com/library/windows/hardware/dn265307) SerCx2 に通知するメソッド。 SerCx2 が開始している新しい I/O トランザクションはこの通知を受信した後のみです。
