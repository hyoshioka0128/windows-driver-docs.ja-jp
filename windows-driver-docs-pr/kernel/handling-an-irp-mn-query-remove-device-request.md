---
title: IRP_MN_QUERY_REMOVE_DEVICE 要求の処理
description: IRP_MN_QUERY_REMOVE_DEVICE 要求の処理
ms.assetid: 30177e51-5312-4a24-972e-0c1c2d183d18
keywords:
- IRP_MN_QUERY_REMOVE_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd033b68d4ce3b38d86da4e8f2a02edcf93f8d96
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838667"
---
# <a name="handling-an-irp_mn_query_remove_device-request"></a>IRP\_を処理\_クエリ\_\_デバイスの要求を削除する





PnP マネージャーは、この IRP を送信して、デバイスがコンピューターから削除されようとしていることをドライバーに通知し、コンピューターを邪魔せずにデバイスを削除できるかどうかを確認します。 また、この IRP は、ユーザーがデバイスのドライバーを更新するように要求したときにも送信されます。

PnP マネージャーは、システムスレッドのコンテキストでこの IRP を IRQL パッシブ\_レベルで送信します。

この IRP をデバイスのドライバーに送信する前に、次のことを行います。

-   デバイス (または関連デバイス) に通知するために登録されたすべてのユーザーモードアプリケーションに通知します。

    これには、デバイスで通知するために登録されたアプリケーション、デバイスの子孫の1つ (子デバイス、子の子など)、またはデバイスの削除関係の1つが含まれます。 アプリケーションは、 **RegisterDeviceNotification**を呼び出すことによって、このような通知を登録します。

    この通知に応答して、アプリケーションはデバイスの削除を準備するか (デバイスへのハンドルを閉じる)、またはクエリを失敗させることができます。

-   デバイス (または関連デバイス) で通知するために登録されたすべてのカーネルモードドライバーに通知します。

    これには、デバイスで通知するために登録されたドライバー、デバイスの子孫の1つ、またはデバイスの削除関係の1つが含まれます。 ドライバーは、 **eventcategory Targetdevicechange**のイベントカテゴリを使用して[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)を呼び出すことによって、この通知を登録します。

    この通知に応答して、ドライバーはデバイスの削除を準備するか (デバイスへのハンドルを閉じる)、またはクエリに失敗します。

-   [**Irp\_\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)を送信し、デバイスの子孫のドライバーに\_デバイスの IRP を削除\_ます。

-   (Windows 2000 以降のシステム)ファイルシステムがデバイスにマウントされている場合、PnP マネージャーは、ファイルシステムおよびすべてのファイルシステムフィルターにクエリ削除要求を送信します。 デバイスに開いているハンドルがある場合、通常、ファイルシステムはクエリ削除要求に失敗します。 それ以外の場合、ファイルシステムは通常、将来の作成を防ぐためにボリュームをロックします。 マウントされたファイルシステムがクエリ削除要求をサポートしていない場合、PnP マネージャーはデバイスのクエリ削除要求に失敗します。

上記のすべての手順が成功した場合、PnP マネージャーは、デバイスのドライバーに **\_デバイスを削除\_、IRP\_の\_クエリ**を送信します。

