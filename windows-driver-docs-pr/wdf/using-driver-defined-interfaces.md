---
title: ドライバー定義インターフェイスの使用
description: ドライバー定義インターフェイスの使用
ms.assetid: ad96add6-c982-429b-b815-d7adf6fed8cc
keywords:
- WDK KMDF ドライバー定義インターフェイス
- WDK KMDF インターフェイス
- WDK KMDF の一方向の通信
- WDK KMDF の双方向通信
- 参照カウントの WDK KMDF
- WDK KMDF 関数を参照します。
- WDK KMDF の関数を逆参照します。
- no-op 関数 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57fafacf2bc9c7f782392f294a11923d25396f05
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372264"
---
# <a name="using-driver-defined-interfaces"></a>ドライバー定義インターフェイスの使用


ドライバーは、他のドライバーにアクセスできるデバイスに固有のインターフェイスを定義できます。 これら*ドライバー定義インターフェイス*呼び出し可能なルーチンのセット、一連のデータ構造体、またはその両方で構成できます。 ドライバーは、通常、これらのルーチンと、ドライバーは、他のドライバーを使用できるようにドライバー定義インターフェイス構造体の構造体へのポインターを提供します。

たとえば、バス ドライバーは、その情報が、子デバイスのリソースの一覧で使用できない場合、子デバイスに関する情報を取得するより高度なドライバーが呼び出すことができる 1 つまたは複数のルーチンを提供する可能性があります。

WDK で説明されているドライバーの定義済みのインターフェイスのセットの例は、次を参照してください。 [USB ルーチン](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85))します。 また、framework ベースのバージョンを参照してください、[トースター](sample-kmdf-drivers.md)サンプル。

### <a name="creating-an-interface"></a>インターフェイスの作成

各ドライバーの定義済みのインターフェイスは、によって指定されます。

-   GUID

-   バージョン番号

-   ドライバー定義インターフェイス構造体

-   参照し、ルーチンを逆参照

インターフェイスを作成し、その他のドライバーを使用できるように、framework ベースのドライバーは、次の手順を使用できます。

1.  インターフェイスの構造体を定義します。

    このドライバー定義の構造体の最初のメンバーである必要があります、 [**インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_interface)ヘッダー構造体。 ポインターのインターフェイスのデータとその他のメンバーが含まれます追加の構造やルーチンに、その別のドライバーを呼び出すことができます。

    ドライバーを提供する必要があります、 [ **WDF\_クエリ\_インターフェイス\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/ns-wdfqueryinterface-_wdf_query_interface_config)構造体は、定義したインターフェイスについて説明します。

2.  呼び出す[ **WdfDeviceAddQueryInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceaddqueryinterface)します。

    [ **WdfDeviceAddQueryInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceaddqueryinterface)メソッドは、次を実行します。

    -   フレームワークは、インターフェイスの別のドライバーの要求を認識できるように、GUID、バージョン番号、構造体のサイズなどのインターフェイスに関する情報を格納します。
    -   省略可能な登録[ *EvtDeviceProcessQueryInterfaceRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request)フレームワーク インターフェイスの別のドライバーが表示されたら、イベント コールバック関数。

通常のドライバーを呼び出すように、ドライバーの定義済みのインターフェイスの各インスタンスは、個々 のデバイスに関連付けられて[ **WdfDeviceAddQueryInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceaddqueryinterface)内から、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)または[ *EvtChildListCreateDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device)コールバック関数。

### <a name="accessing-an-interface"></a>インターフェイスへのアクセス

別のフレームワーク ベースのドライバーが呼び出すことによってインターフェイスへのアクセスを要求には、ドライバーは、インターフェイスを定義した場合[ **WdfFdoQueryForInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoqueryforinterface) GUID、バージョン番号へのポインターを渡すと、構造、および構造体のサイズ。 フレームワークは、I/O 要求を作成し、ドライバー スタックの一番上に送信します。

