---
Description: このトピックでは、USB 一括転送について、簡単な概要を説明します。
title: USB バルク転送要求の送信方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 173e34fbb1885aac2824d350341f7cbfe82a9dda
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368751"
---
# <a name="how-to-send-usb-bulk-transfer-requests"></a>USB バルク転送要求の送信方法


このトピックでは、USB 一括転送について、簡単な概要を説明します。 クライアント ドライバーが送信して、デバイスから大量のデータを受信する方法についての詳細な手順についても提供します。

-   [一括エンドポイントについて](#about-bulk-endpoints)
-   [一括トランザクション](#bulk-transactions)
-   [一括転送する場合の USB クライアント ドライバーのタスク](#usb-client-driver-tasks-for-a-bulk-transfer)
-   [一括転送要求の例](#bulk-transfer-request-example)
    -   [前提条件](#prerequisites)
    -   [手順 1: 転送バッファーを取得します。](#step-1--get-the-transfer-buffer--)
    -   [手順 2:書式を設定し、フレームワークの要求オブジェクトを USB ドライバー スタックに送信します。](#step-2--format-and-send-a-framework-request-object-to-the-usb-driver-stack-)
    -   [手順 3:要求の完了ルーチンを実装します。](#step-3--implement-a-completion-routine-for-the-request-)

## <a name="about-bulk-endpoints"></a>一括エンドポイントについて


USB 一括のエンドポイントは、大量のデータを転送できます。 一括転送は、信頼性の高いハードウェア エラーの検出を許可すること、およびハードウェアの再試行回数制限にはが含まれます。 一括エンドポイントへの転送、帯域幅がバス上に予約されていません。 さまざまな種類のエンドポイントを対象とする複数の転送要求が存在する場合、コント ローラー最初にスケジュール時間の重要なデータの転送などアイソクロナスし、パケットを中断します。 未使用の帯域幅が、バス場合にのみ、コント ローラーのスケジュールを一括転送します。 バス上の他の大量のトラフィックがない、場所を一括転送を高速に指定できます。 ただし、その他の転送でビジー状態に、バスは、データの一括が無期限に待機できます。

一括エンドポイントの主な機能を次に示します。

-   一括エンドポイントは、省略可能です。 大量のデータを転送する必要がある USB デバイスがサポートされます。 たとえば、フラッシュ ドライブ、プリンターやスキャナーからのデータ ファイルを転送します。
-   USB フル_スピード、高速および SuperSpeed デバイスは、一括のエンドポイントをサポートします。 低速デバイスは、一括のエンドポイントをサポートしていません。
-   エンドポイントは、一方向と、データは、IN または OUT の方向にも転送されます。 一括のエンドポイントは、ホストからデバイスへのデータを送信するデバイスからデータをホストと外部エンドポイントの一括が使用される読み取りに使用されます。
-   エンドポイントは、エラーをチェックする CRC ビットを備え、データの整合性を提供します。 CRC エラーなどのデータが自動的に再送信されます。
-   SuperSpeed 一括のエンドポイントは、ストリームをサポートできます。 ストリームは、パイプのストリームを個別に転送を送信するホストを許可します。
-   一括エンドポイントの最大パケット サイズは、デバイスのバス速度に依存します。 フル_スピード、高速および SuperSpeed;最大パケット サイズは、それぞれ 64、512、1024 バイトです。

## <a name="bulk-transactions"></a>一括トランザクション


他のすべての USB 転送のように、ホストは常に一括転送を開始します。 通信、ホストとターゲット エンドポイント間で行わをれます。 USB プロトコルでは、一括トランザクションで送信されるデータの任意の形式は適用されません。

バス上のホストとデバイスの通信方法は、デバイスが接続速度によって異なります。 このセクションでは、高速および SuperSpeed 一括転送ホストとデバイス間の通信を示す例をいくつかについて説明します。

Beagle、Ellisys、LeCroy USB プロトコル アナライザーなどの任意の USB アナライザーを使用して、トランザクションとパケットの構造を確認できます。 アナライザー、デバイスは、データを送信または、ネットワーク経由で USB デバイスから受信する方法を示します。 この例では、LeCroy USB アナライザーによってキャプチャされた一部のトレースを調べてみましょう。 この例では、参照するだけです。 これは Microsoft によって、保証ではありません。

**一括をトランザクションの例**

このアナライザー トレースは、高速でトランザクションを例の一括を示しています。

![データ トランザクションの例のトレース。](images/bulk-out-hs.png)

上記のトレースでは、ホストは、PID (出力トークン) の設定を外部のトークンのパケットを送信することによって、高速な一括エンドポイントへの転送を一括を開始します。 パケットには、デバイスとターゲット エンドポイントのアドレスが含まれています。 出力パケットの場合に、ホストは、一括ペイロードを含むデータ パケットを送信します。 エンドポイントが受信データを受け入れる場合は、ACK パケットを送信します。 この例でわかりますホストがデバイス アドレス: 1; に 31 バイトを送信します。エンドポイント アドレス:2.

エンドポイントは、データ パケットが到着して、データを受信するようになって時にビジー状態、デバイスは NAK パケットを送信できます。 その場合は、ホストは、デバイスに PING パケットの送信を開始します。 デバイスは、デバイスがデータを受信する準備ができていない限り、NAK パケットで応答します。 デバイスの準備ができたら、ACK パケットに応答します。 ホストは、アウト転送を再開し、できます。

このアナライザー トレースは、トランザクションを SuperSpeed 一括例を示します。

![データ トランザクションの例のトレース。](images/bulk-out.png)

上記のトレースでは、ホストは、データ パケットを送信して SuperSpeed 一括エンドポイントへのアウト トランザクションを開始します。 データ パケットには、一括ペイロード、デバイス、およびエンドポイント アドレスが含まれています。 この例でわかりますホストがデバイス アドレス: 4; に 31 バイトを送信します。エンドポイント アドレス:2.

デバイスは、受信しデータ パケットが受信確認し、ホストに ACK パケットを送信します。 エンドポイントは、データ パケットが到着して、データを受信するようになって時にビジー状態、デバイスは NRDY パケットを送信できます。 高速でとは異なり、NRDY パケットを受信した後、ホスト繰り返しポーリングしないデバイス。 代わりに、ホストでは、デバイスから、ERDY を待機します。 デバイス準備ができたら、ERDY パケットを送信し、ホストは、エンドポイントにデータを送信します。

**一括でトランザクションの例**

このアナライザー トレースは、高速で一括でトランザクションの例を示します。

![データ トランザクションの例のトレース。](images/bulk-in-hs.png)

上記のトレースに、ホストは PID 内に設定のトークンのパケットを送信することによって、トランザクションを開始します (トークン) にします。 デバイスは、一括ペイロードを使用したデータ パケットを送信します。 エンドポイントは、送信するデータがないかはまだデータを送信する準備ができて、デバイスは NAK ハンドシェイク パケットを送信できます。 ホストは、デバイスからの ACK パケットを受信するまでの転送を再試行します。 ACK パケットは、デバイスが、データを受け入れることを意味します。

このアナライザー トレースは、SuperSpeed 一括 IN トランザクション例を示します。

![データ トランザクションの例のトレース。](images/bulk-in.png)

SuperSpeed エンドポイントから一括で転送を開始するには、ホストは、ACK パケットを送信することによって、一括トランザクションを開始します。 USB 仕様バージョン 3.0 最適化転送の最初の部分はこの ACK をマージすることで、パケットの ACK パケットを 1 つにします。 SuperSpeed、用のトークンでは、代わりに、ホストは送信一括転送を開始する、確認トークン。 デバイスは、データ パケットで応答します。 ホストは、ACK パケットを送信することによって、データ パケットを確認します。 エンドポイントがビジー状態データを送信できなかった場合は、デバイスは NRDY のステータスを送信できます。 その場合は、ホストは、デバイスから取得した、ERDY パケットまでの待機します。

## <a name="usb-client-driver-tasks-for-a-bulk-transfer"></a>一括転送する場合の USB クライアント ドライバーのタスク


アプリケーションや、ホスト上のドライバーは、送信または受信データを一括転送を常に開始します。 クライアント ドライバーでは、USB ドライバー スタックに要求を送信します。 USB ドライバー スタックは、ホスト コント ローラーに要求 プログラムし、プロトコル パケットを送信します (前のセクションで説明) に従って、ネットワーク経由でデバイス。

クライアント ドライバーが、アプリケーションのまたは別のドライバーの要求の結果として一括転送する場合に要求を送信する方法を見てみましょう。 または、ドライバーは、独自の転送を開始できます。 アプローチに関係なく、ドライバーは、転送バッファーと、一括転送を開始するには、要求が必要です。

要求は、framework 要求オブジェクトに記載されている、KMDF ドライバー (を参照してください[WDF 要求オブジェクト参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/))。 クライアント ドライバーでは、USB ドライバー スタックに要求を送信する WDFREQUEST ハンドルを指定することで、要求オブジェクトのメソッドを呼び出します。 クライアント ドライバーがアプリケーションまたは別のドライバーからの要求に対する応答で一括転送を送信する場合、フレームワークは要求オブジェクトを作成し、フレームワークのキュー オブジェクトを使用して、クライアント ドライバーに要求を提供します。 その場合は、クライアント ドライバーでは、一括転送を送信する目的での要求を使用できます。 クライアント ドライバーでは、要求が開始された場合、ドライバーは、独自の要求オブジェクトを割り当てることもできます。

アプリケーションまたは別のドライバーは、送信または要求されたデータ、転送バッファーは、フレームワークによって、ドライバーに渡されます。 または、クライアント ドライバーは、転送バッファーを割り当てるし、ドライバーは、独自の転送を開始する場合は、要求オブジェクトを作成します。

クライアント ドライバーの主要なタスクを次に示します。

1.  転送バッファーを取得します。
2.  形式を取得し、フレームワークの要求オブジェクトを USB ドライバー スタックに送信します。
3.  USB ドライバー スタックは、要求を完了時に受け取る通知を完了ルーチンを実装します。

このトピックでは、ドライバーが、アプリケーションの要求の結果を送信または受信データの一括転送を開始する例を使用してこれらのタスクについて説明します。

デバイスからデータを読み取り、クライアント ドライバーは、継続的なリーダー オブジェクトを提供するフレームワークを使用できます。 詳細については、次を参照してください。 [USB パイプからデータを読み取るための継続的なリーダーを使用する方法](how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md)します。

## <a name="bulk-transfer-request-example"></a>一括転送要求の例


アプリケーションがデバイスにデータの読み書きが、サンプル シナリオを検討してください。 アプリケーションでは、このような要求を送信する Windows Api を呼び出します。 この例では、アプリケーションは、デバイス インターフェイスのカーネル モードで、ドライバーによって発行された GUID を使用して、デバイスを識別するハンドルを開きます。 その後、アプリケーションを呼び出す[ **ReadFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)または[ **WriteFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile)または書き込み要求を読み取りを開始します。 アプリケーションでその呼び出しでは、データの読み取りまたは書き込みを格納するバッファーとそのバッファーの長さも指定します。

I/O マネージャーが要求を受信するには、I/O 要求パケット (IRP)、作成およびクライアント ドライバーに転送します。

フレームワーク要求を受信するには、フレームワーク、要求オブジェクトを作成およびフレームワークのキュー オブジェクトに追加します。 フレームワークは、新しい要求が処理を待機しているクライアント ドライバーを通知します。 通知用のドライバーのキューのコールバック ルーチンを呼び出すことによって行われる[ *EvtIoRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)または[ *EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)します。

フレームワークは、クライアント ドライバーに要求を配信する際は、これらのパラメーターを受け取る。

-   要求を格納するフレームワークのキュー オブジェクトへのハンドルを WDFQUEUE。
-   この要求に関する詳細を含むフレームワーク要求オブジェクトへのハンドルを WDFREQUEST します。
-   転送長さでは、読み取りまたは書き込みバイト数が、します。

クライアント ドライバーの実装で[ *EvtIoRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)または[ *EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)ドライバーを検査、要求のパラメーターとは必要に応じて検証チェックを実行します。

SuperSpeed 一括エンドポイントのストリームを使用している場合は、KMDF がストリームを本質的にサポートされていないために、URB で、依頼が送信されます。 一括エンドポイントのストリームに転送するための要求を送信する方法の詳細については、次を参照してください。[を開いて、USB 一括エンドポイントで静的なストリームを閉じる方法](how-to-open-streams-in-a-usb-endpoint.md)します。

ストリームを使用していない場合は、次の手順に従って、要求を送信する KMDF が定義されているメソッドを使用できます。

### <a name="prerequisites"></a>前提条件

開始する前に、この情報があることを確認します。

-   クライアント ドライバーが framework USB ターゲット デバイス オブジェクトを作成して、WDFUSBDEVICE ハンドルを呼び出すことによって取得する必要があります、 [ **WdfUsbTargetDeviceCreateWithParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)メソッド。

    Microsoft Visual Studio Professional 2012 と共に用意されている USB テンプレートを使用する場合、テンプレート コードは、これらのタスクを実行します。 テンプレート コードでは、ターゲット デバイス オブジェクトを識別するハンドルを取得し、デバイス コンテキストに格納します。 詳細については、「デバイスのソース コード」を参照してください[USB クライアント ドライバー コード構造 (KMDF) について](understanding-the-kmdf-template-code-for-usb.md)します。

-   この要求に関する詳細を含むフレームワーク要求オブジェクトへのハンドルを WDFREQUEST します。
-   読み取りまたは書き込みバイト数。
-   対象のエンドポイントに関連付けられている framework パイプ オブジェクト WDFUSBPIPE ハンドルです。 列挙のパイプでデバイスの構成時にパイプ ハンドルを取得する必要があります。 詳細については、次を参照してください。 [USB パイプを列挙する方法](how-to-get-usb-pipe-handles.md)します。

    一括エンドポイントは、ストリームをサポートする場合は、パイプのストリームへのハンドルが必要です。 詳細については、次を参照してください。[を開いて、USB 一括エンドポイントで静的なストリームを閉じる方法](how-to-open-streams-in-a-usb-endpoint.md)します。

### <a href="" id="step-1--get-the-transfer-buffer--"></a>手順 1:転送バッファーを取得します。

転送バッファーと転送バッファー MDL 送信または受信するデータが含まれています。 このトピックでは、送信または転送バッファー内のデータの受信が前提としています。 転送バッファーが WDF のメモリ オブジェクトに説明されている (を参照してください[メモリ オブジェクトの参照を WDF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/))。 転送バッファーに関連付けられているメモリ オブジェクトを取得するには、これらのメソッドのいずれかを呼び出します。

-   転送要求で一括を呼び出し、 [ **WdfRequestRetrieveOutputMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)メソッド。
-   転送要求を一括で呼び出し、 [ **WdfRequestRetrieveInputMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)メソッド。

クライアント ドライバーは、このメモリを解放する必要はありません。 メモリは、親の要求オブジェクトに関連付けられたされ、親がリリースされたときに解放されます。

### <a href="" id="step-2--format-and-send-a-framework-request-object-to-the-usb-driver-stack-"></a>手順 2:書式を設定し、フレームワークの要求オブジェクトを USB ドライバー スタックに送信します。

非同期的または同期的には、転送要求を送信できます。

非同期のメソッドを次に示します。

-   [**WdfUsbTargetPipeFormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread)
-   [**WdfUsbTargetPipeFormatRequestForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforwrite)

このリストのメソッドは、要求を書式設定します。 要求を非同期的に送信する場合、ポインター ドライバー実装完了ルーチンを呼び出すことによって設定、 [ **WdfRequestSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)メソッド (次の手順で説明)。 要求を送信する、 [ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)メソッド。

同期的に、要求を送信する場合は、これらのメソッドを呼び出します。

-   [**WdfUsbTargetPipeReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously)
-   [**WdfUsbTargetPipeWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipewritesynchronously)

コード例については、これらのメソッドの参照トピックの「例」を参照してください。
### <a href="" id="step-3--implement-a-completion-routine-for-the-request-"></a>手順 3:要求の完了ルーチンを実装します。

要求を非同期的に送信する場合は、USB ドライバー スタックは、要求を完了時に受け取る通知を完了ルーチンを実装する必要があります。 完了すると、フレームワークは、ドライバーの完了ルーチンを呼び出します。 フレームワークは、これらのパラメーターを渡します。

-   WDFREQUEST 要求オブジェクトをハンドルします。
-   WDFIOTARGET 要求に対して I/O ターゲット オブジェクトのハンドルします。
-   ポインターを[ **WDF\_要求\_完了\_PARAMS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/ns-wdfrequest-_wdf_request_completion_params)完了の情報を含む構造体。 USB に固有の情報に含まれている、 **CompletionParams -&gt;Parameters.Usb**メンバー。
-   ドライバーは、その呼び出しで指定されるコンテキストへのハンドルを WDFCONTEXT [ **WdfRequestSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)します。

完了のルーチンでは、これらのタスクを実行します。

-   取得することによって、要求の状態を確認、 **CompletionParams -&gt;IoStatus.Status**値。
-   USB ドライバー スタックが設定 USBD の状態を確認します。
-   パイプのエラーが発生した場合は、エラーの回復操作を実行します。 詳細については、次を参照してください。 [USB パイプ エラーから回復する方法](how-to-recover-from-usb-pipe-errors.md)します。
-   転送されたバイト数を確認します。

    要求されたバイト数をまたはデバイスから転送されたときに、一括転送が完了しました。 KMDF メソッドを呼び出すことによって、要求のバッファーを送信する場合で受信した値を確認し、 **CompletionParams -&gt;Parameters.Usb.Completion -&gt;Parameters.PipeWrite.Length**または**CompletionParams -&gt;Parameters.Usb.Completion -&gt;Parameters.PipeRead.Length**メンバー。

    USB ドライバー スタックが 1 つのデータ パケットで要求されたすべてのバイトを送信する単純な転送、比較を確認することができます、**長さ**要求されたバイト数の値。 USB ドライバー スタックは、複数のデータ パケットに要求を転送する場合は、する必要がありますの追跡転送されたバイト数と残りのバイト数。

-   転送された合計バイト数、要求を完了します。 エラーが発生した場合は、返されたエラー コードで要求を完了します。 呼び出すことによって、要求を完了、 [ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)メソッド。 場合は、転送されたバイト数などの情報を設定するには、呼び出して[ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549945withinformation)します。
-   情報を含む要求を完了するとバイト数でなければならないことと同じ、または要求されたバイト数よりも小さいかを確認します。 フレームワークは、これらの値を検証します。 長さを設定完了済みの要求がより大きい場合、元の要求の長さのバグチェックが発生することができます。

このコード例では、クライアント ドライバーが一括転送要求を送信する方法を示します。 ドライバーは、完了ルーチンを設定します。 ルーチンは、次のコード ブロックに表示されます。

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

このコードの例では、一括転送する場合、完了の日常的な実装を示します。 クライアント ドライバーは、完了ルーチンの要求を完了し、この要求の情報を設定します。 状態とバイト数を転送します。

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
[USB I/O の転送](usb-device-i-o.md)  
[USB 一括エンドポイントで静的なストリームを開閉する方法](how-to-open-streams-in-a-usb-endpoint.md)  



