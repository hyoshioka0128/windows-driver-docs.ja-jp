---
title: バス ドライバーでのデバイス オブジェクトの作成
description: バス ドライバーでのデバイス オブジェクトの作成
ms.assetid: 36b4d24c-9f5e-4853-bf70-c94613e01f2b
keywords:
- PnP WDK KMDF、バスドライバー
- WDK KMDF、バスドライバープラグアンドプレイ
- 電源管理 WDK KMDF、バスドライバー
- バスドライバー WDK KMDF
- 物理デバイスオブジェクト WDK KMDF
- PDOs WDK KMDF
- バス列挙型 WDK KMDF
- 列挙型 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 355d82a89777e60e11d392b6b0f6bef62251cffb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844687"
---
# <a name="creating-device-objects-in-a-bus-driver"></a>バス ドライバーでのデバイス オブジェクトの作成


各[バスドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/bus-drivers)は、子デバイスが親デバイスに接続されていることを検出すると、フレームワークデバイスオブジェクトを作成する必要があります。 親デバイスは通常、バスですが、各機能が個別のドライバーセット (デジタルオーディオと MIDI をサポートするサウンドカードなど) を必要とする多機能デバイスである場合もあります。 バスドライバーによって作成されるデバイスオブジェクトは、物理デバイスオブジェクト (PDOs) と呼ばれます。これは、それぞれが1つのハードウェア (子) から別のハードウェア (親) への実際の接続を表しているためです。

バスに接続されているデバイスを識別して報告するプロセスを、 *bus 列挙*と呼びます。

-   バスドライバーが[動的バス列挙](dynamic-enumeration.md)を実行すると、その[*EvtChildListCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device) Callback 関数は、 [**wdfdevice\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体へのハンドルを受け取ります。

-   バスドライバーが[静的バス列挙](static-enumeration.md)を実行する場合は、 [**Wdfpdoinitallocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)を呼び出して、WDFDEVICE\_INIT 構造体へのハンドルを取得する必要があります。

バス列挙の詳細については、「[バス上のデバイスの列挙](enumerating-the-devices-on-a-bus.md)」を参照してください。

バスドライバーは、一連の[フレームワークデバイスオブジェクトの初期化メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/#device-init-methods)を呼び出すことができます。これにより、 [**wdfdevice\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体に情報が格納されます。 また、バスドライバーは、[フレームワークの PDO 初期化メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/#pdo-init-methods)を呼び出すことができます。

列挙された子デバイスのフレームワークデバイスオブジェクトを作成するには、通常、次の手順を実行します。

-   バスドライバー固有のコールバック関数を登録しています。

    ほとんどのバスドライバーは、デバイスが必要とするシステムハードウェアリソースを指定する必要があるため、 [**Wdfpdoinitseteventcallbacks バック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitseteventcallbacks)を呼び出します。 ハードウェアリソースの指定の詳細については、「[フレームワークベースのドライバーのハードウェアリソース](hardware-resources-for-kmdf-drivers.md)」を参照してください。 デバイスとドライバーでの取り出しがサポートされている場合は、追加のコールバック関数を登録できます。

-   [デバイス識別文字列](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)を報告しています。

    バスドライバーは、 [**Wdfpdoinit割り当て deviceid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassigndeviceid)、 [**wdfpdoinit割り当て instanceid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassigninstanceid)、 [**wdfpdoinitassigndeviceid id**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitaddcompatibleid)、および文字列の種類ごと[**に、デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitaddhardwareid)の識別文字列を報告する必要があります。デバイスでがサポートされています。 さらに、バージョン1.9 以降のフレームワークを使用するバスドライバーは、 [**Wdfpdoinit割り当ての containerid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassigncontainerid)を呼び出すことができます。

-   バスドライバーが raw モードでデバイスをサポートできるかどうかを報告します。

    バスドライバーがデバイスの raw モードをサポートしている場合は、 [**Wdfpdoinit割り当て Rawdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)を呼び出す必要があります。

-   デバイスを説明する表示可能なテキストを提供します。

    バスドライバーは、 [**Wdfpdoinitadddevicetext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitadddevicetext)と[**Wdfpdoinitadddevicetext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitsetdefaultlocale)を呼び出して、デバイスを説明するテキストを複数の言語でユーザーに提供します。

-   デバイスオブジェクトを作成しています。

    デバイスオブジェクトを作成する最後の手順は、 [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出すことです。

[**Wdfpdoinitallocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)から取得した wdfdevice\_INIT 構造体を初期化しているときに、ドライバーでエラーが発生した場合、ドライバーは[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)ではなく[**wdfdeviceinitfree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)を呼び出す必要があります。

バスドライバーは、デバイスオブジェクトを作成した後、通常は[**WdfDeviceSetPnpCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetpnpcapabilities)と[**Wdfdevicesetpowercapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetpowercapabilities)を呼び出して、デバイスのプラグアンドプレイと電源機能を報告します。

各バスドライバーは、バスアダプターの関数ドライバーでもあります。 そのため、ドライバーは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数も提供する必要があります。 このコールバック関数は、システム上の各バスアダプターに対して機能デバイスオブジェクト (FDO) を作成します。 FDOs の作成の詳細については、「[関数ドライバーでのデバイスオブジェクトの作成](creating-device-objects-in-a-function-driver.md)」を参照してください。

 

 





