---
title: AV/C コマンドの構築と送信
description: AV/C コマンドの構築と送信
ms.assetid: 0f5bb205-7ffe-4007-bb66-a77889af2eed
keywords:
- Avc.sys 関数ドライバー WDK、コマンドのビルドと送信
- WDK AV/C を構築するコマンド
- WDK AV/C を送信するコマンド
- AV/C WDK、コマンド
- Irp WDK AV/C
- I/O WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e99299a05a757a873d3b08b2dcfacb50292336d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386680"
---
# <a name="building-and-sending-an-avc-command"></a>AV/C コマンドの構築と送信

次の手順をビルドして、AV/C コマンドを送信するプロセスについて説明します。

1. サブユニット ドライバーする必要があります割り当ておよびそれ自体の下のドライバーの数の適切な IRP の初期化 (下位の [次へ] ドライバーのデバイスで指定されている\_オブジェクト -&gt;**StackSize**メンバー)。 ドライバーの作成者によって実装される IRP 管理のスタイルを使用した IRP を取得する方法に影響を与えます*Avc.sys*します。 通常、ミニドライバーを呼び出す[ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp) AV/C コマンドを新しい IRP を割り当てられません。 呼び出さない[ **IoInitializeIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializeirp)サブユニット ドライバーでは、割り当てられた IRP の**IoAllocateIrp**します。 再初期化し、古い IRP を再利用しようとするのではなく呼び出す[ **IoFreeIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)で呼び出して、既存の IRP **IoAllocateIrp**新しい IRP を割り当てることです。

    > [!NOTE]
    > 読みやすくするために、次のコード例ではエラー処理は示していません。

    ```cpp
    PIRP Irp;
    Irp = IoAllocateIrp(DeviceExtension->ParentDeviceObject->StackSize, FALSE);
    ```

2. サブユニット ドライバーを割り当てます、AVC\_コマンド\_IRB または AVC\_MULTIFUNC\_IRB 構造が必要な AV/C 関数の種類に適したし、目的の AV/C 要求のブロックを格納します。パラメーター。 リファレンス ページの各 IOCTL\_AVC\_クラス関数が関数に必要などの IRB について説明します。 IRB、AV/C オペコードおよび実行する操作を記述するデータのブロックです。 各関数でサポートされている*Avc.sys*特定 IRB 構造に関連付けられています。 非ページ プールから、IRB 用のメモリを割り当てる必要があります。 IRB 用のメモリが割り当てられると、その関連付けられている構造の定義に従って関数のパラメーターを入力します。

    使用可能な関数とその関連付けられている構造定義の一覧で、次を参照してください[AV/C プロトコル ドライバー関数コード](https://docs.microsoft.com/windows-hardware/drivers/stream/av-c-protocol-driver-function-codes)、 [AV/C 構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index)、および[AV/C 列挙体](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index).

    次に示すコード サンプル方法、AVC\_コマンド\_IRB 構造体を割り当てられ、1 つのオペランドのバイトで構成される AV/C コントロール コマンド用に初期化された可能性があります。

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

3. サブユニット ドライバーは IRP を指定する必要があります**MajorFunction**と**Parameters.DeviceIoControl.IoControlCode**メンバーだけが、手順 2. で割り当てられた IRB へのポインター。 対応する IRB では、非ページ メモリを割り当て、オペレーティング システムから IRP の割り当てし、IRB のパラメーターを設定し後、は、IRB IRP に関連付ける必要があります。 IRB の関数のコードによってには、IRP で適切なディスパッチ ルーチンを指定する必要があります。 IOCTL に対応する AV/C 関数のコードの\_AVC\_クラス (つまり、 **Parameters.DeviceIoControl.IoControlCode** IOCTL にメンバーが設定されている\_AVC\_クラス)、IRP\_MN\_内部\_デバイス\_として割り当てられた IRP のコントロールを指定する必要があります**MajorFunction**値。 サポートされている他のすべての AV/C 関数コード*Avc.sys*など[ **IOCTL\_AVC\_UPDATE\_仮想\_サブユニット\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ni-avc-ioctl_avc_update_virtual_subunit_info)、 [ **IOCTL\_AVC\_削除\_仮想\_サブユニット\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ni-avc-ioctl_avc_remove_virtual_subunit_info)、および[**IOCTL\_AVC\_BUS\_リセット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ni-avc-ioctl_avc_bus_reset)、IRP を指定する必要があります\_MJ\_デバイス\_として割り当てられた IRP のコントロール**MajorFunction**値。

    次のコード サンプルの IRP を設定する方法を示しています。 *Avc.sys*プロセスに。

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

4. サブユニット ドライバーでは、少なくとも、応答を解析する IRP の I/O 完了ルーチンを指定します。 完了ルーチンが同期的に完了しない Irp に以前割り当てられた IRP と IRB リソースを解放できますも (つまり、完了ルーチンのみリソースを解放 IRP と IRB IRP が以前の保留中としてマークされた場合)。

    サブユニット ドライバーは Irp との通信に割り当てる必要がありますので、I/O 完了ルーチンが必要な*Avc.sys*します。 完了ルーチンでは、I/O マネージャーが下位のドライバーのサブユニットの呼び出しが完了したら、サブユニット ドライバーの割り当てられた IRP の処理を継続できなくなります。 I/O 完了ルーチンは、状態を返す必要があります常に\_詳細\_処理\_必要な作業です。 サブユニット ドライバーは、その要件を超えるその制御フローとリソース管理のメカニズムを実装できます。

    サブユニット ドライバーが I/O 完了ルーチンを設定すると、PVOID コンテキスト パラメーターに含めることができます。 このパラメーターは、それに対応する完了ルーチンが書き込まれる限り、何もへのポインターを指定できます。 サブユニット ドライバーが含むことはありません AV/C 要求を行うことを確認して場合*中間処理*、I/O 完了ルーチンを非常に単純なことができますし、: 使用してトリガーする、 [ **KSEVENT** ](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))(PVOID コンテキストとして渡されます)。 呼び出すメイン コード パス[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) (手順 5 で説明)、イベント、記憶域を提供しを使用して[ **kewaitforsingleobject の 1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)完了ルーチンと同期します。 IRP と IRB は、メインのコード パスで解放されます。

    ただし、サブユニット ドライバーでは、中間処理を伴う可能性がある要求を送信するが場合は、完了ルーチンは、応答の処理と IRP と IRB リソースの解放を担当します。 メインのコード パスでは、完了ルーチンにすべての IRP の処理の責任を解放します。

