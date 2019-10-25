---
title: ファンクション ドライバーでのデバイスの開始
description: ファンクション ドライバーでのデバイスの開始
ms.assetid: 148a3128-9cb1-4a2c-a62e-45199476d968
keywords:
- 関数ドライバー WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb7b5f39d6526a13b60bcf42266cdfae4766ed66
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838409"
---
# <a name="starting-a-device-in-a-function-driver"></a>ファンクション ドライバーでのデバイスの開始





関数ドライバーは、 [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定し、 [**irp\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)に渡して、デバイススタックを\_デバイスの要求を開始\_ます。また、すべての下位ドライバーが irp で終了するまで、開始操作を延期します。 カーネルイベントと*Iocompletion*ルーチンを使用して IRP 処理を延期する方法の詳細については、「[ドライバーが低いまで PnP IRP 処理を延期](postponing-pnp-irp-processing-until-lower-drivers-finish.md)する」を参照してください。

すべての下位ドライバーが IRP で終了した後で、その[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンが制御を取り戻すと、関数ドライバーはデバイスを起動するためのタスクを実行します。 関数ドライバーは、次のような手順でデバイスを起動します。

1.  低いドライバーが IRP に失敗した場合 ([**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)からエラーが返された場合) は、irp の処理を続行しないでください。 必要なクリーンアップを実行し、 *DispatchPnP*ルーチンから戻ります (この一覧の最後の手順に進みます)。

2.  低いドライバーが IRP を正常に処理した場合は、デバイスを起動します。

    デバイスを起動するための正確な手順は、デバイスによって異なります。 このような手順には、i/o スペースのマッピング、ハードウェアレジスタの初期化、デバイスの D0 電源状態の設定、 [**Ioconnectinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)による割り込みの接続などがあります。 IRP\_完了した後にデバイスを再起動している場合は、デバイスの要求を[ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device) 、ドライバーのデバイスの状態が復元される可能性があります。

    すべてのドライバーがデバイスにアクセスできるようにするには、デバイスの電源がオンになっている必要があります。 詳細について[は、「デバイスの電源投入](powering-up-a-device.md)」を参照してください。

    デバイスでウェイクアップが有効になっている場合、その電源ポリシーの所有者 (通常は関数ドライバー) は、デバイスの電源を入れた後、Irp\_完了してから **\_デバイス**の要求を開始\_まで待機します。 詳細については、「 [Wait/WAKE IRP の送信](sending-a-wait-wake-irp.md)」を参照してください。

3.  IRP を保持するキューで Irp を開始します。

    ドライバーによって定義された HOLD\_NEW\_REQUESTS フラグをクリアし、IRP を保持するキューで Irp を開始します。 ドライバーは、初めてデバイスを起動するときと、クエリの停止または停止の後にデバイスを再起動するときに、この処理を実行します。 詳細について[は、「デバイスが一時停止したときの受信 irp の保持](holding-incoming-irps-when-a-device-is-paused.md)」を参照してください。

4.  \[オプション\] [**Iosetdeviceinterfacestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)を呼び出して、デバイスのインターフェイスを有効にします。

    ドライバーが存在する場合は、そのインターフェイスを有効にします (または、INF で、または別のコンポーネント ( [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) ) に以前に登録していた場合)。

    Windows 2000 以降のバージョンの Windows では、 **irp\_の\_が開始\_デバイス**の irp が完了するまで、デバイスインターフェイスの到着通知は送信されません。これは、デバイスのすべてのドライバーが使用できることを示します。開始操作を完了しました。 また、PnP マネージャーは、デバイスのすべてのドライバーが開始 IRP を完了する前に受信したすべての作成要求に失敗します。

5.  IRP を完了します。

    関数ドライバーの*Iocompletion*ルーチンは、より多くの\_処理\_必要な\_を返しました。詳細については、「[ドライバーが終了するまで PnP IRP 処理を延期する](postponing-pnp-irp-processing-until-lower-drivers-finish.md)」で説明されているように、関数ドライバーの*DispatchPnP*を参照してください。ルーチンは、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して、i/o 完了の処理を再開する必要があります。

    関数ドライバーの開始操作が成功した場合、ドライバーは**Irp&gt;iostatus. status**を STATUS\_SUCCESS に設定し、IO\_\_priority boost を使用して**IoCompleteRequest**を呼び出します。*DispatchPnP*ルーチンから成功を\_します。

    関数ドライバーが開始操作中にエラーを検出した場合、ドライバーは IRP にエラー状態を設定し、 **IoCompleteRequest**を呼び出して IO\_\_インクリメントを呼び出し、その*DispatchPnP*ルーチンからエラーを返します。

    低いドライバーが IRP (**IoCallDriver**がエラーを返しました) に失敗した場合、関数ドライバーは**IoCompleteRequest**を呼び出して IO\_\_を呼び出し、 *DispatchPnP*ルーチンから**IoCallDriver**エラーを返します。 この場合、関数ドライバーは、irp に失敗した下位のドライバーによって状態が既に設定されているため、 **irp&gt;iostatus. status**を設定しません。

関数ドライバーは、\_デバイスの要求を**開始\_\_、IRP**を受信したときに、構造体を**irpsp-&gt;パラメーターで調べます。 AllocatedResources**と**irpsp-&gt;AllocatedResourcesTranslated。** PnP マネージャーによってデバイスに割り当てられた生リソースと変換されたリソースをそれぞれ記述します。 ドライバーは、デバッグを支援するために、デバイス拡張機能に各リソースリストのコピーを保存する必要があります。

リソースリストは[**CM\_リソース\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)の構造体であり、未加工のリストの各要素は翻訳されたリストの同じ要素に対応しています。 たとえば、 **AllocatedResources**\[0\] によって raw i/o ポート範囲が記述されている場合、 **AllocatedResourcesTranslated**\[0\] は翻訳後の同じ範囲を示します。 変換された各リソースには、物理アドレスとリソースの種類が含まれます。

ドライバーに変換されたメモリリソース (**CmResourceTypeMemory**) が割り当てられている場合は、 [**Mmmapiospace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace)を呼び出して、物理アドレスをデバイスレジスタにアクセスできる仮想アドレスにマップする必要があります。 ドライバーがプラットフォームに依存しない方法で動作するようにするには、返された各リソースをチェックし、必要に応じてマップします。

関数ドライバーは、すべてのデバイスリソースへのアクセスを確保するために **\_デバイス\_開始する IRP\_** に応答して、次の処理を実行する必要があります。

1.  **Irpsp-&gt;AllocatedResources パラメーター**をデバイス拡張機能にコピーします。

2.  **Irpsp-&gt;AllocatedResourcesTranslated パラメーター**をデバイス拡張機能にコピーします。

3.  ループで、 **AllocatedResourcesTranslated**内の各記述子要素を検査します。 記述子のリソースの種類が**CmResourceTypeMemory**の場合は、 **Mmmapiospace**を呼び出して、翻訳されたリソースの物理アドレスと長さを渡します。

ドライバーが Irp を受信し、 **\_デバイス\_停止**した場合は、 **irp\_** \_\_デバイス、または irp\_削除要求\_**突然**\_削除要求同様のループで[**Mmunmapiospace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace)を呼び出すことによって、マッピングを解放する必要があります。 また、ドライバーは、**デバイス要求\_開始\_IRP\_** が失敗する必要がある場合に、 **Mmunmapiospace**を呼び出す必要があります。

詳細については、「[バスの相対アドレスを仮想アドレスにマップする](mapping-bus-relative-addresses-to-virtual-addresses.md)」を参照してください。

 

 




