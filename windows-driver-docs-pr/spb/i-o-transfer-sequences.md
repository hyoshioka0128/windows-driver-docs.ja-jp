---
title: I/O 転送シーケンス
description: SPB framework extension (SpbCx) では、i/o 転送シーケンスがサポートされています。
ms.assetid: 7415DB28-5E93-4F47-B169-7C652969D4C7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 109362ddf4fcca4d5d5558cc0cf66ec63764e50c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842870"
---
# <a name="io-transfer-sequences"></a>I/O 転送シーケンス

SPB framework extension (SpbCx) では、i/o 転送シーケンスがサポートされています。 I/o 転送シーケンスは、単一のアトミックバス操作として実行される、順序付けされたバス転送 (読み取りおよび書き込み操作) のセットです。 I/o 転送シーケンス内のすべての転送は、バス上の同じターゲットデバイスにアクセスします。 シーケンスが実行されている間、バス上の他のデバイスにアクセスできなくなります。ただし、i/o 転送シーケンスが完了する前に、SPB コントローラードライバーが他のデバイスに対して i/o 要求を受信する可能性があります。

I/o 転送シーケンスの例としては、書き込み読み取り操作があります。これは、バス書き込み操作の後にバス読み取り操作が行われます。 クライアントの周辺機器ドライバーでは、この種類のシーケンスを使用して、SPB に接続された周辺機器の関数選択レジスタに書き込み、選択したデバイス関数の値を読み取ることができます。 この2つの転送の長さは異なる場合があります。 たとえば、書き込み操作によって1バイトのデータが転送され、読み取り操作によって大量のデータが転送される可能性があります。

## <a name="types-of-io-transfer-sequences"></a>I/o 転送シーケンスの種類

クライアントは、次の2つの方法のいずれかで i/o 転送シーケンスを開始できます。

