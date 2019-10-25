---
title: SerCx2 カスタム-送信トランザクション
description: シリアルコントローラーハードウェアによっては、シリアルコントローラーにデータを書き込むための PIO やシステム DMA 以外のデータ転送機構を実装する場合があります。
ms.assetid: E72E68BC-A60A-41BE-8606-92A608648042
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eef16fa5c356043427279dd218dfa15d55897aa5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843045"
---
# <a name="sercx2-custom-transmit-transactions"></a>SerCx2 カスタム-送信トランザクション

シリアルコントローラーハードウェアによっては、シリアルコントローラーにデータを書き込むための PIO やシステム DMA 以外のデータ転送機構を実装する場合があります。 シリアルコントローラードライバーは、カスタム送信トランザクションをサポートして、このデータ転送メカニズムを SerCx2 で使用できるようにすることができます。

SerCx2 は、カスタム送信トランザクションを開始するために、ドライバーの[*EvtSerCx2CustomTransmitTransactionStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_start)イベントコールバック関数を呼び出し、書き込み ([**IRP\_MJ\_write**](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))) 要求とその説明をパラメーターとして渡します。トランザクションの書き込みバッファー。 この呼び出しでは、関数はトランザクションを開始し、を返します。 次に、ドライバーはトランザクションの完了と書き込み要求の完了を行います。

## <a name="creating-the-custom-transmit-object"></a>カスタム送信オブジェクトの作成

SerCx2 がシリアルコントローラードライバーの*EvtSerCx2CustomTransmitTransaction*Xxx * * 関数を呼び出すことができるようにするには、ドライバーが[**SerCx2CustomTransmitTransactionCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmittransactioncreate)メソッドを呼び出してこれらの関数を SerCx2 に登録する必要があります。 このメソッドは、入力パラメーターとして、SERCX2 へのポインター\_カスタム\_、ドライバーの*EvtSerCx2CustomTransmitTransaction*Xxx * * へのポインターを含む[ **\_トランザクション\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/ns-sercx-_sercx2_custom_transmit_transaction_config)構造体を転送します。関数.

ドライバーは、次の関数を実装する必要があります。

- [*EvtSerCx2CustomTransmitTransactionStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_start)

オプションとして、ドライバーは次の機能のいずれかまたは両方を実装できます。

- [*EvtSerCx2CustomTransmitTransactionInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_initialize)
- [*EvtSerCx2CustomTransmitTransactionCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_cleanup)

**SerCx2CustomTransmitTransactionCreate**メソッドは、カスタム送信オブジェクトを作成し、このオブジェクトへの[**SERCX2CUSTOMTRANSMITTRANSACTION**](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-object-handles#sercx2customtransmittransaction-object-handle)ハンドルを呼び出し元のドライバーに提供します。 ドライバーの*EvtSerCx2CustomTransmitTransaction*Xxx * * 関数はすべて、このハンドルを最初のパラメーターとして受け取ります。 次の SerCx2 メソッドは、このハンドルを最初のパラメーターとして受け取ります。

- [**SerCx2CustomTransmitTransactionInitializeComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmittransactioninitializecomplete)
- [**SerCx2CustomTransmitTransactionCleanupComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmittransactioncleanupcomplete)

## <a name="hardware-initialization-and-clean-up"></a>ハードウェアの初期化とクリーンアップ

シリアルコントローラードライバーによっては、カスタム送信トランザクションの開始時にシリアルコントローラーハードウェアを初期化したり、トランザクションの終了時にシリアルコントローラーのハードウェア状態をクリーンアップしたりすることが必要になる場合があります。

ドライバーが[*EvtSerCx2CustomTransmitTransactionInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_initialize)イベントコールバック関数を実装している場合、SerCx2 はこの関数を呼び出して、トランザクションを開始する前にシリアルコントローラーを初期化します。 実装されている場合、 *EvtSerCx2CustomTransmitTransactionInitialize*関数は[**SerCx2CustomTransmitTransactionInitializeComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmittransactioninitializecomplete)メソッドを呼び出して、ドライバーがシリアルコントローラーの初期化を完了したときに SerCx2 に通知する必要があります。

ドライバーが[*EvtSerCx2CustomTransmitTransactionCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_cleanup)イベントコールバック関数を実装している場合、SerCx2 はこの関数を呼び出して、トランザクションの終了後にハードウェアの状態をクリーンアップします。 実装されている場合、 *EvtSerCx2CustomTransmitTransactionInitialize*関数は[**SerCx2CustomTransmitTransactionCleanupComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmittransactioncleanupcomplete)メソッドを呼び出して、ドライバーがシリアルコントローラーのクリーンアップを完了したことを SerCx2 に通知する必要があります。

## <a name="accessing-the-request-object"></a>要求オブジェクトへのアクセス

SerCx2 は、カスタム送信トランザクションを開始するために、ドライバーの[*EvtSerCx2CustomTransmitTransactionStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_start)関数を呼び出し、関連付けられている書き込み要求 (WDFREQUEST オブジェクトハンドルでカプセル化されたもの) をパラメーターとしてこの関数に渡します。 このドライバーは、トランザクションの終了時にこの要求を完了するために、 [**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)などのメソッドを呼び出す役割を担います。 要求をすぐに完了できない限り、 *EvtSerCx2CustomTransmitTransactionStart*関数がを返す前に、ドライバーは[**Wdfrequestmarkcancelableex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)などのメソッドを呼び出して、要求をキャンセル可能としてマークする必要があります。

シリアルコントローラードライバーは、書き込み要求のデータバッファーにアクセスするために、 [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)などのメソッドを使用することはできません。 代わりに、ドライバーは、 *EvtSerCx2CustomTransmitTransactionStart*関数に渡された*Mdl*、 *Offset*、および*Length*パラメーター値を使用して、このバッファーにアクセスする必要があります。

カスタム送信トランザクションの実行中に、ドライバーは、要求オブジェクトにアタッチされているコンテキストにトランザクションに関する情報を格納することが必要になる場合があります。 その場合、ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)イベントコールバック関数は、 [**Wdfdeviceinitsetrequestattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)メソッドを呼び出して、要求オブジェクトに使用する属性を設定できます。 これらの属性には、要求コンテキストに使用する名前と割り当てサイズが含まれます。 この呼び出しで指定される要求属性は、ドライバーが[**SerCx2InitializeDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2initializedevice)メソッドの呼び出しで指定する要求属性と一致する必要があります。 これらの属性は、ドライバーが**SerCx2InitializeDevice**に渡す**SERCX2\_CONFIG**構造体の**requestattributes**メンバーで指定されます。 詳細については、「 [**SERCX2\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/ns-sercx-_sercx2_config)」を参照してください。

カスタム送信トランザクションの開始時にシリアルコントローラードライバーが受信する書き込み要求の場合、ドライバーフレームワークによって割り当てられた要求コンテキストは初期化されていません。 ドライバーは、この要求コンテキストをすべてゼロに初期化するために[**Rtlゼロメモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory)ルーチンを呼び出すことをお勧めします。
