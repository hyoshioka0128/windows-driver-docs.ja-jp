---
title: オプションのディスパッチ ルーチン
description: オプションのディスパッチ ルーチン
ms.assetid: 38a3fcc9-237d-432d-85db-1594697c96a5
keywords:
- ディスパッチルーチン WDK カーネル、省略可能
- オプションのディスパッチルーチン WDK カーネル
- 大容量記憶装置デバイス WDK ディスパッチルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91eab670c8d73244748bd778682aa5ce5daeb065
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827723"
---
# <a name="optional-dispatch-routines"></a>オプションのディスパッチ ルーチン





ドライバーには、次のディスパッチルーチンが含まれる場合があります。

-   [*DispatchCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_CLEANUP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)は、ターゲットデバイスオブジェクトに関連付けられているファイルオブジェクトの最後のハンドルが閉じられていることを示します。 ファイルオブジェクトに対する未処理の i/o 要求がまだ存在している可能性があります。 ドライバーは、特定のファイルハンドルに固有ではないクリーンアップを実行する*DispatchCleanup*ルーチンを実装できます。 ドライバーは、同じ目的で[*DispatchClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンを使用することもできます。

-   [*DispatchQueryInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、 [ *DispatchSetInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    一部の最上位レベルのドライバーでは、 [**irp\_MJ\_クエリ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-query-information)、および[**irp\_MJ\_設定\_情報**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-set-information)irp を処理する必要がある場合があります。 このような要求は、ユーザーモードのアプリケーション、カーネルモードコンポーネント、またはドライバーが、ユーザーモードの要求者がハンドルを持っている (ドライバーのデバイスオブジェクトを表す) ファイルオブジェクトの長さに関する情報を要求していること、またはユーザーモードであることを示しています。リクエスターが、そのファイルオブジェクトにファイルの終わりを設定しようとしています。

    並列クラスおよびシリアルデバイスドライバーは、[**ファイル\_標準\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_standard_information)またはファイルを設定することによって、これらの要求を処理します。これには、情報の長さや位置を示す0に[ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)ます。 その他の最上位レベルのデバイスドライバーでは、特にユーザーモードアプリケーションやカーネルモードドライバーが C ランタイム関数を呼び出してファイルオブジェクトを操作する場合に、これらの要求をサポートする必要があります。 ファイルシステムドライバーは、これらの最高レベルのデバイスドライバーよりも多くの要求をサポートする必要があります。

-   [*DispatchFlushBuffers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    デバイスにデータをキャッシュしたり、ドライバーによって割り当てられたメモリ内にデータをバッファーしたりするドライバーは、 [**IRP\_MJ\_フラッシュ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)を受け取る可能性があります。 この要求を受信すると、ドライバーがバッファー内のデータを書き込んだり、キャッシュされたデータをデバイスにフラッシュしたり、デバイスから読み取られたバッファーまたはキャッシュされたデータを破棄したりする必要があることを示します。

    たとえば、システムキーボードおよびマウスクラスドライバーは、デバイスからの入力データの内部リングバッファーがあるため、フラッシュ要求をサポートしています。 その上にある大容量記憶装置とドライバーのドライバーも、この要求をサポートしています。

-   [*DispatchShutdown*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    システムがシャットダウンする前に呼び出される可能性のあるすべてのドライバーは、 [**IRP\_MJ\_のシャットダウン**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)を処理する必要があります。 *DispatchShutdown*ルーチンは、電源マネージャーがシステムをシャットダウンするシステムセット-電源 IRP を送信する前に、ドライバーによって決定されたすべてのクリーンアップを実行する必要があります。 ドライバーは、 [**IoRegisterShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregistershutdownnotification)または[**IoRegisterLastChanceShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterlastchanceshutdownnotification)を呼び出して、シャットダウン通知を登録できます。

大容量記憶装置のドライバーと中間のドライバーは、システムがシャットダウンされるときに、最上位レベルのファイルシステムドライバーを使用してシャットダウン Irp を送信することができます。 つまり、FSD は、システムがシャットダウンされる前に、キャッシュされたファイルデータが周辺機器に書き込まれることを確認し、基になるドライバーを呼び出してデバイスのキャッシュまたはバッファーからデータをフラッシュする必要があります。

データを内部的にキャッシュする大容量記憶装置のドライバーは、 *DispatchShutdown*および*DispatchFlushBuffers*ルーチンを提供する必要があります。 大容量記憶装置ドライバーがメモリ内のデータをバッファーするが、そのデバイスに内部キャッシュがない場合は、 *DispatchShutdown*ルーチンと*DispatchFlushBuffers*ルーチンも提供する必要があります。

Irp\_MJ を処理するドライバーの上に階層化された中間ドライバー [ **\_フラッシュ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)および[**irp\_MJ\_シャットダウン**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)要求も*DispatchShutdown*と*DispatchFlushBuffers*を提供します。ルーチン.

 

 