通常、ドライバーを呼び出します[ **WdfFdoQueryForInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoqueryforinterface)内から、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数。 または、ドライバーは、デバイスでの稼働状態でないときに、インターフェイスを解放する必要がある場合、ドライバー呼び出せる**WdfFdoQueryForInterface**内から、 [ *EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数とインターフェイスのルーチン内からの逆参照呼び出し、 [ *EvtDeviceReleaseHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)コールバック関数。

フレームワークがドライバー B. の要求を処理する場合、ドライバー、ドライバー B をインターフェイスに要求すると、B が定義されているドライバーをフレームワークでは、GUID とバージョン、サポートされているインターフェイスを表すし、構造がそのドライバーをサイズを指定したが、インターフェイスを保持するために十分な大きさのことを検証します。

ドライバーを呼び出すと[ **WdfFdoQueryForInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoqueryforinterface)、ドライバー スタックの一番下に、フレームワークを作成する I/O 要求が送信されます。 A、B、および C の-3 つのドライバーの単純なドライバー スタックが構成されている場合、およびドライバー A インターフェイスを要求する場合は、ドライバー B と C のドライバーの両方を使うことにより、インターフェイスをサポートすることができます。 たとえば、ドライバー B がいっぱいに A のドライバー インターフェイス構造体で提供 C ドライバーをドライバーに要求を渡す前に、 [ *EvtDeviceProcessQueryInterfaceRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request)コールバック関数インターフェイス構造体の内容を調べ、場合によって変更します。

ドライバー A が B のドライバーのインターフェイスにアクセスする必要があります、B のドライバーがリモートの I/O ターゲット (別のドライバー スタック内にあるドライバー) と、ドライバー A を呼び出す必要があります[ **WdfIoTargetQueryForInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetqueryforinterface)の代わりに[ **WdfFdoQueryForInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoqueryforinterface)します。

### <a name="using-one-way-or-two-way-communication"></a>一方向または双方向通信を使用します。

一方向の通信または双方向通信を提供する 1 つを提供するインターフェイスを定義することができます。 双方向の通信は、ドライバーのセットを指定する、 **ImportInterface**のメンバー、 [ **WDF\_クエリ\_インターフェイス\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/ns-wdfqueryinterface-_wdf_query_interface_config)構造体を**TRUE**します。

A. ドライバーをドライバー B からのみインターフェイスのデータが流れるインターフェイスは、一方向の通信を提供し、ドライバー、ドライバー B のインターフェイスを要求する場合は、フレームワークでは、一方向の通信をサポートするインターフェイスのドライバーの要求を受信したときに、フレームワークは A のドライバー インターフェイス構造体にインターフェイスのドライバーの定義済みの値をコピーします。 ドライバーの B を呼び出して[ *EvtDeviceProcessQueryInterfaceRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request)を確認し、インターフェイスの値を変更するために、存在する場合、コールバック関数。

インターフェイスは、双方向通信を提供する場合、インターフェイス構造に含まれる一部のメンバー B ドライバーをドライバーに要求パラメーターの値読み取ることができます、そのドライバーを送信する前に、入力が提供され、についてこれらの値に基づく選択を行うドライバーA. ドライバーに提供する情報フレームワークは、双方向通信をサポートするインターフェイスのドライバーの要求を受信したときにフレームワークのドライバー B の[ *EvtDeviceProcessQueryInterfaceRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request)コールバック関数、値と出力値を指定で受信したを調べることができます。 双方向の通信フレームワークでは、任意のインターフェイスの値 A のドライバー インターフェイス構造体にコピーされないため、コールバック関数が必要です。

### <a name="maintaining-a-reference-count"></a>参照カウントを維持

Reference 関数と逆参照関数の場合、インクリメントおよびデクリメント インターフェイスの参照カウントが、各インターフェイスを含める必要があります。 インターフェイスを定義するドライバーがこれらの関数のアドレスを指定します、 [**インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_interface)構造体。

フレームワークがドライバー A. にインターフェイスを使用できるようにする前に、インターフェイスの参照関数を呼び出すドライバー A では、インターフェイスの B のドライバーが表示されたら、インターフェイスを呼び出す必要があります、ドライバーは、インターフェイスを使用してが完了したら、関数の逆参照します。

参照と関数を逆参照のほとんどのインターフェイスは、何もしないは no-op 関数を指定できます。 フレームワークが、何も参照カウントの機能を提供[ **WdfDeviceInterfaceReferenceNoOp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceinterfacereferencenoop)と[ **WdfDeviceInterfaceDereferenceNoOp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceinterfacedereferencenoop)、ほとんどのドライバーが使用できます。

きのみのドライバーを保持する必要がありますインターフェイスの参照カウントの追跡し実際の参照を提供し、関数の逆参照、ドライバー A は、リモートの I/O ターゲット (別のドライバー スタック内にあるドライバー) のインターフェイスを要求するときは、します。 ここでは、ドライバー B (別のスタック) では参照カウントを実装する必要がありますできなくなることがそのデバイス ドライバー A が B のドライバー インターフェイスを使用するときに削除されないようにします。

B で、インターフェイスを定義するには、ドライバーを設計する場合は、ドライバーのインターフェイスが別のドライバー スタックからアクセスされるかどうかを決定する必要があります。 (ドライバー B 特定できないかどうかそのインターフェイスの要求は、ローカル ドライバー スタックから、またはリモートのスタックから。)ドライバーでは、リモートのスタックからインターフェイスの要求をサポートする、ドライバーは参照カウントを実装する必要があります。

ドライバー A は、アクセスすると、リモートの I/O ターゲットで、インターフェイス、設計する場合、ドライバーを提供する必要があります、 [ *EvtIoTargetQueryRemove* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_query_remove)インターフェイスを解放するコールバック関数と B のドライバーデバイスが削除される直前には、 [ *EvtIoTargetRemoveComplete* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_complete)ドライバー B のデバイスが突然削除されたときに、インターフェイスを解放するコールバック関数[ *EvtIoTargetRemoveCanceled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_canceled)デバイスを削除する試行が取り消された場合に、インターフェイスを再取得するコールバック関数。

 

 





