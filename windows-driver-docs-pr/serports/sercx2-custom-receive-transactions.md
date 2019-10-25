---
title: SerCx2 カスタム-受信トランザクション
description: シリアルコントローラーハードウェアによっては、シリアルコントローラーからデータを読み取るために PIO やシステム DMA 以外のデータ転送機構を実装している場合があります。
ms.assetid: 29849A8C-6656-444C-BE91-405A4BA2D5B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99101047422dfaeaebdf8e303cc62883ac73a132
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843050"
---
# <a name="sercx2-custom-receive-transactions"></a>SerCx2 カスタム-受信トランザクション

シリアルコントローラーハードウェアによっては、シリアルコントローラーからデータを読み取るために PIO やシステム DMA 以外のデータ転送機構を実装している場合があります。 シリアルコントローラードライバーは、カスタム受信トランザクションをサポートして、このデータ転送メカニズムを SerCx2 で使用できるようにすることができます。

カスタム受信トランザクションを開始するには、SerCx2 はドライバーの[*EvtSerCx2CustomReceiveTransactionStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_start)イベントコールバック関数を呼び出し、読み取り ([**IRP\_MJ\_読み取り**](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))) 要求と読み取りの説明をパラメーターとして渡します。トランザクションのバッファー。 この呼び出しでは、関数はトランザクションを開始し、を返します。 次に、ドライバーはトランザクションの完了と読み取り要求の完了を行います。

## <a name="creating-the-custom-receive-object"></a>カスタム受信オブジェクトの作成

SerCx2 がシリアルコントローラードライバーの*EvtSerCx2CustomReceiveTransaction*Xxx * * 関数を呼び出すことができるようにするには、ドライバーが[**SerCx2CustomReceiveTransactionCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactioncreate)メソッドを呼び出してこれらの関数を SerCx2 に登録する必要があります。 このメソッドは、入力パラメーターとして、SERCX2 へのポインターとして、ドライバーの*EvtSerCx2CustomReceiveTransaction*Xxx * * へのポインターを含む[ **\_トランザクション\_CONFIG 構造体を受け取るカスタム\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/ns-sercx-_sercx2_custom_receive_transaction_config)を受け取ります。関数.

ドライバーは、次の2つの関数を実装する必要があります。

- [*EvtSerCx2CustomReceiveTransactionStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_start)
- [*EvtSerCx2CustomReceiveTransactionQueryProgress*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn265203(v=vs.85))

オプションとして、ドライバーは次の3つの関数のいずれかまたはすべてを実装できます。

- [*EvtSerCx2CustomReceiveTransactionEnableNewDataNotification*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn265201(v=vs.85))
- [*EvtSerCx2CustomReceiveTransactionInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_initialize)
- [*EvtSerCx2CustomReceiveTransactionCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_cleanup)

**SerCx2CustomReceiveTransactionCreate**メソッドは、カスタム受信オブジェクトを作成し、このオブジェクトへの[**SERCX2CUSTOMRECEIVETRANSACTION**](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-object-handlessercx2customreceivetransaction-object-handle)ハンドルを呼び出し元のドライバーに提供します。 ドライバーの*EvtSerCx2CustomReceiveTransaction*Xxx * * 関数はすべて、このハンドルを最初のパラメーターとして受け取ります。 次の SerCx2 メソッドは、このハンドルを最初のパラメーターとして受け取ります。

- [**SerCx2CustomReceiveTransactionNewDataNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactionnewdatanotification)
- [**SerCx2CustomReceiveTransactionReportProgress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactionreportprogress)
- [**SerCx2CustomReceiveTransactionInitializeComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactioninitializecomplete)
- [**SerCx2CustomReceiveTransactionCleanupComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactioncleanupcomplete)

## <a name="hardware-initialization-and-clean-up"></a>ハードウェアの初期化とクリーンアップ

シリアルコントローラードライバーによっては、カスタム受信トランザクションの開始時にシリアルコントローラーハードウェアを初期化したり、トランザクションの終了時にシリアルコントローラーのハードウェア状態をクリーンアップしたりすることが必要になる場合があります。

ドライバーが[*EvtSerCx2CustomReceiveTransactionInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_initialize)イベントコールバック関数を実装している場合、SerCx2 はこの関数を呼び出して、トランザクションを開始する前にシリアルコントローラーを初期化します。 実装されている場合、 *EvtSerCx2CustomReceiveTransactionInitialize*関数は[**SerCx2CustomReceiveTransactionInitializeComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactioninitializecomplete)メソッドを呼び出して、ドライバーがシリアルコントローラーの初期化を完了したときに SerCx2 に通知する必要があります。

ドライバーが[*EvtSerCx2CustomReceiveTransactionCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_cleanup)イベントコールバック関数を実装している場合、SerCx2 はこの関数を呼び出して、トランザクションの終了後にハードウェアの状態をクリーンアップします。 実装されている場合、 *EvtSerCx2CustomReceiveTransactionInitialize*関数は[**SerCx2CustomReceiveTransactionCleanupComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactioncleanupcomplete)メソッドを呼び出して、ドライバーがシリアルコントローラーのクリーンアップを完了したことを SerCx2 に通知する必要があります。

## <a name="new-data-notifications"></a>新規-データ通知

オプションとして、シリアルコントローラードライバーは[*EvtSerCx2CustomReceiveTransactionEnableNewDataNotification*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn265201(v=vs.85))イベントコールバック関数を実装できます。 実装されている場合、SerCx2 はこの関数を使用して、カスタム受信トランザクションとして処理される読み取り要求の処理中に発生した間隔タイムアウトを効率的に管理します。

