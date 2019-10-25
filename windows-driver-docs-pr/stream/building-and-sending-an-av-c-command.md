---
title: AV/C コマンドのビルドと送信
description: AV/C コマンドのビルドと送信
ms.assetid: 0f5bb205-7ffe-4007-bb66-a77889af2eed
keywords:
- Avc 関数ドライバー WDK、コマンドのビルドと送信
- WDK AV/C のビルドコマンド
- WDK AV/C を送信するコマンド
- AV/C WDK、コマンド
- Irp WDK AV/C
- I/O WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84e14e674d5e25c4248a1d47ad6d06836ca46d59
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840610"
---
# <a name="building-and-sending-an-avc-command"></a>AV/C コマンドのビルドと送信

次の手順では、AV/C コマンドをビルドして送信するプロセスの概要を示します。

1. サブユニットドライバーは、その下にあるドライバーの数に適した IRP を割り当てて初期化する必要があります (これは、次の下位のドライバーのデバイス\_オブジェクト&gt;**StackSize**メンバー) に対して指定されています。 ドライバーライターによって実装される IRP 管理のスタイルは、 *Avc*で使用する irp を取得する方法に影響します。 通常、ミニドライバーは[**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)を呼び出して、AV/C コマンドに新しい IRP を割り当てます。 **Ioallocateirp**によってサブユニットドライバーに割り当てられた IRP に対して[**Ioinitializer eirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeirp)を呼び出さないでください。 古い IRP を再初期化して再利用するのではなく、既存の IRP に対して[**Iofreeirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)を呼び出し、次に**Ioallocateirp**を呼び出して新しい irp を割り当てます。

    > [!NOTE]
    > 読みやすくするために、次のコード例ではエラー処理を示していません。

    ```cpp
    PIRP Irp;
    Irp = IoAllocateIrp(DeviceExtension->ParentDeviceObject->StackSize, FALSE);
    ```

2. 次に、サブモジュールドライバーは、必要な av/C 関数の種類に適した、IRB または AVC\_MULTIFUNC\_IRB 構造体の AVC\_コマンド\_割り当てます。また、必要な AV/C 要求パラメーターをブロックに入力します。 各 IOCTL\_AVC\_クラス関数のリファレンスページでは、関数が必要とする IRB について説明します。 IRB は、実行する AV/C オペコードと操作を記述するデータのブロックです。 *Avc*でサポートされる各関数は、特定の IRB 構造に関連付けられています。 IRB のメモリは、非ページプールから割り当てる必要があります。 IRB のメモリが割り当てられたら、関連付けられている構造体の定義に従って、関数のパラメーターを入力します。

    使用可能な関数とそれに関連付けられている構造体の定義の一覧については、「 [av/c プロトコルドライバー関数コード](https://docs.microsoft.com/windows-hardware/drivers/stream/av-c-protocol-driver-function-codes)」、「 [Av/c 構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)」、および「 [av/c 列挙](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)体」を参照してください。

    次に示すコードサンプルは、1つのオペランドバイトで構成される AV/C コントロールコマンドに対して、IRB 構造体の AVC\_コマンド\_割り当ておよび初期化する方法を示しています。

    ```cpp
    #include <avc.h>
    ...
    /* Define a custom pool tag to identify your subunit driver's memory allocations */
    #define CUSTOM_DRIVER_POOL_TAG 'C/VA'
    ...
    PAVC_COMMAND_IRB  AvcIrb;
    ...
    AvcIrb = ExAllocatePoolWithTag(NonPagedPool, sizeof(AVC_COMMAND_IRB), CUSTOM_DRIVER_POOL_TAG);
    ...
    RtlZeroMemory(AvcIrb, sizeof(AVC_COMMAND_IRB));

    #ifdef __cplusplus
    AvcIrb->Common.Function = AVC_FUNCTION_COMMAND;
    #else
    AvcIrb->Function = AVC_FUNCTION_COMMAND;
    #endif

    /*++ Do this to override the default time-out and retry values
    AvcIrb->TimeoutFlag = 1;
    AvcIrb->RetryFlag = 1;
    AvcIrb->Timeout.Quadpart = DEFAULT_AVC_TIMEOUT * 5;
    AvcIrb->Retries = 1;
    --*/
    AvcIrb->CommandType = AVC_CTYPE_CONTROL;
    AvcIrb->Opcode = Opcode;
    AvcIrb->OperandLength = 1;
    AvcIrb->Operand[0] = Operand;
    ```

3. サブユニットドライバーは、IRP の**MajorFunction**と**DeviceIoControl**のメンバー、および手順 2. で割り当てられた IRB へのポインターを指定する必要があります。 オペレーティングシステムから IRP を割り当てた後、対応する IRB に対して非ページメモリを割り当て、IRB のパラメーターを設定した後、IRB を IRP に関連付ける必要があります。 IRB の関数コードによっては、IRP で正しいディスパッチルーチンを指定する必要があります。 IOCTL\_AVC\_クラスに対応する AV/C 関数コードの場合 (つまり、 **DeviceIoControl コード**メンバーが IOCTL\_AVC\_クラスに設定されている)、IRP\_\_内部\_デバイス @no__t割り当てられた IRP の**MajorFunction**値として、8_ コントロールを指定する必要があります。\_ IOCTL\_\_AVC など、 *avc*でサポートされているその他のすべての AV/C 関数コードは[ **\_仮想\_サブユニット\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_update_virtual_subunit_info)、 [**IOCTL\_Avc\_\_仮想\_サブユニットを削除\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_remove_virtual_subunit_info)、 [**IOCTL\_AVC\_BUS\_RESET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_bus_reset)) では、割り当てられた irp の**MajorFunction**値として、irp\_MJ\_デバイス\_コントロールを指定する必要があります。

    次のコードサンプルは、Avc の IRP で処理するように設定する方法を示して*い*ます。

    ```cpp
    #include <avc.h>
    ...
    PAVC_COMMAND_IRB  AvcIrb;
    PIRP Irp;
    PIO_STACK_LOCATION NextIrpStack;
    ...
    AvcIrb = ExAllocatePoolWithTag(NonPagedPool, sizeof(AVC_COMMAND_IRB), 'C/VA');
    ...
    Irp = IoAllocateIrp(DeviceExtension->ParentDeviceObject->StackSize, FALSE);
    ...
    NextIrpStack = IoGetNextIrpStackLocation(Irp);
    NextIrpStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;
    NextIrpStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_AVC_CLASS;
    NextIrpStack->Parameters.Others.Argument1 = AvcIrb;
    ```

