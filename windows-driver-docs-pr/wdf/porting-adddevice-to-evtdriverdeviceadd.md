---
title: AddDevice から EvtDriverDeviceAdd への移植
description: AddDevice から EvtDriverDeviceAdd への移植
ms.assetid: 8FCFDA98-621E-415E-83D7-0371F55DD8A8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bdb18384c9658909cd78d99820d8665174cfe48
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842259"
---
# <a name="porting-adddevice-to-evtdriverdeviceadd"></a>AddDevice から EvtDriverDeviceAdd への移植


プラグアンドプレイをサポートするすべてのカーネルモードドライバーフレームワーク (KMDF) またはユーザーモードドライバーフレームワーク (UMDF) ドライバーには、WDM ドライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)関数に相当する、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックが必要です。

WDM [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)関数は、デバイスオブジェクトを作成し、デバイスインターフェイスを作成して、WMI を初期化します。また、ドライバーのデバイス拡張機能で多数の変数を初期化します。 WDM ドライバーは、通常、i/o キューと割り込みオブジェクトの作成を遅延させます。これは、 [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)関数を呼び出して、\_デバイスの要求を[**開始\_\_IRP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)を処理します。

フレームワークベースのドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックは、列挙されたばかりのデバイスを表す wdfdevice オブジェクトを作成します。 また、独自の内部構造および基になる WDM 構造体を設定するために必要な情報をフレームワークに提供するために、多くの追加の初期化タスクを実行します。

その結果、ほとんどのフレームワークベースのドライバーでは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックは、対応する WDM [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)関数よりもかなり長くなります。 フレームワークベースのドライバーでは、ほとんどすべてのデバイスの初期化コードが*Evtdriverdeviceadd*関数に含まれています。 ただし、WDM バージョンでは、初期化コードはドライバー内の複数の関数によって拡散される傾向があります。

[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)のコードは、次の順序で表示されます。

1.  [Wdfdevice\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体に入力します。これにより、デバイスオブジェクトの作成に使用される情報が提供されます。 WDFDEVICE\_INIT の使用方法の詳細については、「 [Framework デバイスオブジェクトの作成](creating-a-framework-device-object.md)」を参照してください。
2.  デバイスオブジェクトのコンテキスト領域を設定します。これは、WDM デバイス拡張機能に似ています。
3.  [デバイスオブジェクトを作成](creating-a-framework-device-object.md)します。
4.  [I/o キュー](creating-i-o-queues.md)や[割り込みオブジェクト](creating-an-interrupt-object.md)の作成など、追加の初期化タスクとスタートアップタスクを実行します。

KMDF バスドライバーは、通常、複数のデバイスオブジェクトを作成します。これは、バス自体の関数ドライバーとしてのロールの FDO、およびバスに接続されている各子デバイスの PDO です。 システムがバスを列挙すると、フレームワークはドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)関数を呼び出します。 次に、その子デバイスを列挙し、それを表す PDOs を作成します。 KMDF は、子デバイスの[静的](static-enumeration.md)と[動的](dynamic-enumeration.md)の両方の列挙をサポートします。 また、PDO 固有のその他の機能も含まれています。

## <a name="device-object-context-area"></a>デバイスオブジェクトコンテキスト領域


