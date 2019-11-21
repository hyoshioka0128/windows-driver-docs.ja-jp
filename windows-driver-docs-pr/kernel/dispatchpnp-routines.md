---
title: DispatchPnP ルーチン
description: DispatchPnP ルーチン
ms.assetid: 909d99ac-5bd3-4b12-bfb4-79713cf2a156
keywords:
- ディスパッチルーチン WDK カーネル、DispatchPnP ルーチン
- DispatchPnP ルーチン
- PnP ディスパッチルーチン WDK カーネル
- Irp WDK カーネル、プラグアンドプレイディスパッチルーチン
- プラグアンドプレイディスパッチルーチン WDK カーネル
- IRP_MJ_PNP i/o 関数コード
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 251f5d5b45a037b91b3c88ec47b18bb4054bfef9
ms.sourcegitcommit: 46853426563bfac36651565181d7edac339f63af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74261429"
---
# <a name="dispatchpnp-routines"></a>DispatchPnP ルーチン





ドライバーの[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、 [**irp\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp) I/o 関数コードの irp を処理することによって、[プラグアンドプレイ](implementing-plug-and-play.md)をサポートします。 **IRP\_MJ\_PNP**関数コードに関連付けられているのは、いくつかのマイナー i/o 関数コードです (「[プラグアンドプレイの小さな irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)」を参照)。一部のドライバーは処理する必要があり、一部のドライバーは必要に応じて処理できます。 PnP マネージャーは、これらのマイナー関数コードを使用して、デバイスを開始、停止、および削除し、デバイスに関するドライバーを照会するようにドライバーに指示します。

デバイスのすべてのドライバーには、デバイスの PnP Irp を処理する機会が必要です。ただし、関数またはフィルタードライバーが IRP を失敗させることが許可されている場合は例外です。

各ドライバーの*DispatchPnP*ルーチンは、次の規則に従う必要があります。

-   関数またはフィルタードライバーは、デバイススタック内の次のドライバーに PnP Irp を渡す必要があります。ただし、関数またはフィルタードライバーが IRP を処理し、リソースが不足していることが原因でエラーが発生した場合 (たとえば、リソースが不足している場合など)。

    いずれかのドライバーでエラーが発生しない限り、デバイスのすべてのドライバーにデバイスの PnP Irp を処理する機会がある必要があります。 PnP マネージャーは、デバイススタックの最上位のドライバーに Irp を送信します。 関数とフィルタードライバーは、IRP を次のドライバーに渡し、親バスドライバーが IRP を完了します。 詳細については[、「PnP irp をデバイススタックに渡す](passing-pnp-irps-down-the-device-stack.md)」を参照してください。

    Irp を処理しようとしてエラー (リソース不足など) が発生した場合、ドライバーは IRP を失敗させる可能性があります。 ドライバーが処理していないコードを使用して IRP を受信した場合、ドライバーは IRP を失敗させることはできません。 IRP の状態を変更せずに、このような IRP を次のドライバーに渡す必要があります。

-   ドライバーは特定の PnP Irp を処理する必要があり、必要に応じて他の Irp を処理することができます。

    各 PnP ドライバーは、特定の Irp を処理する必要があります。たとえば、 [**irp\_、\_デバイス\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)するなどの特定の irp を処理し、必要に応じて他の irp を処理できます。 各種類のドライバー (関数ドライバー、フィルタードライバー、およびバスドライバー) で必要とされる Irp の詳細については[プラグアンドプレイ「小さな irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps) 」を参照してください。

    ドライバーは、適切なエラー状態で必要な PnP IRP を失敗させることができますが、このような IRP でサポートされて\_いない\_、ドライバーがステータスを返さないようにする必要があります。

-   ドライバーが PnP IRP を正常に処理した場合、ドライバーは IRP ステータスを success に設定します。 状態を設定するために、スタック内の別のドライバーに依存しません。

    ドライバーは**irp&gt;iostatus. status**を STATUS\_SUCCESS に設定して、ドライバーが irp を正常に処理したことを PnP マネージャーに通知します。 一部の Irp では、非バスドライバーが親バスドライバーに依存して状態を成功に設定できる場合があります。 ただし、これはリスクの高い方法です。 整合性と堅牢性を確保するために、ドライバーは、正常に処理される各 PnP IRP の IRP ステータスを成功に設定する必要があります。

-   ドライバーが IRP に失敗した場合、ドライバーは、エラー状態を使用して IRP を完了します。 IRP は次のドライバーに渡されません。

    Irp [ **\_\_クエリ\_停止して\_デバイスを停止**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)するような irp を失敗させるには、ドライバーが**Irp-&gt;iostatus**を設定\_失敗します。 その他の Irp のエラー状態の値には、\_\_リソースの不足、状態\_無効\_デバイス\_状態があります。

    ドライバーは、処理する Irp に対して\_サポートされていない\_状態を設定しません。 これは、PnP マネージャーによって設定された初期状態です。 この状態で IRP が完了した場合は、スタック内のドライバーによって IRP が処理されなかったことを意味します。すべてのドライバーは、IRP を次のドライバーに渡しました。

-   ドライバーは、IRP の参照ページで指定されているように、 [**Iocompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチン (irp によるデバイススタックのバックアップ)、またはその両方で、ディスパッチルーチン内の PnP IRP を処理する必要があります。

    [**IRP\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)などの一部の PnP irp は、デバイススタックの一番上にあるドライバーによって最初に処理される必要があります。その後、次に低いドライバーごとに処理する必要があります。 その他 ( [**IRP\_、\_デバイスの開始\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)など) は、最初に親バスドライバーによって処理される必要があります。 また、 [**IRP\_\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)などの他の機能は、デバイススタックとバックアップ方法の両方で処理できます。 各 PnP IRP に適用されるルールについては、「[プラグアンドプレイの小さな irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps) 」を参照してください。 親バスドライバーによって最初に処理される必要がある PnP Irp の処理の詳細については[、「ドライバーが終了するまで PNP irp の処理を延期](postponing-pnp-irp-processing-until-lower-drivers-finish.md)する」を参照してください。

-   ドライバーでは、irp に対してデバイススタック上で irp に情報を追加し、IRP のバックアップ方法に関する情報を変更または削除する必要があります。

    PnP クエリの IRP に応答して情報を返す場合、ドライバーはこの規則に従って、デバイスのレイヤー化されたドライバーで渡される情報を有効にする必要があります。

-   明示的に文書化されている場合を除き、ドライバーは、特定の順序で送信される PnP Irp に依存しないようにする必要があります。

-   ドライバーは、PnP IRP を送信するときに、デバイススタックの最上位のドライバーに IRP を送信する必要があります。

    ほとんどの PnP Irp は PnP マネージャーによって送信されますが、ドライバーによって送信される場合があります (たとえば、 [**IRP\_\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface))。 ドライバーは、デバイススタックの一番上にあるドライバーに PnP IRP を送信する必要があります。 [**IoGetAttachedDeviceReference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference)を呼び出して、デバイススタックの一番上にあるドライバーのデバイスオブジェクトへのポインターを取得します。


 

 