5. サブユニット ドライバーを呼び出して[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)し、[次へ] の下位のドライバーを渡します (への呼び出しによって返される[ **IoAttachDeviceToDeviceStack** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)サブユニット ドライバーの**AddDevice**ルーチン) とを処理する IRP *Avc.sys*します。

    ```cpp
    status = IoCallDriver( DeviceExtension->NextLowerDriver, Irp );
    ```

必要に応じて、5 から、手順 1. を繰り返します。

*Avc.sys* AV/C 要求が行われ、呼び出しの範囲内で、少なくとも 1 つの中間の応答が受信したことを保証しようとしています。 次の表に、考えられる**保留**AV/C 要求の処理方法を示すコードを返します。

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
<td><p>要求が行われ、AV/C 仕様のタイムアウトと再試行のパラメーターの範囲内で最後の応答を受け取りました。 サブユニットの応答コード (、 <strong>ResponseCode</strong>のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_command_irb" data-raw-source="[&lt;strong&gt;AVC_COMMAND_IRB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_command_irb)"> <strong>AVC_COMMAND_IRB</strong> </a>構造) も true、操作の結果を確認する検証が必要です。 STATUS_SUCCESS は、(既定のタイムアウト値が 100 ミリ秒から変更されていないと仮定)、100 ミリ秒未満でラウンドト リップの要求および応答のサイクルが完了したことを意味します。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_TIMEOUT</p></td>
<td><p>要求が行われたが、すべてタイムアウトするまでの応答が受信されず、再試行の処理が完了します。 ターゲット AV/C デバイスは、前の要求がまだ処理されている場合に要求を無視に注意してください。 一部の AV/C デバイスせずに準拠してくださいいくつかの連続する試行した後でも 100 ミリ秒のタイムアウト以内に応答を拒否します。 AVC_COMMAND_IRB 構造により、既定値の調整<strong>タイムアウト</strong>と<strong>再試行</strong>メンバー (100 ミリ秒と 9 ミリ秒は、それぞれ)、既定の設定は、すべてのための十分なされているが、既知の実装。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_PENDING</p></td>
<td><p>要求が行われ、暫定的な応答を受け取りました。 最後の応答を処理し、IRP と IRB リソースを解放し、サブユニット ドライバーの I/O 完了ルーチンの役目です。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_REQUEST_ABORTED</p></td>
<td><p><em>Avc.sys</em>いくつかの理由で発生することが、操作が終了しました。</p>
<p>AV C/コマンド/要求は、暫定的な応答を受信したが、IEEE 1394 のバスのリセット (およびこれらのコマンドが、サブユニットによって削除されます。 サイレント モードで) 後の応答を待機していた。</p>
<p>内部の AV/C IRP の処理が異常終了しているため、未解決のコマンドを停止すると、デバイス上で進行中のコマンドは、ある可能性がありますが)。</p>
<p>サブユニットが接続されている、または<em>Avc.sys</em> (たとえばデバイス マネージャーから) を無効にされました。</p>
<p>これらすべてのシナリオでのサブユニット ドライバーはエラー状態は一時的な場合にコマンドを再試行する必要があります。</p></td>
</tr>
</tbody>
</table>

その他の戻り値から**保留**AV/C プロトコルの範囲を超えていたエラーが発生したことを示します。 以下に例を示します。

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
<td><p>0XC000000ESTATUS_NO_SUCH_DEVICE</p></td>
<td><p>デバイスの接続が解除されました。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td><p>システム メモリが不足します。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_INVALID_PARAMETER</p></td>
<td><p>無効なパラメーターが渡された<em>Avc.sys</em>します。</p></td>
</tr>
</tbody>
</table>

基本的な IRP の処理では、下位の IRP が同期的に完了するかをドライバーの (直ちに)、または、後でその完了を延期します。 操作の遅延し、IRP に、保留中とマークされている場合は、下位のドライバーのステータスを返します\_ドライバーのそれぞれのディスパッチ ルーチンからのリターン コードとしてのサブユニット ドライバーに戻ったから PENDING**保留**. *Avc.sys*このモデルに AV C/コマンド/応答プロトコルを変換します。

AV/C*状態*または*照会*の期間中に、即座 (同期) に応答する要求が完全に完了、**保留**呼び出します。 すぐに回収**保留**AV/C 仕様に記載された 100 ミリ秒 AV/C 応答タイムアウト制限内に応答が発生することを示します。

A*通知*が応答を要求するエラー条件がある場合は、すぐにのみです。

いくつか*コントロール*すべて*通知*要求承認しますが、必ずしもが完了していない 100 ミリ秒以内で要求します。 このドキュメントで呼ばれる中間の応答は、受信確認*中間処理*します。 中間の応答には、その結果、**保留**ステータスを返します\_保留します。 この結果は、要求が AV/C のサブユニットで最後に完了したときに、上記の手順 4 で指定された I/O 完了ルーチンは通知のポイントに発生します。 場合、

Irp と Ioctl の詳細については、次を参照してください。 [Irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)します。
