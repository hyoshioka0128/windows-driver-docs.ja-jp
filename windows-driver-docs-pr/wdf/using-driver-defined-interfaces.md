---
title: ドライバー定義インターフェイスの使用
description: ドライバー定義インターフェイスの使用
ms.assetid: ad96add6-c982-429b-b815-d7adf6fed8cc
keywords:
- ドライバーで定義されたインターフェイス (WDK KMDF)
- インターフェイス WDK KMDF
- 一方向通信の WDK KMDF
- 双方向通信 (WDK KMDF)
- 参照カウント WDK KMDF
- 参照関数 WDK KMDF
- 逆参照関数 WDK KMDF
- 非 op 関数 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9190e97daec40de161a8c3a3efe35b89b3175bdf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843083"
---
# <a name="using-driver-defined-interfaces"></a>ドライバー定義インターフェイスの使用


ドライバーは、他のドライバーがアクセスできるデバイス固有のインターフェイスを定義できます。 これらの*ドライバー定義のインターフェイス*は、一連の呼び出し可能ルーチン、一連のデータ構造、またはその両方で構成されます。 ドライバーは、通常、ドライバー定義のインターフェイス構造内のこれらのルーチンと構造体へのポインターを提供します。このインターフェイスは、ドライバーによって他のドライバーが使用できるようにします。

たとえば、バスドライバーは、子デバイスに関する情報が子デバイスのリソースリストで利用できない場合に、上位レベルのドライバーがを呼び出して子デバイスに関する情報を取得することができる1つ以上のルーチンを提供する場合があります。

WDK に記載されているドライバー定義の一連のインターフェイスの例については、「 [USB ルーチン](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85))」を参照してください。 また、[トースター](sample-kmdf-drivers.md)サンプルのフレームワークベースバージョンを参照してください。

### <a name="creating-an-interface"></a>インターフェイスの作成

ドライバー定義の各インターフェイスは、次の方法で指定します。

-   GUID

-   バージョン番号

-   ドライバー定義のインターフェイス構造体

-   参照ルーチンと逆参照ルーチン

インターフェイスを作成し、他のドライバーで使用できるようにするには、フレームワークベースのドライバーで次の手順を実行します。

1.  インターフェイス構造を定義します。

    このドライバー定義構造体の最初のメンバーは、[**インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)ヘッダー構造体である必要があります。 追加のメンバーには、インターフェイスデータと、別ドライバーが呼び出すことができる追加の構造体またはルーチンへのポインターが含まれる場合があります。

    ドライバーは、定義されているインターフェイスを説明する[**WDF\_クエリ\_インターフェイス\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfqueryinterface/ns-wdfqueryinterface-_wdf_query_interface_config)構造体を提供する必要があります。

2.  [**Wdfdeviceaddqueryinterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceaddqueryinterface)を呼び出します。

    [**Wdfdeviceaddqueryinterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceaddqueryinterface)メソッドは、次のことを行います。

    -   は、インターフェイスに関する情報 (GUID、バージョン番号、構造体のサイズなど) を格納するため、フレームワークはインターフェイスに対する別のドライバーの要求を認識できます。
    -   別のドライバーがインターフェイスを要求したときにフレームワークが呼び出す、省略可能な[*EvtDeviceProcessQueryInterfaceRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request)イベントコールバック関数を登録します。

ドライバー定義のインターフェイスの各インスタンスは個々のデバイスに関連付けられているため、ドライバーは通常、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)または[*EvtChildListCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device) Callback 関数内から[**wdfdeviceaddqueryinterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceaddqueryinterface)を呼び出します。

### <a name="accessing-an-interface"></a>インターフェイスへのアクセス

ドライバーでインターフェイスが定義されている場合、別のフレームワークベースのドライバーは、 [**Wdffdoqueryforinterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoqueryforinterface)を呼び出し、GUID、バージョン番号、構造体へのポインター、および構造体のサイズを渡すことによって、インターフェイスへのアクセスを要求できます。 このフレームワークは、i/o 要求を作成し、ドライバースタックの一番上に送信します。