* クライアントは\_シーケンス I/o 制御要求を[**実行\_、IOCTL\_SPB**](https://msdn.microsoft.com/library/windows/hardware/hh450857)内のシーケンス全体を指定できます。 この要求により、SPB コントローラードライバーは、転送シーケンスを実行するために使用できる任意のハードウェア固有のパフォーマンスの最適化を使用できます。 詳細については、「[単一要求シーケンス](#single-request-sequences)」を参照してください。

* クライアントは、シーケンスの開始時にコントローラーをロックするための[**ioctl\_spb\_ロック\_コントローラー**](https://msdn.microsoft.com/library/windows/hardware/hh450858)の i/o 制御要求を送信し、シーケンスがである場合に\_コントローラーのロックを[**解除\_、ioctl\_SPB**](https://msdn.microsoft.com/library/windows/hardware/hh450859)を送信できます。完了. コントローラーがロックされている間、クライアントは、シーケンス内の読み取りまたは書き込み操作ごとに、個別の i/o 要求 ([**irp\_MJ\_read**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)または[**irp\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)) を送信します。 詳細については、「[クライアントによって実装](#client-implemented-sequences)されるシーケンス」を参照してください。

クライアントは、可能な限り、 **IOCTL\_SPB**を使用して\_シーケンス要求を実行\_高速で、エラーが発生しにくく、他のクライアントがバスからロックアウトされるまでの時間が大幅に短縮されます。 ただし、クライアントは、シーケンス内の転送中に読み取られた値を確認する必要がある場合に、\_コントローラーおよび**ioctl\_spb**を\_して、 **ioctl\_spb**を使用して\_コントローラーの要求のロックを解除\_ことができます。シーケンス内で後で転送を開始する前に。 この場合は、他のクライアントが必要以上に長い間ロックされないように注意して設計する必要があります。また、不適切に設計された周辺機器ドライバーがシステム全体のパフォーマンスを低下させる可能性があります。

## <a name="single-request-sequences"></a>単一要求シーケンス

パフォーマンスを向上させるには、SPB コントローラードライバーが[*EvtSpbControllerIoSequence*](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_sequence)コールバック関数を実装し、 [ **\_シーケンス要求を実行\_IOCTL\_SPB**](https://msdn.microsoft.com/library/windows/hardware/hh450857)を処理する必要があります。 この方法では、SPB コントローラードライバーが複雑になりますが、他のクライアントがバスからロックアウトされている間に、一連の個別の読み取りおよび書き込み操作として、クライアントが i/o 転送シーケンスを実行する必要がありません。

> [!NOTE]
> *EvtSpbControllerIoSequence*関数を実装することを強くお勧めします。これは、Windows 8 の要件になる場合があります。

 転送シーケンスの実装は、単純な読み取り操作または書き込み操作の場合と似ていますが、シーケンス内の個々の転送間のシーケンス操作の格納された状態を更新する必要もあります。 最初の転送が完了すると、SPB コントローラードライバーはシーケンスの状態を更新して、シーケンス内の次の転送を選択します。 シーケンスの状態はデバイスコンテキストに格納され、 *EvtSpbControllerIoSequence*コールバックに渡される[**spbrequest**](https://docs.microsoft.com/windows-hardware/drivers/spb/spbcx-object-handles)ハンドルを含みます。 SPB コントローラードライバーは、このハンドルを使用して、シーケンス内の個々の転送のバッファー、長さ、方向、および位置パラメーターを取得します。 これらのパラメーターの取得の詳細については、「 [**Spbrequestgettransferparameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbrequestgettransferparameters)」を参照してください。

SPB コントローラードライバーが、要求された**IOCTL\_spb**を実行できない場合は\_シーケンス操作を実行\_、エラーコードを使用して要求を完了します。 このような障害が発生した場合、クライアントはオプションとしてバスをロックし、単純な一連の単純な i/o 要求として明示的に i/o 転送シーケンスを実行し、バスのロックを解除することができます。 詳細については、「[クライアントによって実装](#client-implemented-sequences)されるシーケンス」を参照してください。

SpbCx は、IOCTL\_SPB のパラメーターチェックを行い、周辺機器ドライバーから受信した要求を **\_* XXX*** します。 **\_シーケンス要求を実行\_IOCTL\_SPB**の場合、SpbCx は空のシーケンスと NULL バッファーポインターまたは長さ0のバッファーを含むシーケンスの両方を拒否します。

SPB コントローラードライバーは、シーケンス内の各転送の長さが、ドライバーによって指定された制限を超えていないことを確認する必要があります。 たとえば、Windows Driver Kit (WDK) の SkeletonI2C サンプルドライバーは、4 k バイトを超える転送を指定し、この要求のステータスコードを\_状態に設定する **\_シーケンス要求を実行\_、IOCTL\_SPB**に失敗します。\_パラメーターが無効です。 **\_シーケンス要求を実行\_IOCTL\_SPB**のシーケンス操作を開始する前に、ドライバーはシーケンス内のすべての転送のパラメーターを検証して、操作を正常に完了できることを確認する必要があります。

SpbCx は、 [*EvtspbEvtSpbControllerIoSequence lock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_lock)コールバックを使用したコールバックの前にはなりません。また、 [*Evtspb Unlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_lock)コールバックによる*EvtSpbControllerIoSequence*コールバックに従うことはありません。

## <a name="client-implemented-sequences"></a>クライアントによって実装されたシーケンス

SPB コントローラードライバーのクライアントは、単純な読み取りと書き込みの一連の操作として、i/o 転送シーケンスを明示的に実行できます。 クライアントは、バスに接続されている周辺機器を制御するカーネルモードドライバーまたはユーザーモードドライバーのいずれかになります。 シーケンス内の最初の転送の前に、クライアントは[**IOCTL\_SPB**](https://msdn.microsoft.com/library/windows/hardware/hh450858)を送信し、ターゲットデバイスにロック\_コントローラー要求\_します。これにより、シーケンス内の転送間で他の関連のないバスアクセスが発生するのを防ぐことができます。 次に、クライアントが[**irp\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)および[**IRP\_\_MJ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)に送信し、シーケンスの転送を実行する書き込み要求を送信します。 最後に、クライアントは、ロックを解除するために[ **\_コントローラーの要求\_、IOCTL\_SPB**](https://msdn.microsoft.com/library/windows/hardware/hh450859)を送信します。

シーケンス内の後の転送が以前の転送に依存している場合、クライアントはこの種類の i/o 転送シーケンスを実装する必要があります。 たとえば、最初の読み取りでは、後で読み取りまたは書き込みを行うバイト数を示している可能性があります。 ただし、このような依存関係が存在しない場合、クライアントは、\_シーケンス要求を SPB コントローラードライバーに[**実行\_の IOCTL\_spb**](https://msdn.microsoft.com/library/windows/hardware/hh450857)を送信する必要があります。これにより、シーケンスをより効率的に実行できます。

クライアントに実装されたシーケンスを開始する **\_ロック\_コントローラー**の要求と、IOCTL **\_spb\_** 、シーケンスを終了する i/o 要求だけを終了する\_コントローラー要求の間で、ioctl\_spb の間クライアントがターゲットデバイスに送信できるのは、 **irp\_MJ\_READ**および**irp\_MJ\_書き込み**要求です。 このルールの違反は、エラーです。

SPB ロックは、読み取りと書き込みのシーケンスがアトミックバス操作として実行されることを保証するためにのみ使用され、その目的でのみ使用する必要があります。

詳細については、「[クライアントに実装](https://docs.microsoft.com/windows-hardware/drivers/spb/handling-client-implemented-sequences)されたシーケンスの処理」を参照してください。
