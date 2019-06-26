---
title: AddDevice から EvtDriverDeviceAdd への移植
description: AddDevice から EvtDriverDeviceAdd への移植
ms.assetid: 8FCFDA98-621E-415E-83D7-0371F55DD8A8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2aa0115440112f17dddf209c9282070e036ecba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379658"
---
# <a name="porting-adddevice-to-evtdriverdeviceadd"></a>AddDevice から EvtDriverDeviceAdd への移植


プラグ アンド プレイをサポートしているすべてのカーネル モード ドライバー フレームワーク (KMDF) またはユーザー モード ドライバー フレームワーク (UMDF) ドライバーが必要、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックは、機能と同等のWDM ドライバーの[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)関数。

WDM [ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)関数デバイス オブジェクトを作成、デバイスのインターフェイスを作成および WMI を初期化しますがもドライバーのデバイスの拡張機能の多くの変数を初期化します。 WDM ドライバーは通常の I/O キューとまでは、割り込みオブジェクトの作成を遅らせる、 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)を処理する関数が呼び出された、 [ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求。

フレームワーク ベースのドライバーの[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックが列挙されているデバイスを表す WDFDEVICE オブジェクトを作成します。 また、独自の内部構造と基になる WDM 構造を設定することが必要な情報を提供する多数の追加の初期化タスクを実行します。

ほとんどのフレームワークに基づいたドライバーの結果として、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックは、対応する WDM を大幅に超える[ *AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)関数。 フレームワーク ベースのドライバーでほぼすべてのデバイスの初期化コードが、 *EvtDriverDeviceAdd*関数。 ただし、WDM バージョンでは、初期化コードが、ドライバーでの複数の関数を使用してを分散する傾向があります。

コードでは、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)次の順序で表示されます。

1.  入力、 [WDFDEVICE\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体は、デバイス オブジェクトを作成するために使用する情報を提供します。 WDFDEVICE の使用の詳細については\_INIT を参照してください[Framework デバイス オブジェクトを作成する](creating-a-framework-device-object.md)します。
2.  WDM デバイス拡張機能に似ていますが、デバイス オブジェクトのコンテキストの領域を設定します。
3.  [デバイス オブジェクトを作成](creating-a-framework-device-object.md)です。
4.  など、追加の初期化と、スタートアップ タスクを実行[I/O キューの作成](creating-i-o-queues.md)と[オブジェクトを中断](creating-an-interrupt-object.md)します。

KMDF バス ドライバーは通常、複数のデバイス オブジェクトを作成します。 バス自体の関数のドライバーとしての役割に FDO とバスに接続されている子デバイスごとの PDO します。 フレームワークは、ドライバーの[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)システム バスを列挙するときに機能します。 ドライバー自体は、その子デバイスを列挙し、それを表すための Pdo を作成します。 KMDF は両方ともサポート[静的](static-enumeration.md)と[動的](dynamic-enumeration.md)子デバイスの列挙体。 PDO 固有の追加機能も含まれています。

## <a name="device-object-context-area"></a>デバイス オブジェクトのコンテキストの領域


ドライバーには、通常ポインターとオブジェクト固有のデータを維持するためにデバイス オブジェクトに関連付けられている記憶域が必要です。 WDM ドライバーで、 **DeviceExtension**のフィールド、 [**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)構造体は、このようなストレージを提供します。 フレームワーク ベースのドライバーでは、WDFDEVICE オブジェクトのオブジェクト コンテキストの領域は、同じ目的を果たします。

割り当てとフレームワーク オブジェクト コンテキストの領域にアクセスする方法については、次を参照してください。[フレームワーク オブジェクト コンテキストの空間](framework-object-context-space.md)します。

## <a name="device-object-creation"></a>デバイス オブジェクトの作成


WDM ドライバーを作成、 [**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)を各デバイス オブジェクトを表す構造体であり、プラグ アンド プレイ デバイス スタックにデバイス オブジェクトをアタッチします。 フレームワーク ベースのドライバーでは、WDFDEVICE ハンドルを使用して参照されるデバイス オブジェクトも作成します。

デバイス オブジェクトの属性を設定、WDF ドライバーが必要な初期化メソッドを呼び出してから (通常は、コンテキストの領域の種類とサイズ) を呼び出して、 [ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)を作成する、デバイス オブジェクト。 **WdfDeviceCreate** WDFDEVICE オブジェクトと、基になる WDM 作成[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)、WDM をアタッチします**デバイス\_オブジェクト**デバイス スタックに WDFDEVICE オブジェクトにハンドルを返します。

## <a name="additional-evtdriverdeviceadd-tasks"></a>追加 EvtDriverDeviceAdd タスク


フレームワーク ベースのドライバーには、デバイス オブジェクトが作成されたら、その必要があります。

-   [I/O キューを作成](creating-i-o-queues.md)指定と[要求ハンドラー](request-handlers.md)デバイス オブジェクト。
-   [デバイスのインターフェイスを作成](using-device-interfaces.md)です。
-   設定[アイドル状態のデバイス ポリシー](supporting-idle-power-down.md)と[wake 設定](supporting-system-wake-up.md)デバイス オブジェクトには、電源ポリシーが所有している場合、します。
-   [割り込みオブジェクトを作成](creating-an-interrupt-object.md)ハードウェア割り込みをサポートしている場合、します。
-   [WMI の初期化](supporting-wmi-in-kmdf-drivers.md).<sup>†</sup>

† この機能は、KMDF ドライバーをできるだけです。

フレームワーク ベースのドライバーの I/O キューの設定し、割り込みオブジェクトを作成する必要があります、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)デバイス オブジェクトを作成した直後に、コールバック。 フレームワークでは、割り込みオブジェクトを接続し、後で、適切な時にデバイスの起動処理中に、キューを開始します。

## <a name="child-device-enumeration-pdos-kmdf-only"></a>子デバイスの列挙 (Pdo、KMDF のみ)


通常、バスを制御するドライバーが複数のデバイス オブジェクトを作成します。 バス自体の関数のドライバーとしての役割に FDO とバスに接続されている子デバイスごとの PDO。 KMDF 子デバイスの静的および動的の両方の列挙をサポートしています。 PDO 固有の追加機能も含まれています。

フレームワークは、ドライバーを呼び出す[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)プラグ アンド プレイ manager バスを列挙するときに機能します。 *EvtDriverDeviceAdd*バスの FDO を作成し、し、子デバイスを列挙し、それぞれの PDO を作成します。 ドライバーでは、子のデバイスをか列挙[静的](static-enumeration.md)または[動的に](dynamic-enumeration.md)します。

特定のコールバック関数は、Pdo を表すデバイス オブジェクトにのみ適用されます。 ドライバーのデバイス オブジェクトの初期化とは、対応するコールバックを登録します。 Pdo は、デバイスのリソースとリソース要件、ロック、または、デバイスを取り出すへの要求についてのクエリに応答し、要求を有効にし、デバイスを無効にする信号をスリープ解除します。

マイナー IRP コードとして WDM ドライバーにこれらの要求が送られてくる、 [ **IRP\_MJ\_PNP** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)または[ **IRP\_MJ\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)要求。 KMDF ドライバーでは、それらを処理のコールバックを実装して、デバイス オブジェクトの初期化中に呼び出すことによってコールバックを登録して[ **WdfPdoInitSetEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitseteventcallbacks)します。 次の表では、PDO 固有のコールバックを示します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query" data-raw-source="[&lt;em&gt;EvtDeviceResourcesQuery&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query)"><em>EvtDeviceResourcesQuery</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resources" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_RESOURCES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resources)"><strong>IRP_MN_QUERY_RESOURCES</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query" data-raw-source="[&lt;em&gt;EvtDeviceResourceRequirementsQuery&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query)"><em>EvtDeviceResourceRequirementsQuery</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_RESOURCE_REQUIREMENTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements)"><strong>IRP_MN_QUERY_RESOURCE_REQUIREMENTS</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_eject" data-raw-source="[&lt;em&gt;EvtDeviceEject&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_eject)"><em>EvtDeviceEject</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-eject" data-raw-source="[&lt;strong&gt;IRP_MN_EJECT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-eject)"><strong>IRP_MN_EJECT</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_set_lock" data-raw-source="[&lt;em&gt;EvtDeviceSetLock&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_set_lock)"><em>EvtDeviceSetLock</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-lock" data-raw-source="[&lt;strong&gt;IRP_MN_SET_LOCK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-lock)"><strong>IRP_MN_SET_LOCK</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus" data-raw-source="[&lt;em&gt;EvtDeviceEnableWakeAtBus&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus)"><em>EvtDeviceEnableWakeAtBus</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake" data-raw-source="[&lt;strong&gt;IRP_MN_WAIT_WAKE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)"><strong>IRP_MN_WAIT_WAKE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus" data-raw-source="[&lt;em&gt;EvtDeviceDisableWakeAtBus&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus)"><em>EvtDeviceDisableWakeAtBus</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake" data-raw-source="[&lt;strong&gt;IRP_MN_WAIT_WAKE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)"><strong>IRP_MN_WAIT_WAKE</strong></a></p></td>
</tr>
</tbody>
</table>

 

追加**WdfPdoInitXxx**メソッドは、デバイス Id などのデバイスに固有のデータを指定するドライバーを有効にします。

 

 