4. サブユニットドライバーは、少なくとも応答を解析する IRP の i/o 完了ルーチンを指定する必要があります。 また、完了ルーチンは、同期的に完了していない irp に割り当てられた IRP および IRB リソースを解放することもできます (つまり、IRP が既に保留中としてマークされている場合、完了ルーチンは IRP と IRB リソースのみを解放します)。

    サブユニットドライバーは、 *Avc*と通信するために irp を割り当てる必要があるため、i/o 完了ルーチンが必要です。 完了ルーチンを実行すると、下位のドライバーに対するサブユニットの呼び出しが完了した後に、i/o マネージャーがサブユニットドライバーの割り当てられた IRP の処理を続行できなくなります。 I/o 完了ルーチンは、\_処理\_必要なよりも多くの\_ステータスを常に返す必要があります。 この要件を超えて、サブユニットドライバーは制御フローとリソース管理のメカニズムを実装する場合があります。

    サブユニットドライバーは、i/o 完了ルーチンを設定するときに、PVOID コンテキストパラメーターを含めることができます。 このパラメーターは、完了ルーチンがそれを処理するように記述されていれば、任意のものへのポインターにすることができます。 サブユニットドライバーが、*中間処理*を伴わない AV/C 要求を確実に行うようにした場合、i/o 完了ルーチンは非常に単純になります。これを使用すると、 [**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)) (pvoid コンテキストとして渡される) をトリガーすることができます。 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出すメインコードパス (手順 5. で説明) は、イベントのストレージを提供し、 [**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)を使用して完了ルーチンと同期します。 IRP と IRB は、メインコードパスによって解放されます。

    ただし、サブユニットドライバーが中間処理を伴う可能性のある要求を送信している場合、完了ルーチンは応答を処理し、IRP および IRB リソースを解放します。 メインコードパスは、すべての IRP 処理を完了ルーチンに任せます。

