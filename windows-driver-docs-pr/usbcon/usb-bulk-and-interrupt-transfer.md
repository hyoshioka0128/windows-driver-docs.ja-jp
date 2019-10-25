---
Description: このトピックでは、USB 一括転送の概要について説明します。
title: USB バルク転送要求の送信方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6af27cbf17014fc84645ddebe130160f3eb3c8b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843202"
---
# <a name="how-to-send-usb-bulk-transfer-requests"></a>USB バルク転送要求の送信方法


このトピックでは、USB 一括転送の概要について説明します。 また、クライアントドライバーがデバイスから一括データを送受信する方法について、手順を追って説明します。

-   [一括エンドポイントについて](#about-bulk-endpoints)
-   [一括トランザクション](#bulk-transactions)
-   [一括転送のための USB クライアントドライバーのタスク](#usb-client-driver-tasks-for-a-bulk-transfer)
-   [一括転送要求の例](#bulk-transfer-request-example)
    -   [前提条件](#prerequisites)
    -   [手順 1: 転送バッファーを取得します。](#step-1--get-the-transfer-buffer--)
    -   [手順 2: フレームワークの要求オブジェクトを書式設定し、USB ドライバースタックに送信します。](#step-2--format-and-send-a-framework-request-object-to-the-usb-driver-stack-)
    -   [手順 3: 要求の完了ルーチンを実装します。](#step-3--implement-a-completion-routine-for-the-request-)

## <a name="about-bulk-endpoints"></a>一括エンドポイントについて


USB 一括エンドポイントは、大量のデータを転送できます。 一括転送は、ハードウェアエラーの検出を可能にする信頼性が高く、ハードウェアの再試行回数が制限されます。 一括エンドポイントへの転送では、帯域幅はバス上で予約されていません。 さまざまな種類のエンドポイントを対象とする複数の転送要求がある場合、コントローラーは、アイソクロナスや割り込みパケットなど、時間の重要なデータの転送を最初にスケジュールします。 バスで使用可能な未使用の帯域幅がある場合にのみ、コントローラーは一括転送をスケジュールします。 バス上に他の重要なトラフィックがない場合は、一括転送が高速になることがあります。 ただし、バスが他の転送でビジー状態になると、一括データは無期限に待機することができます。

次に、一括エンドポイントの主な機能を示します。

-   一括エンドポイントは省略可能です。 これらは、大量のデータを転送する USB デバイスでサポートされています。 たとえば、ファイルをフラッシュドライブに転送したり、プリンターやスキャナーとの間でデータを転送したりすることができます。
-   USB の全速度、高速、SuperSpeed デバイスは、一括エンドポイントをサポートします。 低速デバイスは、一括エンドポイントをサポートしていません。
-   エンドポイントは一方向であり、データは IN または OUT 方向に転送できます。 Bulk IN エンドポイントは、デバイスからホストにデータを読み取るために使用されます。また、bulk OUT エンドポイントは、ホストからデバイスにデータを送信するために使用されます。
-   エンドポイントには、エラーをチェックするための CRC ビットがあるため、データの整合性が確保されます。 CRC エラーの場合、データは自動的に再送信されます。
-   SuperSpeed 一括エンドポイントは、ストリームをサポートできます。 ストリームは、ホストが個々のストリームパイプに転送を送信できるようにします。
-   一括エンドポイントの最大パケットサイズは、デバイスのバス速度によって異なります。 最高速度、高速、SuperSpeedパケットの最大サイズは、それぞれ64、512、および1024バイトです。

## <a name="bulk-transactions"></a>一括トランザクション


他のすべての USB 転送と同様に、ホストは常に一括転送を開始します。 通信は、ホストとターゲットエンドポイント間で行われます。 USB プロトコルでは、一括トランザクションで送信されるデータにフォーマットは適用されません。

ホストとデバイスがバスでどのように通信するかは、デバイスが接続されている速度によって異なります。 このセクションでは、ホストとデバイス間の通信を示す高速および SuperSpeed の一括転送の例について説明します。

トランザクションとパケットの構造は、Beagle、Ellisys、LeCroy USB プロトコルアナライザーなどの任意の USB アナライザーを使用して確認できます。 Analyzer デバイスは、ネットワーク経由で USB デバイスとの間でデータを送受信する方法を示しています。 この例では、LeCroy USB アナライザーによってキャプチャされたトレースをいくつか確認してみましょう。 この例は、情報のみを対象としています。 これは Microsoft が保証するものではありません。

**Bulk OUT トランザクションの例**

このアナライザートレースは、高速での一括出力トランザクションの例を示しています。

![データトランザクション例のトレース。](images/bulk-out-hs.png)

このトレースでは、ホストは、PID が OUT (OUT token) に設定されたトークンパケットを送信することにより、高速一括エンドポイントへの一括転送を開始します。 このパケットには、デバイスとターゲットエンドポイントのアドレスが含まれています。 OUT パケットの後、ホストは一括ペイロードを含むデータパケットを送信します。 エンドポイントが受信データを受け入れる場合は、ACK パケットを送信します。 この例では、ホストがデバイスアドレスに31バイトを送信したことを確認できます。1エンドポイントアドレス: 2。

データパケットが到着した時点でエンドポイントがビジー状態で、データを受信できない場合、デバイスは NAK パケットを送信できます。 この場合、ホストはデバイスへの PING パケットの送信を開始します。 デバイスは、デバイスがデータを受信する準備ができていない限り、NAK パケットで応答します。 デバイスの準備が整うと、ACK パケットで応答します。 ホストは、OUT 転送を再開できます。

このアナライザートレースは、SuperSpeed bulk OUT トランザクションの例を示しています。

![データトランザクション例のトレース。](images/bulk-out.png)

前のトレースでは、ホストはデータパケットを送信することによって、SuperSpeed bulk エンドポイントへの OUT トランザクションを開始します。 データパケットには、一括ペイロード、デバイス、およびエンドポイントのアドレスが含まれています。 この例では、ホストがデバイスアドレスに31バイトを送信したことがわかります。エンドポイントアドレス: 2。

デバイスは、データパケットを受信して確認し、ホストに ACK パケットを送り返します。 データパケットが到着した時点でエンドポイントがビジー状態で、データを受信できない場合、デバイスは NRDY パケットを送信できます。 高速とは異なり、NRDY パケットを受信した後、ホストはデバイスを繰り返しポーリングしません。 代わりに、ホストはデバイスからの ERDY を待機します。 デバイスの準備ができたら、ERDY パケットが送信され、ホストはエンドポイントにデータを送信できるようになります。

**Bulk IN transaction の例**

このアナライザートレースは、高速でトランザクションを一括した例を示しています。

![データトランザクション例のトレース。](images/bulk-in-hs.png)

前のトレースでは、ホストは PID を IN (トークン内) に設定してトークンパケットを送信することで、トランザクションを開始します。 その後、デバイスは一括ペイロードを使用してデータパケットを送信します。 エンドポイントに送信するデータがない場合、またはデータを送信する準備がまだできていない場合、デバイスは NAK ハンドシェイクパケットを送信できます。 ホストは、デバイスから ACK パケットを受信するまで、転送を再試行します。 この ACK パケットは、デバイスがデータを受け入れたことを意味します。

このアナライザートレースは、SuperSpeed bulk IN transaction の例を示しています。

![データトランザクション例のトレース。](images/bulk-in.png)

SuperSpeed エンドポイントからの一括転送を開始するために、ホストは ACK パケットを送信して一括トランザクションを開始します。 USB 仕様バージョン3.0 では、ACK とパケットを1つの ACK パケットにマージすることで、この最初の部分の転送が最適化されます。 SuperSpeed の場合、トークンではなく、ホストは、一括転送を開始するために ACK トークンを送信します。 デバイスはデータパケットで応答します。 次に、ホストは ACK パケットを送信してデータパケットを確認します。 エンドポイントがビジーで、データを送信できなかった場合、デバイスは NRDY の状態を送信できます。 この場合、ホストはデバイスから ERDY パケットを取得するまで待機します。

## <a name="usb-client-driver-tasks-for-a-bulk-transfer"></a>一括転送のための USB クライアントドライバーのタスク


ホスト上のアプリケーションまたはドライバーは、常に一括転送を開始してデータを送受信します。 クライアントドライバーは、要求を USB ドライバースタックに送信します。 USB ドライバースタックは、要求をホストコントローラーにプログラムし、ネットワーク経由でデバイスに対してプロトコルパケット (前のセクションで説明) を送信します。

アプリケーションまたは他のドライバーの要求の結果として、クライアントドライバーが一括転送の要求を送信する方法を見てみましょう。 または、ドライバーが独自の転送を開始することもできます。 方法に関係なく、一括転送を開始するために、ドライバーに転送バッファーと要求が必要です。

KMDF ドライバーの場合、要求はフレームワークの要求オブジェクトに記述されます (「 [WDF Request オブジェクトリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/)」を参照してください)。 クライアントドライバーは、要求を USB ドライバースタックに送信する WDFREQUEST ハンドルを指定することによって、要求オブジェクトのメソッドを呼び出します。 クライアントドライバーがアプリケーションまたは別のドライバーからの要求に応答して一括転送を送信する場合、フレームワークは、要求オブジェクトを作成し、フレームワークキューオブジェクトを使用してクライアントドライバーに要求を配信します。 この場合、クライアントドライバーは、一括転送を送信するために、その要求を使用することがあります。 クライアントドライバーが要求を開始した場合、ドライバーは独自の要求オブジェクトを割り当てることができます。

アプリケーションまたはその他のドライバーがデータを送信または要求した場合、転送バッファーはフレームワークによってドライバーに渡されます。 また、ドライバーが独自に転送を開始する場合は、クライアントドライバーが転送バッファーを割り当て、要求オブジェクトを作成することもできます。

クライアントドライバーの主なタスクは次のとおりです。

1.  転送バッファーを取得します。
2.  フレームワークの要求オブジェクトを取得して書式設定し、USB ドライバースタックに送信します。
3.  完了ルーチンを実装して、USB ドライバースタックが要求を完了したときに通知を受け取るようにします。

このトピックでは、これらのタスクについて説明します。この例では、アプリケーションがデータを送受信するための要求の結果として、ドライバーが一括転送を開始します。

デバイスからデータを読み取るために、クライアントドライバーは、提供されている継続的なリーダーオブジェクトを使用できます。 詳細については、「[連続リーダーを使用して USB パイプからデータを読み取る方法](how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md)」を参照してください。

## <a name="bulk-transfer-request-example"></a>一括転送要求の例


アプリケーションがデバイスに対してデータの読み取りまたは書き込みを行うシナリオの例を考えてみましょう。 このような要求を送信するために、アプリケーションは Windows Api を呼び出します。 この例では、カーネルモードでドライバーによって発行されたデバイスインターフェイス GUID を使用して、アプリケーションがデバイスへのハンドルを開きます。 次に、アプリケーションは、 [**ReadFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)または[**WriteFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile)を呼び出して、読み取り要求または書き込み要求を開始します。 この呼び出しでは、アプリケーションは、読み取りまたは書き込みを行うデータとそのバッファーの長さを含むバッファーも指定します。

I/o マネージャーは、要求を受信し、i/o 要求パケット (IRP) を作成して、それをクライアントドライバーに転送します。

フレームワークは、要求をインターセプトし、フレームワーク要求オブジェクトを作成して、フレームワークキューオブジェクトに追加します。 次に、フレームワークは、新しい要求が処理を待機していることをクライアントドライバーに通知します。 その通知は、 [*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)または[*Evtiowrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)のドライバーのキューコールバックルーチンを呼び出すことによって行われます。

フレームワークは、クライアントドライバーに要求を配信するときに、次のパラメーターを受け取ります。

-   要求を含むフレームワークキューオブジェクトへの WDFQUEUE ハンドル。
-   この要求の詳細を格納しているフレームワーク要求オブジェクトへの WDFREQUEST ハンドル。
-   転送の長さ。つまり、読み取りまたは書き込みの対象となるバイト数です。

クライアントドライバーによる[*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)または[*Evtiowrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)の実装では、ドライバーは要求パラメーターを検査し、必要に応じて検証チェックを実行できます。

SuperSpeed bulk エンドポイントのストリームを使用している場合は、KMDF が本質的にストリームをサポートしていないため、要求を URB で送信します。 一括エンドポイントのストリームへの転送要求を送信する方法の詳細については、「 [USB 一括エンドポイントで静的ストリームを開いて閉じる方法](how-to-open-streams-in-a-usb-endpoint.md)」を参照してください。

ストリームを使用していない場合は、次の手順で説明するように、KMDF で定義されたメソッドを使用して要求を送信できます。

### <a name="prerequisites"></a>前提条件

開始する前に、次の情報があることを確認してください。

-   クライアントドライバーは、フレームワークの USB ターゲットデバイスオブジェクトを作成し、 [**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)メソッドを呼び出すことによって WDFUSBDEVICE ハンドルを取得する必要があります。

    Microsoft Visual Studio Professional 2012 で提供されている USB テンプレートを使用している場合は、テンプレートコードによってそれらのタスクが実行されます。 テンプレートコードは、ターゲットデバイスオブジェクトへのハンドルを取得し、デバイスコンテキストに格納します。 詳細については、「 [USB クライアントドライバーのコード構造 (KMDF)](understanding-the-kmdf-template-code-for-usb.md)について」の「デバイスのソースコード」を参照してください。

-   この要求の詳細を格納しているフレームワーク要求オブジェクトへの WDFREQUEST ハンドル。
-   読み取りまたは書き込みを行うバイト数。
-   ターゲットエンドポイントに関連付けられているフレームワークパイプオブジェクトへの WDFUSBPIPE ハンドル。 パイプを列挙することによって、デバイスの構成中にパイプハンドルを取得する必要があります。 詳細については、「 [USB パイプを列挙する方法](how-to-get-usb-pipe-handles.md)」を参照してください。

    一括エンドポイントでストリームがサポートされている場合は、ストリームへのパイプハンドルが必要です。 詳細については、「 [USB 一括エンドポイントで静的ストリームを開いて閉じる方法](how-to-open-streams-in-a-usb-endpoint.md)」を参照してください。

### <a href="" id="step-1--get-the-transfer-buffer--"></a>手順 1: 転送バッファーを取得します。

転送バッファーまたは転送バッファー MDL には、送信または受信するデータが含まれています。 このトピックでは、転送バッファーでデータを送受信することを前提としています。 転送バッファーは、WDF memory オブジェクトに記述されています (「 [WDF Memory オブジェクトリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/)」を参照してください)。 転送バッファーに関連付けられているメモリオブジェクトを取得するには、次のいずれかのメソッドを呼び出します。

-   一括転送要求の場合は、 [**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)メソッドを呼び出します。
-   一括送信転送要求の場合は、 [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)メソッドを呼び出します。

クライアントドライバーは、このメモリを解放する必要はありません。 メモリは親要求オブジェクトに関連付けられ、親が解放されると解放されます。

### <a href="" id="step-2--format-and-send-a-framework-request-object-to-the-usb-driver-stack-"></a>手順 2: フレームワークの要求オブジェクトを書式設定し、USB ドライバースタックに送信します。

転送要求は、非同期的または同期的に送信できます。

非同期メソッドは次のとおりです。

-   [**WdfUsbTargetPipeFormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread)
-   [**WdfUsbTargetPipeFormatRequestForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforwrite)

この一覧のメソッドは、要求を書式設定します。 要求を非同期的に送信する場合は、次の手順で説明するように、 [**Wdfrequestsetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)メソッドを呼び出して、ドライバーによって実装された完了ルーチンへのポインターを設定します。 要求を送信するには、 [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)メソッドを呼び出します。

要求を同期的に送信する場合は、次のメソッドを呼び出します。

-   [**WdfUsbTargetPipeReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously)
-   [**WdfUsbTargetPipeWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipewritesynchronously)

コード例については、これらのメソッドのリファレンストピックの「例」のセクションを参照してください。
### <a href="" id="step-3--implement-a-completion-routine-for-the-request-"></a>手順 3: 要求の完了ルーチンを実装します。

要求が非同期に送信される場合は、USB ドライバースタックが要求を完了したときに通知を受け取るために、完了ルーチンを実装する必要があります。 完了時に、フレームワークはドライバーの完了ルーチンを呼び出します。 フレームワークは、次のパラメーターを渡します。

-   要求オブジェクトへの WDFREQUEST ハンドル。
-   WDFIOTARGET は、要求の i/o ターゲットオブジェクトをハンドルします。
-   完了情報を格納している[**WDF\_要求\_完了\_PARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_completion_params)構造体へのポインター。 USB 固有の情報は、 **&gt;Parameters. usb**メンバーに格納されています。
-   [**Wdfrequestset補完ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)の呼び出しでドライバーによって指定されたコンテキストへの wdfcontext ハンドル。

完了ルーチンで、次のタスクを実行します。

-   要求の状態を確認するには、 **&gt;IoStatus. status**値を取得します。
-   USB ドライバースタックによって設定された USBD の状態を確認します。
-   パイプエラーが発生した場合は、エラー回復操作を実行します。 詳細については、「 [USB パイプのエラーから回復する方法](how-to-recover-from-usb-pipe-errors.md)」を参照してください。
-   転送されたバイト数を確認します。

    一括転送は、要求されたバイト数がデバイスとの間で転送されたときに完了します。 KMDF メソッドを呼び出すことによって要求バッファーを送信する場合は、 **PipeWrite パラメーター&gt;** で受け取った値を確認します。または&gt;Completion **params-&gt;PipeRead&gt;のパラメーター。** メンバーを入力します。

    USB ドライバースタックが1つのデータパケット内の要求されたバイトをすべて送信する単純な転送では、 **[長さ]** の値と、要求されたバイト数を比較することができます。 USB ドライバースタックが複数のデータパケットで要求を転送する場合、転送されたバイト数と残りのバイト数を追跡する必要があります。

-   合計バイト数が転送された場合は、要求を完了します。 エラー状態が発生した場合は、返されたエラーコードを使用して要求を完了します。 [**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)メソッドを呼び出して要求を完了します。 転送されたバイト数などの情報を設定する場合は、 [**Wdfrequestcompletewithinformation**](https://msdn.microsoft.com/library/windows/hardware/ff549945withinformation)を呼び出します。
-   情報で要求を完了するときは、バイト数が要求されたバイト数以下であることを確認してください。 これらの値は、フレームワークによって検証されます。 完了した要求で設定された長さが元の要求の長さよりも大きい場合、バグチェックが発生する可能性があります。

このコード例は、クライアントドライバーが一括転送要求を送信する方法を示しています。 ドライバーは、完了ルーチンを設定します。 そのルーチンを次のコードブロックに示します。

```cpp
/*++

Routine Description:

This routine sends a bulk write request to the 
USB driver stack. The request is sent asynchronously and 
the driver gets notified through a completion routine.

Arguments:

Queue - Handle to a framework queue object.
Request - Handle to the framework request object.
Length - Number of bytes to transfer.


Return Value:

VOID

--*/


VOID Fx3EvtIoWrite(
    IN WDFQUEUE  Queue,
    IN WDFREQUEST  Request,
    IN size_t  Length
    )
{
    NTSTATUS  status;
    WDFUSBPIPE  pipe;
    WDFMEMORY  reqMemory;
    PDEVICE_CONTEXT  pDeviceContext;

    pDeviceContext = GetDeviceContext(WdfIoQueueGetDevice(Queue));

    pipe = pDeviceContext->BulkWritePipe;

    status = WdfRequestRetrieveInputMemory(
                                           Request,
                                           &reqMemory
                                           );
    if (!NT_SUCCESS(status))
    {
        goto Exit;
    }

    status = WdfUsbTargetPipeFormatRequestForWrite(
                                                   pipe,
                                                   Request,
                                                   reqMemory,
                                                   NULL
                                                   );
    if (!NT_SUCCESS(status))
       {
        goto Exit;
    }

    WdfRequestSetCompletionRoutine(
                                   Request,
                                   BulkWriteComplete,
                                   pipe
                                   );

    if (WdfRequestSend( Request,
                        WdfUsbTargetPipeGetIoTarget(pipe),
                        WDF_NO_SEND_OPTIONS) == FALSE) 
       {
        status = WdfRequestGetStatus(Request);
        goto Exit;
    }

Exit:
    if (!NT_SUCCESS(status)) {
        WdfRequestCompleteWithInformation(
                                          Request,
                                          status,
                                          0
                                          );
    }
    return;
}
```

このコード例は、一括転送の完了ルーチンの実装を示しています。 クライアントドライバーは、完了ルーチンで要求を完了し、この要求情報 (状態と転送されたバイト数) を設定します。

```cpp
/*++

Routine Description:

This completion routine is invoked by the framework when
the USB drive stack completes the previously sent 
bulk write request. The client driver completes the 
the request if the total number of bytes were transferred
to the device.
In case of failure it queues a work item to start the 
error recovery by resetting the target pipe.

Arguments:

Queue - Handle to a framework queue object.
Request - Handle to the framework request object.
Length - Number of bytes to transfer.
Pipe - Handle to the pipe that is the target for this request.

Return Value:

VOID

--*/

VOID BulkWriteComplete(  
    _In_ WDFREQUEST                  Request,  
    _In_ WDFIOTARGET                 Target,  
    PWDF_REQUEST_COMPLETION_PARAMS   CompletionParams,  
    _In_ WDFCONTEXT                  Context  
    )  
{

    PDEVICE_CONTEXT deviceContext;

    size_t          bytesTransferred=0; 

    NTSTATUS        status;


    UNREFERENCED_PARAMETER (Target);
    UNREFERENCED_PARAMETER (Context);


    KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL, 
        "In completion routine for Bulk transfer.\n"));

    // Get the device context. This is the context structure that
    // the client driver provided when it sent the request.

    deviceContext = (PDEVICE_CONTEXT)Context;

    // Get the status of the request
    status = CompletionParams->IoStatus.Status;
    if (!NT_SUCCESS (status))
    {
        // Get the USBD status code for more information about the error condition.
        status = CompletionParams->Parameters.Usb.Completion->UsbdStatus;

        KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL,
            "Bulk transfer failed. 0x%x\n",  
            status));       

        // Queue a work item to start the reset-operation on the pipe
        // Not shown.

        goto Exit;
    }

    // Get the actual number of bytes transferred.
    bytesTransferred = 
            CompletionParams->Parameters.Usb.Completion->Parameters.PipeWrite.Length;

    KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL,
            "Bulk transfer completed. Transferred %d bytes. \n",  
            bytesTransferred));

Exit:

    // Complete the request and update the request with 
    // information about the status code and number of bytes transferred.

    WdfRequestCompleteWithInformation(Request, status, bytesTransferred);

    return;
}
```

## <a name="related-topics"></a>関連トピック
[USB i/o 転送](usb-device-i-o.md)  
[USB 一括エンドポイントで静的ストリームを開いて閉じる方法](how-to-open-streams-in-a-usb-endpoint.md)  