シリアルコントローラーによって受信された2つの連続するバイトの間隔がクライアントが指定した最大時間を超えた場合、間隔のタイムアウトが発生します。 周辺機器のドライバーから SerCx2 に読み取り要求が送信された後、シリアル接続された周辺機器から少なくとも1バイトのデータを受信するまで、間隔のタイムアウトは発生しません。 最初のバイトを受信した後、読み取り要求が到着してから、周辺機器からデータの最初のバイトが受信されるまでにかかる時間は、読み取り要求の残りのデータを受信するために必要な時間よりもかなり長くなる可能性があります。 詳細については、「 [**SERIAL\_のタイムアウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_timeouts)」を参照してください。

SerCx2 は、 *EvtSerCx2CustomReceiveTransactionEnableNewDataNotification*関数が実装されている場合、その関数を呼び出して、新しいデータ通知を有効にします。 この通知が有効になっていて、シリアルコントローラーが周辺機器から1バイト以上の新しいデータを受信した場合、または既にデータを受信 FIFO に保持している場合は、シリアルコントローラードライバー[**が**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactionnewdatanotification)SerCx2 に通知する SerCx2CustomReceiveTransactionNewDataNotification メソッド。

SerCx2 は、可能な間隔タイムアウトを検出するために、 [*EvtSerCx2CustomReceiveTransactionQueryProgress*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn265203(v=vs.85))イベントコールバック関数を定期的に呼び出して、前の間隔でデータが受信されたかどうかを確認します。 SerCx2 がデータの最初のバイトの受信を検出する方法は、シリアルコントローラードライバーが*EvtSerCx2CustomReceiveTransactionEnableNewDataNotification*関数を実装しているかどうかによって異なります。 この関数が実装されている場合、SerCx2 は関数を呼び出して新しいデータ通知を有効にし、データの最初のバイトが受信されたときにドライバーによって通知されます。 それ以外の場合、SerCx2 は、最初のバイトの受信を検出するために*EvtSerCx2CustomReceiveTransactionQueryProgress*関数を定期的に呼び出します。また、これらの呼び出しを行うには、プロセッサを定期的にスリープ解除する必要があります。 したがって、 *EvtSerCx2CustomReceiveTransactionEnableNewDataNotification*関数を実装するドライバーは、プロセッサが頻繁にスリープ解除されることを必要としないため、電力消費を減らすことができます。

SerCx2 は、カスタム受信トランザクションに対して保留中の新規データ通知を明示的に取り消しません。 ただし、次のいずれかの理由で、シリアルコントローラードライバーは、通知が有効で、ドライバーが関連する読み取り要求を完了する必要がある場合に、新しいデータ通知を暗黙的にキャンセルする必要がある場合があります。

- 読み取り要求がタイムアウトするか、取り消されます。
- シリアルコントローラーは、D0 デバイスの電源状態を終了して低電力状態にしようとしています。

通常、このドライバーは、 [**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)などのメソッドを呼び出して、要求を完了します。 要求が完了した後、ドライバーは**SerCx2CustomReceiveTransactionNewDataNotification**を呼び出さないでください。

## <a name="accessing-the-request-object"></a>要求オブジェクトへのアクセス

SerCx2 は、カスタム受信トランザクションを開始するために、ドライバーの[*EvtSerCx2CustomReceiveTransactionStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_start)関数を呼び出し、関連付けられている読み取り要求 (WDFREQUEST オブジェクトハンドルでカプセル化されたもの) をパラメーターとしてこの関数に渡します。 このドライバーは、トランザクションの終了時にこの要求を完了するために、 [**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)などのメソッドを呼び出す役割を担います。 要求をすぐに完了できない限り、 *EvtSerCx2CustomReceiveTransactionStart*関数がを返す前に、ドライバーは[**Wdfrequestmarkcancelableex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)などのメソッドを呼び出して、要求をキャンセル可能としてマークする必要があります。

シリアルコントローラードライバーは、 [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)などのメソッドを使用して、読み取り要求のデータバッファーにアクセスすることはできません。 代わりに、ドライバーは、 *EvtSerCx2CustomReceiveTransactionStart*関数に渡された*Mdl*、 *Offset*、および*Length*パラメーター値を使用して、このバッファーにアクセスする必要があります。

カスタム受信トランザクションの実行中に、ドライバーは、要求オブジェクトにアタッチされているコンテキストにトランザクションに関する情報を格納する必要がある場合があります。 その場合、ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)イベントコールバック関数は、 [**Wdfdeviceinitsetrequestattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)メソッドを呼び出して、要求オブジェクトに使用する属性を設定できます。 これらの属性には、要求コンテキストに使用する名前と割り当てサイズが含まれます。 この呼び出しで指定される要求属性は、ドライバーが[**SerCx2InitializeDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2initializedevice)メソッドの呼び出しで指定する要求属性と一致する必要があります。 これらの属性は、ドライバーが**SerCx2InitializeDevice**に渡す**SERCX2\_CONFIG**構造体の**requestattributes**メンバーで指定されます。 詳細については、「 [**SERCX2\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/ns-sercx-_sercx2_config)」を参照してください。

カスタム受信トランザクションの開始時にシリアルコントローラードライバーが受信する読み取り要求の場合、ドライバーフレームワークによって割り当てられた要求コンテキストは初期化されていません。 ドライバーは、この要求コンテキストをすべてゼロに初期化するために[**Rtlゼロメモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory)ルーチンを呼び出すことをお勧めします。