5. 次に、サブシステムドライバーは[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出し、次に低いドライバー (サブシステムドライバーの**AddDevice**ルーチンで[**Ioattachdevicetodevicestack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)への呼び出しによって返される) と、 *Avc*に処理される IRP を渡します。

    ```cpp
    status = IoCallDriver( DeviceExtension->NextLowerDriver, Irp );
    ```

必要に応じて手順 1. ~ 5. を繰り返します。

*Avc*は、AV/C 要求が行われることを保証し、少なくとも呼び出しの範囲内で中間応答を受信します。 次の表では、AV/C 要求がどのように処理されたかを示す**IoCallDriver**リターンコードについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STATUS_SUCCESS</p></td>
<td><p>要求が行われ、AV/C 仕様のタイムアウトと再試行のパラメーターの境界内で最終的な応答が受信されました。 サブユニットの応答コード ( <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_command_irb" data-raw-source="[&lt;strong&gt;AVC_COMMAND_IRB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_command_irb)"><strong>AVC_COMMAND_IRB</strong></a>構造体の応答コードメンバー) は、操作の<strong>真の結果</strong>を確認するために引き続き検査する必要があります。 STATUS_SUCCESS は、ラウンドトリップ要求と応答サイクルが100ミリ秒未満で完了したことを意味します (既定のタイムアウトが100ミリ秒から変更されていないことを前提としています)。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_TIMEOUT</p></td>
<td><p>要求が行われましたが、すべてのタイムアウトと再試行処理が完了する前に応答が受信されませんでした。 前の要求がまだ処理されている場合、ターゲットの AV/C デバイスは要求を無視します。 一部の AV/C デバイスは、連続して複数回試行された後でも、100-ミリ秒間のタイムアウト時間内に応答しなくなります。 AVC_COMMAND_IRB 構造体を使用すると、既定の<strong>タイムアウト</strong>と<strong>再試行</strong>のメンバー (それぞれ100ミリ秒と9ミリ秒) を調整できますが、これらの既定の設定はすべての既知の実装に対して十分です。</p></td>
</tr>
<tr class="odd">
<td><p>あります</p></td>
<td><p>要求が行われ、中間応答が受信されました。 サブユニットドライバーの i/o 完了ルーチンは、最終的な応答を処理し、IRP および IRB リソースを解放する必要があります。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_REQUEST_ABORTED</p></td>
<td><p><em>Avc</em>が操作を終了しました。これはいくつかの理由で発生する可能性があります。</p>
<p>AV/C コマンド/要求は、中間応答を受信した後に応答を待機していましたが、IEEE 1394 バスはリセットされました (これらのコマンドは、サブユニットによって自動的に削除されます)。</p>
<p>内部の AV/C IRP 処理は異常終了したため、未処理のコマンドは停止されますが、デバイスではコマンドがまだ進行中である可能性があります)。</p>
<p>サブユニットが切断されたか、または<em>Avc</em>が無効になりました (たとえば、デバイスマネージャー)。</p>
<p>これらのすべてのシナリオで、サブユニットドライバーは、エラー状態が一時的なものである場合にコマンドを再試行する必要があります。</p></td>
</tr>
</tbody>
</table>

**IoCallDriver**からのその他の戻り値は、AV/C プロトコルの範囲を超えたエラーが発生したことを示します。 例:

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STATUS_NO_SUCH_DEVICE</p></td>
<td><p>デバイスが取り外されています。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td><p>システムのメモリが不足しています。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_INVALID_PARAMETER</p></td>
<td><p><em>Avc</em>に無効なパラメーターが渡されました。</p></td>
</tr>
</tbody>
</table>

基本の IRP 処理では、より低いドライバーで IRP を同期的に完了するか (直ちに)、後で完了するまで待機することができます。 操作が遅延されると、IRP は pending としてマークされ、下位のドライバーは、 **IoCallDriver**からのリターンコードとしてサブユニットドライバーに戻される、そのドライバーの各ディスパッチルーチンから保留状態\_を返します。 *Avc*は、AV/C コマンド/応答プロトコルをこのモデルに変換します。

即時 (同期) 応答が返される AV/C*状態*または*照会*要求は、 **IoCallDriver**呼び出しの間に完全に完了します。 **IoCallDriver**から直接戻ると、Av/c 仕様で詳細に説明されている 100 ms AV/c 応答タイムアウト制約内で応答が発生したことを示します。

エラー状態が発生した場合にのみ、*通知*要求がすぐに応答します。

一部の*コントロール*とすべての*通知*要求は、100ミリ秒以内に要求を確認しますが、完了しないことがあります。 受信確認は中間応答を介して行われます。これは、このドキュメントで*中間処理*として参照されます。 中間応答の結果として、 **IoCallDriver**は状態\_PENDING を返します。 この結果が発生した場合、上記の手順 4. で指定した i/o 完了ルーチンは、要求が AV/C サブユニットによって最後に完了したときの通知ポイントです。

Irp と Ioctl の詳細については、「 [irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)」を参照してください。