**\_デバイス要求を削除\_の IRP\_\_クエリ**は、デバイススタックの上位のドライバーによって最初に処理され、次に下位のドライバーごとに処理されます。 ドライバーは、 [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチン内の irp の削除を処理します。

IRP\_に応答して **\_デバイスを削除\_\_クエリ**を実行した場合、ドライバーは次の操作を行う必要があります。

1.  操作を中断せずに、デバイスをコンピューターから削除できるかどうかを判断します。

    次のいずれかに該当する場合、ドライバーはクエリ-削除 IRP を失敗させる必要があります。

    -   デバイスを削除すると、データが失われる可能性があります。

    -   コンポーネントにデバイスへのハンドルが開かれている場合。 (これは Windows 98/Me でのみ発生する問題です。 Windows 2000 以降のバージョンの Windows では開いているハンドルが開かれ、 **IRP\_\_クエリ\_\_デバイスの削除**が完了した後に開いているハンドルがある場合、クエリは失敗します。

    -   デバイスがページング、クラッシュダンプ、または休止状態のファイルのパスにあることを通知する ( [**IRP\_\_デバイス\_USAGE\_NOTIFICATION**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification) IRP を介して) ことを通知されたドライバーがある場合。

    -   ドライバーがデバイスに対して未処理のインターフェイス参照を持っている場合。 つまり、IRP\_に対する応答としてのインターフェイスが提供されています。これは、[**クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)要求で、インターフェイスが逆参照されていない\_です。

2.  デバイスを削除できない場合は、クエリの削除-IRP を失敗させます。

    **Irp&gt;iostatus. status**を適切なエラー状態 (通常はステータス\_失敗) に設定し、\_IO を使用して[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出します。このとき、\_増分はなく、ドライバーの*DispatchPnP*ルーチンから戻ります。 IRP を次の下位のドライバーに渡さないでください。

3.  ドライバーが以前に IRP\_送信したことがある場合は、ウェイクアップのためにデバイスを有効にするために[ **\_待機\_ウェイク**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)要求を待ってから、待機ウェイク IRP をキャンセルします。

4.  デバイスの以前の PnP 状態を記録します。

    ドライバーは、ドライバーが[ **\_\_\_\_irp**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)を受信したときのデバイスの PnP 状態を記録する必要があります。この場合、ドライバーは、クエリが取り消された場合にデバイスをその状態に返す必要があるため ([**irp\_の\_[キャンセル]\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)) を削除します。 以前の状態は通常 "開始済み" です。これは、ドライバーが正常に\_IRP を完了したときにデバイスが入力した状態であり、 [ **\_デバイスの要求\_開始**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)します。

    ただし、その他の以前の状態が発生する可能性があります。 たとえば、ユーザーがデバイスマネージャーによってデバイスを無効にした可能性があります。 または、 **IRP\_\_クエリ\_機能**の要求に応じて、親バスドライバー (またはバスドライバーのフィルタードライバー) によって、デバイスのハードウェアが無効になっていると報告されている可能性があります。 どちらの場合でも、無効になっているデバイスのドライバーは、irp\_\_\_**デバイス**要求を受信する前に\_デバイスの要求を**削除\_クエリ**を実行することで、irp\_を受け取ることができます。\_

5.  IRP を完了します。

    関数またはフィルタードライバーの場合:

    -   **Irp-&gt;iostatus. status**を STATUS\_SUCCESS に設定します。

    -   [**IoskipIoCallDriver Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を使用して次のスタックの場所を設定し、IRP を次の下位[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)のドライバーに渡します。

    -   **IoCallDriver**の状態を*DispatchPnP*ルーチンからの戻りステータスとして伝達します。

    -   IRP を完了しないでください。

    バスドライバーの場合:

    -   **Irp-&gt;iostatus. status**を STATUS\_SUCCESS に設定します。

    -   IO\_\_を増やさずに、IRP ([**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) を完了します。

    -   *DispatchPnP*ルーチンからを返します。

デバイススタック内のいずれかのドライバーで Irp\_が失敗した場合 **\_クエリ\_\_デバイスを削除**すると、PnP マネージャーは\_デバイススタックへの **\_デバイスの削除\_取り消し**\_を送信します。 これにより、ドライバーが IRP に失敗したかどうかを検出するために、クエリ-削除 IRP の[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンが不要になります。

ドライバーが IRP\_完了した後 **\_クエリ\_\_デバイスを削除**し、デバイスが削除待ち状態であると見なされた場合、ドライバーはデバイスの後続の作成要求をすべて失敗させる必要があります。 ドライバーは、すべての Irp を通常どおりに処理します。これにより、ドライバーが Irp を受信したときに、\_デバイスまたは**irp\_\_デバイスを削除** **\_削除\_キャンセル**するまで、その他のすべての irp が\_されます。\_

 

 




