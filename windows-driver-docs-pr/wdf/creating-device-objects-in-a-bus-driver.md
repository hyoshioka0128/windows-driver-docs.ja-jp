---
title: バス ドライバーでのデバイス オブジェクトの作成
description: バス ドライバーでのデバイス オブジェクトの作成
ms.assetid: 36b4d24c-9f5e-4853-bf70-c94613e01f2b
keywords:
- PnP WDK KMDF、バス ドライバー
- プラグ アンド プレイ WDK KMDF、バス ドライバー
- 電源管理 WDK KMDF、バス ドライバー
- バス ドライバー WDK KMDF
- 物理デバイス オブジェクト WDK KMDF
- Pdo WDK KMDF
- バスの WDK KMDF 列挙型
- WDK KMDF 列挙型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: beac4c1379a62a6c8ec70443bc38217ef4b30b02
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382377"
---
# <a name="creating-device-objects-in-a-bus-driver"></a>バス ドライバーでのデバイス オブジェクトの作成


各[バス ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/bus-drivers)子デバイスが、親デバイスに接続されていることを検出したときに、framework デバイス オブジェクトを作成する必要があります。 親デバイスは通常、バスですが、各関数が、別の一連の (デジタル オーディオおよび MIDI をサポートしているサウンド カード) などのドライバーが必要です、多機能デバイスにもできます。 別の 1 つのハードウェア (子) の実際の接続をそれぞれ表すために、バス ドライバーを作成するデバイス オブジェクトが物理デバイス オブジェクト (Pdo) と呼ばれます (親)。

識別して、バスに接続されているデバイスをレポート作成のプロセスが呼び出されます*列挙体のバス*します。

-   バス ドライバーを実行する場合[動的 bus 列挙](dynamic-enumeration.md)その[ *EvtChildListCreateDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device)コールバック関数を識別するハンドルを受け取る、 [ **WDFDEVICE\_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体。

-   バス ドライバーを実行する場合[静的 bus 列挙](static-enumeration.md)、呼び出す必要があります[ **WdfPdoInitAllocate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallocate) 、WDFDEVICE を識別するハンドルを取得する\_INIT 構造体。

バスの列挙体の詳細については、次を参照してください。[バス上のデバイスを列挙する](enumerating-the-devices-on-a-bus.md)します。

バス ドライバーのセットを呼び出すことができます[framework デバイス オブジェクトの初期化メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/#device-init-methods)、情報を格納する、 [ **WDFDEVICE\_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体。 さらに、バス ドライバーが呼び出せる[framework PDO 初期化メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/#pdo-init-methods)します。

通常、デバイスの列挙子 framework デバイス オブジェクトを作成するには、次の手順が含まれています。

-   バス ドライバー固有のコールバック関数を登録しています。

    バス ドライバーの呼び出しのほとんど[ **WdfPdoInitSetEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitseteventcallbacks)デバイスで必要なシステムのハードウェア リソースを指定する必要があります。 ハードウェア リソースを指定する方法については、次を参照してください。 [Framework ベースのドライバーのハードウェア リソース](hardware-resources-for-kmdf-drivers.md)します。 デバイスとドライバーの取り出しをサポートする場合、追加のコールバック関数を登録できます。

-   Reporting[識別文字列](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)します。

    バス ドライバーは、呼び出すことによって、デバイスの識別文字列をレポートする必要があります[ **WdfPdoInitAssignDeviceID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitassigndeviceid)、 [ **WdfPdoInitAssignInstanceID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitassigninstanceid)、 [ **WdfPdoInitAddCompatibleID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitaddcompatibleid)、および[ **WdfPdoInitAddHardwareID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitaddhardwareid)各タイプの文字列にします。デバイスをサポートします。 さらに、バージョン 1.9 以降のフレームワークを使用するバス ドライバーが呼び出せる[ **WdfPdoInitAssignContainerID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitassigncontainerid)します。

-   Raw モードで、バス ドライバーがデバイスをサポートできるかどうかを報告します。

    呼び出す必要がありますが、バス ドライバーでは、デバイスの raw モードをサポートする場合[ **WdfPdoInitAssignRawDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)します。

-   デバイスを表す表示可能なテキストを提供します。

    バス ドライバー呼び出し[ **WdfPdoInitAddDeviceText** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitadddevicetext)と[ **WdfPdoInitSetDefaultLocale** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitsetdefaultlocale)にデバイスを説明するテキストを提供するには複数の言語でのユーザー。

-   デバイス オブジェクトを作成します。

    デバイス オブジェクトを作成する最後の手順を呼び出すことです。 [ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)します。

ドライバー、WDFDEVICE の初期化中にエラーが発生した場合\_から取得した INIT 構造[ **WdfPdoInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)、ドライバーを呼び出す必要があります[ **WdfDeviceInitFree** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)の代わりに[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)します。

通常、呼び出す、バス ドライバーには、デバイス オブジェクトが作成、 [ **WdfDeviceSetPnpCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetpnpcapabilities)と[ **WdfDeviceSetPowerCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetpowercapabilities)デバイスのプラグ アンド プレイと電源機能レポートします。

各バス ドライバーは、関数のドライバー、バス アダプターもです。 そのため、ドライバーが提供する必要がありますも、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数。 このコールバック関数では、システム上の各バス アダプターの機能のデバイス オブジェクト (FDO) を作成します。 Fdo の作成の詳細については、次を参照してください。 [Function ドライバーのデバイス オブジェクトの作成](creating-device-objects-in-a-function-driver.md)です。

 

 