通常、ドライバーは、ポインターおよびオブジェクト固有のデータを維持するために、デバイスオブジェクトに関連付けられているストレージを必要とします。 WDM ドライバーでは、[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造の**deviceextension**フィールドにこのような記憶域が用意されています。 フレームワークベースのドライバーでは、WDFDEVICE オブジェクトのオブジェクトコンテキスト領域は同じ目的で機能します。

フレームワークオブジェクトのコンテキスト空間の割り当てとアクセスについては、「[フレームワークオブジェクトコンテキスト空間](framework-object-context-space.md)」を参照してください。

## <a name="device-object-creation"></a>デバイスオブジェクトの作成


WDM ドライバーは、各デバイスオブジェクトを表す[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造を作成し、デバイスオブジェクトをプラグアンドプレイデバイススタックにアタッチします。 フレームワークベースのドライバーは、WDFDEVICE ハンドルを使用して参照されるデバイスオブジェクトも作成します。

WDF ドライバーは、必要な初期化メソッドを呼び出すと、デバイスオブジェクトの属性 (通常はコンテキスト領域のサイズと種類) を設定し、次に[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出してデバイスオブジェクトを作成します。 **WdfDeviceCreate**は、wdfdevice オブジェクトと基になる wdm[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)を作成し、wdm**デバイス\_オブジェクト**をデバイススタックにアタッチして、wdfdevice オブジェクトへのハンドルを返します。

## <a name="additional-evtdriverdeviceadd-tasks"></a>追加の EvtDriverDeviceAdd タスク


フレームワークベースのドライバーは、デバイスオブジェクトを作成した後、次のことを行う必要があります。

-   [I/o キューを作成](creating-i-o-queues.md)し、デバイスオブジェクトの[要求ハンドラー](request-handlers.md)を指定します。
-   [デバイスインターフェイスを作成](using-device-interfaces.md)します。
-   デバイスオブジェクトが電源ポリシーを所有している場合は、[デバイスのアイドルポリシー](supporting-idle-power-down.md)と[ウェイク設定](supporting-system-wake-up.md)を設定します。
-   割り込み[オブジェクトを作成](creating-an-interrupt-object.md)します (ハードウェアで割り込みがサポートされている場合)。
-   [WMI を初期化](supporting-wmi-in-kmdf-drivers.md)します。<sup>†</sup>

†この機能は KMDF ドライバーでのみ使用できます。

フレームワークベースのドライバーは、デバイスオブジェクトを作成した直後に、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックで i/o キューを設定し、interrupt オブジェクトを作成する必要があります。 フレームワークは、割り込みオブジェクトを接続し、後で、開始デバイスの処理中にキューを開始します。

## <a name="child-device-enumeration-pdos-kmdf-only"></a>子デバイスの列挙 (PDOs、KMDF のみ)


バスを制御するドライバーは、通常、複数のデバイスオブジェクトを作成します。これは、バス自体の関数ドライバーとしてのロールの FDO、およびバスに接続されている各子デバイスの PDO です。 KMDF は、子デバイスの静的と動的の両方の列挙をサポートします。 また、PDO 固有のその他の機能も含まれています。

フレームワークは、プラグアンドプレイマネージャーがバスを列挙するときに、ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)関数を呼び出します。 *Evtdriverdeviceadd*は、バスの FDO を作成し、子デバイスを列挙して、それぞれに対して PDO を作成します。 ドライバーは、[静的](static-enumeration.md)または[動的](dynamic-enumeration.md)に子デバイスを列挙できます。

特定のコールバック関数は、PDOs を表すデバイスオブジェクトにのみ適用されます。 ドライバーがデバイスオブジェクトを初期化すると、対応するコールバックが登録されます。 PDOs は、デバイスリソースとリソースの要件、デバイスをロックまたは取り出す要求、デバイスのウェイクアップシグナルを有効または無効にする要求に関するクエリに応答します。

WDM ドライバーでは、これらの要求は、 [**irp\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)または[**irp\_MJ\_の電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)要求で、マイナー irp コードとして受信されます。 KMDF ドライバーは、コールバックを実装し、 [**Wdfpdoinitseteventcallbacks バック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitseteventcallbacks)を呼び出すことによって、デバイスオブジェクトの初期化中にコールバックを登録することによって処理します。 次の表に、PDO 固有のコールバックの一覧を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KMDF コールバック</th>
<th align="left">WDM IRP</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query" data-raw-source="[&lt;em&gt;EvtDeviceResourcesQuery&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query)"><em>EvtDeviceResourcesQuery</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resources" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_RESOURCES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resources)"><strong>IRP_MN_QUERY_RESOURCES</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query" data-raw-source="[&lt;em&gt;EvtDeviceResourceRequirementsQuery&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query)"><em>EvtDeviceResourceRequirementsQuery</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_RESOURCE_REQUIREMENTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements)"><strong>IRP_MN_QUERY_RESOURCE_REQUIREMENTS</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_eject" data-raw-source="[&lt;em&gt;EvtDeviceEject&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_eject)"><em>EvtDeviceEject</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-eject" data-raw-source="[&lt;strong&gt;IRP_MN_EJECT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-eject)"><strong>IRP_MN_EJECT</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_set_lock" data-raw-source="[&lt;em&gt;EvtDeviceSetLock&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_set_lock)"><em>EvtDeviceSetLock</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-lock" data-raw-source="[&lt;strong&gt;IRP_MN_SET_LOCK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-lock)"><strong>IRP_MN_SET_LOCK</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus" data-raw-source="[&lt;em&gt;EvtDeviceEnableWakeAtBus&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus)"><em>EvtDeviceEnableWakeAtBus</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake" data-raw-source="[&lt;strong&gt;IRP_MN_WAIT_WAKE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)"><strong>IRP_MN_WAIT_WAKE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus" data-raw-source="[&lt;em&gt;EvtDeviceDisableWakeAtBus&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus)"><em>EvtDeviceDisableWakeAtBus</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake" data-raw-source="[&lt;strong&gt;IRP_MN_WAIT_WAKE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)"><strong>IRP_MN_WAIT_WAKE</strong></a></p></td>
</tr>
</tbody>
</table>

 

追加の**Wdfpdoinitxxx**メソッドを使用すると、ドライバーはデバイス id などのデバイス固有のデータを指定できます。

 

 