通常、ドライバーは[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数内から[**Wdffdoqueryforinterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoqueryforinterface)を呼び出します。 または、デバイスが動作状態でないときにドライバーがインターフェイスを解放する必要がある場合、ドライバーは[*Evtdeviceのハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数内から**Wdffdoqueryforinterface**を呼び出し、インターフェイスの逆参照を呼び出すことができます。[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)コールバック関数内からのルーチン。

ドライバー b によって定義されているインターフェイスについてドライバー B に要求がある場合、このフレームワークはドライバー b の要求を処理します。フレームワークは、GUID とバージョンがサポートされているインターフェイスを表しているかどうか、およびそのドライバーが指定した構造体のサイズがインターフェイスを保持するのに十分な大きさであることを確認します。

ドライバーが[**Wdffdoqueryforinterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoqueryforinterface)を呼び出すと、フレームワークによって作成された i/o 要求が、ドライバースタックの一番下まで移動します。 単純なドライバースタックが3つのドライバー (A、B、C) で構成されていて、ドライバー A がインターフェイスを要求した場合、ドライバー B とドライバー C の両方がインターフェイスをサポートできます。 たとえば、ドライバー B は、要求をドライバー C に渡す前にドライバー A のインターフェイス構造を設定することがあります。ドライバー C は、インターフェイス構造の内容を検査する[*EvtDeviceProcessQueryInterfaceRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request)コールバック関数を提供できます。変更する可能性があります。

ドライバー A がドライバー B のインターフェイスにアクセスする必要があり、ドライバー B がリモート i/o ターゲット (つまり、別のドライバースタック内のドライバー) である場合、ドライバー A は[**Wdffdoqueryforinterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoqueryforinterface)ではなく[**Wdfiotargetqueryforinterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetqueryforinterface)を呼び出す必要があります。

### <a name="using-one-way-or-two-way-communication"></a>一方向または双方向の通信を使用する

一方向の通信を提供するインターフェイス、または双方向の通信を提供するインターフェイスを定義できます。 双方向の通信を指定するために、ドライバーは、 [**WDF\_QUERY\_INTERFACE\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfqueryinterface/ns-wdfqueryinterface-_wdf_query_interface_config)構造体の**Importinterface**メンバーを**TRUE**に設定します。

インターフェイスが一方向の通信を提供し、ドライバー A がドライバー B のインターフェイスを要求した場合、インターフェイスデータはドライバー B からドライバー A にのみ流れます。フレームワークは、一方向の通信をサポートするインターフェイスに対してドライバー A の要求を受け取ると、ドライバー定義のインターフェイス値をドライバー A のインターフェイス構造にコピーします。 次に、ドライバー B の[*EvtDeviceProcessQueryInterfaceRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request) callback 関数 (存在する場合) を呼び出します。これにより、インターフェイスの値を確認し、変更する可能性があります。

インターフェイスが双方向の通信を提供する場合、インターフェイス構造には、ドライバー B に要求を送信する前にドライバーが入力するいくつかのメンバーが含まれます。ドライバー B は、そのドライバーが提供したパラメーター値を読み取り、それらの値に基づいて選択を行うことができます。ドライバー A に提供する情報。フレームワークは、双方向の通信をサポートするインターフェイスに対してドライバー A の要求を受け取ると、受け取った値を調べて出力を指定できるように、ドライバー B の[*EvtDeviceProcessQueryInterfaceRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request) callback 関数を呼び出します。値. 双方向の通信では、フレームワークがインターフェイスの値をドライバー A のインターフェイス構造にコピーしないため、コールバック関数が必要です。

### <a name="maintaining-a-reference-count"></a>参照カウントの保持

各インターフェイスには、参照関数と、インターフェイスの参照カウントをインクリメントおよびデクリメントする逆参照関数が含まれている必要があります。 インターフェイスを定義するドライバーは、[**インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)構造内のこれらの関数のアドレスを指定します。

ドライバー A がインターフェイスに対してドライバー B に要求すると、インターフェイスをドライバー A が使用できるようにする前に、フレームワークはインターフェイスの参照関数を呼び出します。ドライバー A がインターフェイスの使用を終了すると、インターフェイスの逆参照関数を呼び出す必要があります。

ほとんどのインターフェイスの参照関数と逆参照関数は、何も行わない操作なしの関数にすることができます。 フレームワークには、ほとんどのドライバーで使用できる[**WdfDeviceInterfaceReferenceNoOp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceinterfacereferencenoop)および[**WdfDeviceInterfaceDereferenceNoOp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceinterfacedereferencenoop)という非 op 参照カウント関数が用意されています。

ドライバーがインターフェイスの参照カウントを追跡し、実際の参照関数と逆参照関数を提供する必要があるのは、ドライバー A がリモート i/o ターゲット (つまり、別のドライバースタックにあるドライバー) からのインターフェイスを要求する場合のみです。 この場合、ドライバー A がドライバー B のインターフェイスを使用している間にデバイスが削除されないようにするには、別のスタック内のドライバー B が参照カウントを実装する必要があります。

インターフェイスを定義するドライバー B を設計する場合は、別のドライバースタックからドライバーのインターフェイスにアクセスするかどうかを決定する必要があります。 (ドライバー B は、インターフェイスの要求がローカルドライバースタックまたはリモートスタックからのものであるかどうかを判断できません)。ドライバーがリモートスタックからのインターフェイス要求をサポートする場合、ドライバーは参照カウントを実装する必要があります。

ドライバー A を設計する場合は、リモート i/o ターゲットのインターフェイスにアクセスするには、ドライバー B のデバイスが削除されるときにインターフェイスを解放する[*Evtiotargetqueryremove*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_query_remove)コールバック関数、ドライバー b のデバイスが突然削除されたときにインターフェイスを解放する[*EvtIoTargetRemoveComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_complete)コールバック関数、およびデバイスを削除しようとしたときにインターフェイスを再取得する[*EvtIoTargetRemoveCanceled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_canceled)コールバック関数が必要です。

 

 





