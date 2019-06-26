---
title: 機能ドライバーでのデバイス オブジェクトの作成
description: 機能ドライバーでのデバイス オブジェクトの作成
ms.assetid: 3b988f6d-c50e-412d-85cb-031746535ff4
keywords:
- PnP WDK KMDF、関数のドライバー
- プラグ アンド プレイ WDK KMDF、関数のドライバー
- 電源管理 WDK KMDF、関数のドライバー
- 機能ドライバー WDK KMDF
- WDK KMDF の機能のデバイス オブジェクト
- Fdo WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54fe53b4b7978960eceb15c5071651a8b92f0821
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382381"
---
# <a name="creating-device-objects-in-a-function-driver"></a>機能ドライバーでのデバイス オブジェクトの作成


各[関数ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/function-drivers)システム上に存在する、サポートされているデバイスの各フレームワーク デバイス オブジェクトを作成します。 関数のドライバーによっては、これらのデバイス オブジェクトが作成された、ため、機能のデバイス オブジェクト (Fdo) は呼び出されます。 各 FDO は function ドライバーのデバイスを表したものです。

関数ドライバー フレームワークのデバイス オブジェクトを作成する必要がありますたびに、フレームワーク、ドライバーの[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数。 フレームワークは、システムでサポートされているデバイスのいずれかが存在するドライバーに通知するには、このコールバック関数を呼び出します。

ドライバーの[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数へのポインターを受け取る、 [ **WDFDEVICE\_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体。 ドライバーのセットを呼び出すことができます[framework デバイス オブジェクトの初期化メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/#device-init-methods)、WDFDEVICE で情報を格納する\_INIT 構造体。 さらに、ドライバーの関数を呼び出すことができます[framework FDO 初期化メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/#fdo-init-methods)します。

Function ドライバー framework デバイス オブジェクトを作成すると、通常は、次の手順が含まれています。

-   PnP、パワー、および電源ポリシーのコールバック関数を登録しています。

    ほとんどの関数のドライバー呼び出し[ **WdfDeviceInitSetPnpPowerEventCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks) PnP と電力のコールバック関数を登録します。 これらのコールバック関数の詳細については、次を参照してください。 [PnP をサポートしていると関数のドライバーでの電源管理](supporting-pnp-and-power-management-in-function-drivers.md)します。

    デバイスは、低電力アイドル状態をサポートしていますまたは、ウェイク アップ機能を備えて、場合、関数のドライバーもは[ **WdfDeviceInitSetPowerPolicyEventCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)電源ポリシーのコールバックを登録するには。関数。 これらのコールバック関数の詳細については、次を参照してください。[電源ポリシー所有権](power-policy-ownership.md)します。

-   ドライバー固有のコールバック関数の関数を登録しています。

    一部の関数のドライバー呼び出し[ **WdfFdoInitSetEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitseteventcallbacks)場合、それらのデバイスで必要なシステムのハードウェア リソースを指定するときに参加する必要があります。 ハードウェア リソースの詳細については、次を参照してください。 [Framework ベースのドライバーのハードウェア リソース](hardware-resources-for-kmdf-drivers.md)します。

-   ファイルのイベントのコールバック関数を登録しています。

    ドライバーを呼び出す必要があります、ドライバーは、アプリケーションを開くか、デバイス上のファイルを閉じたときに応答する必要がある場合、 [ **WdfDeviceInitSetFileObjectConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig) framework ファイル オブジェクトのコールバック関数を登録するには. 詳細については、次を参照してください。 [Framework ファイル オブジェクトを使用する](framework-file-objects.md)します。

-   I/O 要求の属性を設定します。

    ドライバーを呼び出すことができる場合、ドライバーはフレームワークのキュー オブジェクトからの I/O 要求を受信、 [ **WdfDeviceInitSetRequestAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)フレームワークがデバイスを割り当てることのコンテキストのメモリを設定するには要求オブジェクト。 詳細については、次を参照してください。[要求オブジェクトのコンテキストを使用して](using-request-object-context.md)します。

-   デバイスの特性を設定します。

    通常、関数ドライバーは、一部のデバイスの特性を指定する次のメソッドを呼び出します。

    -   [**WdfDeviceInitSetDeviceType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdevicetype)ドライバーがサポートするハードウェアの種類を識別します。
    -   [**WdfDeviceInitSetIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype)をドライバーがアプリケーションからの I/O 要求を処理する場合は、データのバッファーにアクセスするためのメソッドを識別します。
    -   [**WdfDeviceInitSetCharacteristics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetcharacteristics)デバイスは読み取り専用またはリムーバブル メディアをサポートしているかどうかなど、デバイスの特性を設定します。
    -   [**WdfDeviceInitSetExclusive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetexclusive)デバイスは、一度に 1 つのアプリケーションでの排他アクセスを必要とする場合、します。
    -   [**WdfDeviceInitSetPowerInrush**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerinrush)低電力状態からの作業 (D0) 状態に遷移するとき、デバイスに、突入電流が必要な場合、します。
    -   [**WdfDeviceInitSetPowerPageable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable)または[ **WdfDeviceInitSetPowerNotPageable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowernotpageable)システムは、ドライバーはページング可能なデータにアクセスする必要があるかどうかを示すために、スリープ状態と動作 (S0) 状態の遷移中です。
    -   [**WdfDeviceInitAssignName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)デバイス オブジェクトに名前を割り当てます。
    -   [**WdfDeviceInitAssignSDDLString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring)セキュリティ記述子をデバイス オブジェクトに割り当てます。
    -   [**WdfDeviceInitSetDeviceClass**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdeviceclass)デバイスのセットアップ クラスを識別します。
-   デバイスのプロパティを取得します。

    場合があります関数ドライバーでは、デバイスのバスのドライバーやその他の下位のドライバーが設定されているデバイスのプロパティに関する情報を取得する必要があります。 ドライバーを呼び出すことができます[ **WdfFdoInitQueryProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitqueryproperty)または[ **WdfFdoInitAllocAndQueryProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitallocandqueryproperty)この情報を取得します。 Windows 8.1 以降を対象とする新しいドライバーが呼び出せる[ **WdfFdoInitQueryPropertyEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitquerypropertyex)と[ **WdfFdoInitAllocAndQueryPropertyEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitallocandquerypropertyex).

-   デバイスのレジストリ キーへのアクセス。

    関数のドライバーによっては、デバイスまたは別のドライバー、ユーザー、またはインストール パッケージが配置されている場合、レジストリのドライバーに関する情報を取得する必要があります。 ドライバーが呼び出せる[ **WdfFdoInitOpenRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey)デバイスまたはドライバーのレジストリ キーを開きます。 詳細については、次を参照してください。 [Framework ベースのドライバーのレジストリを使用して](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-registry-in-wdf-drivers)します。

-   動的な列挙を使用する既定の子リスト構成を作成します。

    かどうか、バスの機能のドライバーを記述して、ドライバーは、バスに接続されている子デバイスの動的な列挙を実行している場合、ドライバーを呼び出す必要があります[ **WdfFdoInitSetDefaultChildListConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitsetdefaultchildlistconfig). 詳細については、次を参照してください。[バス上のデバイスを列挙する](enumerating-the-devices-on-a-bus.md)します。

-   デバイス オブジェクトを作成します。

    デバイス オブジェクトを作成する最後の手順を呼び出すことです。 [ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)します。

 

 





