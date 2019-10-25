---
title: 機能ドライバーでのデバイス オブジェクトの作成
description: 機能ドライバーでのデバイス オブジェクトの作成
ms.assetid: 3b988f6d-c50e-412d-85cb-031746535ff4
keywords:
- PnP WDK KMDF, 関数ドライバー
- プラグアンドプレイ WDK KMDF, 関数ドライバー
- 電源管理 WDK KMDF, 関数ドライバー
- 関数ドライバー WDK KMDF
- 機能デバイスオブジェクト WDK KMDF
- FDOs WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee33a46d0b72d5b675ceda3b86d0b2c3051e3190
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844681"
---
# <a name="creating-device-objects-in-a-function-driver"></a>機能ドライバーでのデバイス オブジェクトの作成


各[関数ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/function-drivers)は、システムに存在する、サポートされている各デバイスのフレームワークデバイスオブジェクトを作成します。 これらのデバイスオブジェクトは関数ドライバーによって作成されるため、機能デバイスオブジェクト (FDOs) と呼ばれます。 各 FDO は、デバイスの関数ドライバーの表現です。

関数ドライバーは、フレームワークがドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数を呼び出すたびに、フレームワークデバイスオブジェクトを作成する必要があります。 フレームワークは、このコールバック関数を呼び出して、サポートされているデバイスの1つがシステムに存在することをドライバーに通知します。

ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数は、 [**wdfdevice\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体へのポインターを受け取ります。 ドライバーは、一連の[フレームワークデバイスオブジェクトの初期化メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/#device-init-methods)を呼び出すことができます。このメソッドは、wdfdevice\_INIT 構造体に情報を格納します。 さらに、関数ドライバーは、[フレームワーク FDO の初期化メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/#fdo-init-methods)を呼び出すことができます。

通常、関数ドライバーでフレームワークデバイスオブジェクトを作成するには、次の手順を実行します。

-   PnP、電源、および電源ポリシーのコールバック関数を登録しています。

    ほとんどの関数ドライバーは[**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)を呼び出して、PnP および電源コールバック関数を登録します。 これらのコールバック関数の詳細については、「[関数ドライバーでの PnP と電源管理のサポート](supporting-pnp-and-power-management-in-function-drivers.md)」を参照してください。

    デバイスで低電力アイドルがサポートされている場合、またはウェイクアップ機能がある場合、関数ドライバーは通常、 [**Wdfdeviceinitsetpowerpolicyeventcallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)も呼び出して、電源ポリシーコールバック関数を登録します。 これらのコールバック関数の詳細については、「[電源ポリシーの所有権](power-policy-ownership.md)」を参照してください。

-   関数ドライバー固有のコールバック関数を登録しています。

    一部の関数ドライバーは、デバイスが必要とするシステムハードウェアリソースの指定に参加する必要がある場合に、 [**Wdffdoinitseteventcallbacks バック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitseteventcallbacks)を呼び出します。 ハードウェアリソースの詳細については、「[フレームワークベースのドライバーのハードウェアリソース](hardware-resources-for-kmdf-drivers.md)」を参照してください。

-   ファイルイベントのコールバック関数を登録しています。

    アプリケーションがデバイス上のファイルを開いたり閉じたりしたときにドライバーが応答する必要がある場合、ドライバーは[**Wdfdeviceinitsetfileobjectconfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig)を呼び出して、フレームワークファイルオブジェクトのコールバック関数を登録する必要があります。 詳細については、「 [Framework ファイルオブジェクトの使用](framework-file-objects.md)」を参照してください。

-   I/o 要求の属性を設定しています。

    ドライバーがフレームワークキューオブジェクトから i/o 要求を受信する場合、ドライバーは[**Wdfdeviceinitsetrequestattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)を呼び出して、フレームワークがデバイスの要求オブジェクトに割り当てるコンテキストメモリを設定できます。 詳細については、「[要求オブジェクトコンテキストの使用](using-request-object-context.md)」を参照してください。

-   デバイスの特性を設定します。

    通常、関数ドライバーは、デバイスの特性を指定するために、次のメソッドの一部を呼び出します。

    -   [**WdfDeviceInitSetDeviceType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdevicetype)。ドライバーがサポートするハードウェアの種類を識別します。
    -   [**Wdfdeviceinitsetiotype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype)。ドライバーがアプリケーションからの i/o 要求を処理する場合に、データバッファーにアクセスするためのメソッドを識別します。
    -   [**Wdfdeviceinitsetcharacteristics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetcharacteristics)。デバイスが読み取り専用であるか、リムーバブルメディアをサポートしているかなど、デバイスの特性を設定します。
    -   [**Wdfdeviceinitsetexclusive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetexclusive)。デバイスが一度に1つのアプリケーションによる排他アクセスを必要とする場合。
    -   デバイスが低電力状態から動作中 (D0) 状態に遷移するときに、現在の突入電流が必要な場合は[**WdfDeviceInitSetPowerInrush**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerinrush)。
    -   [**Wdfdeviceinitsetpowerpageable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable)または[**Wdfdeviceinitsetpowernotページング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowernotpageable)。システムがスリープ状態と動作中 (S0) 状態の間で遷移しているときに、ドライバーがページング可能なデータにアクセスする必要があるかどうかを指定します。
    -   [**Wdfdeviceinitassign name**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)。デバイスオブジェクトに名前を割り当てます。
    -   [**Wdfdeviceinitassign Sddlstring**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring)。これにより、デバイスオブジェクトにセキュリティ記述子が割り当てられます。
    -   [**Wdfdeviceinitsetdeviceclass**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdeviceclass)。デバイスのセットアップクラスを識別します。
-   デバイスのプロパティを取得しています。

    場合によっては、デバイスのバスのドライバーまたはその他の下位のドライバーによって設定されたデバイスのプロパティに関する情報を取得する必要があります。 ドライバーは、この情報を取得するために、 [**wdffdoinitqueryproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitqueryproperty)または[**Wdffdoinitallocandqueryproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitallocandqueryproperty)を呼び出すことができます。 Windows 8.1 以降をターゲットとする新しいドライバーでは、 [**Wdffdoinitquerypropertyex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitquerypropertyex)と[**Wdffdoinitallocandquerypropertyex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitallocandquerypropertyex)を呼び出すことができます。

-   デバイスのレジストリキーにアクセスしています。

    一部の関数ドライバーでは、別のドライバー、ユーザー、またはインストールパッケージがレジストリに配置したデバイスまたはドライバーに関する情報を取得する必要があります。 ドライバーは、 [**Wdffdoinitopenregistrykey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey)を呼び出して、デバイスまたはドライバーのレジストリキーを開くことができます。 詳細については、「[フレームワークベースのドライバーでのレジストリの使用](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-registry-in-wdf-drivers)」を参照してください。

-   動的列挙に使用する既定の子リスト構成を作成しています。

    バス用の関数ドライバーを作成していて、バスに接続されている子デバイスの動的な列挙をドライバーが実行する場合、ドライバーは[**Wdffdoinitsetdefaultchildlistconfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetdefaultchildlistconfig)を呼び出す必要があります。 詳細については、「[バス上のデバイスの列挙](enumerating-the-devices-on-a-bus.md)」を参照してください。

-   デバイスオブジェクトを作成しています。

    デバイスオブジェクトを作成する最後の手順は、 [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出すことです。

 

 





