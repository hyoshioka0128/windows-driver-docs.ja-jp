---
title: ドライバーでの WMI サポートの初期化
description: ドライバーでの WMI サポートの初期化
ms.assetid: cf79176c-8e08-45f9-b2fb-a82707d8667b
keywords:
- WMI の WDK KMDF、サポートの初期化
- プロバイダー インスタンスの WDK KMDF
- 複数のプロバイダー インスタンスの WDK KMDF
- 1 つのプロバイダー インスタンスの WDK KMDF
- 名前を WDK KMDF MOF リソースの登録
- MOF リソース名の WDK KMDF
- WMI のサポートを WDK KMDF の初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8458e8aa055fc6311b171703d34a349761d74667
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371138"
---
# <a name="initializing-wmi-support-in-your-driver"></a>ドライバーでの WMI サポートの初期化


\[KMDF にのみ適用されます。\]

WMI データのブロック、framework ベースのドライバーをサポートするには。

-   レジスタのいずれかの管理オブジェクト フォーマット (MOF) のリソース名のカスタマイズで定義されていない WMI データのプロバイダー *Wmicore.mof*します。

-   読み取りまたは書き込みができるデータ ブロックを表す 1 つ以上の WMI インスタンス オブジェクトを作成します。

-   必要に応じて、ドライバーを提供する WMI データを提供する 1 つ以上のイベントのコールバック関数を実装します。

-   WMI クライアントが使用できるようにする各 WMI インスタンス オブジェクトを登録します。

WMI のサポートを初期化する KMDF ドライバーに依存して次の手順では、通常内でその[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)または[ *EvtDeviceSelfManagedIoInit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)コールバック。

1.  カスタマイズされた WMI データ プロバイダーをサポートするための MOF ファイルを提供するドライバーを呼び出す必要があります、 [ **WdfDeviceAssignMofResourceName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassignmofresourcename)ドライバーは、WMI プロバイダーを作成する前に、MOF リソースの名前を登録する方法データ プロバイダーを表すオブジェクト。

2.  WMI プロバイダーの構成構造を初期化し、必要に応じて、WMI プロバイダー オブジェクト (WDFWMIPROVIDER) を作成します。
3.  WMI インスタンスの構成構造を初期化し、WMI インスタンス オブジェクト (WDFWMIINSTANCE) を作成します。

フレームワークは、KMDF ドライバーは、その最初の WMI インスタンスを作成するときに、既定では、WMI プロバイダーを作成します。 そのため、ドライバーは、1 つの WMI プロバイダーを必要とする場合必要はありません、プロバイダーの作成メソッドを呼び出す ([**WdfWmiProviderCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nf-wdfwmi-wdfwmiprovidercreate))。 ただし、ドライバーは、この構造体のインスタンスを作成するときにフレームワークによって使用されるプロバイダーに関する情報を提供するため、プロバイダーの構成構造を入力する必要があります。

ドライバーの作成の各 WMI データ ブロックの 1 つのインスタンスの場合、サポート ドライバー呼び出し[ **WdfWmiInstanceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nf-wdfwmi-wdfwmiinstancecreate)、両方を渡して、 [ **WDF\_WMI\_プロバイダー\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/ns-wdfwmi-_wdf_wmi_provider_config)構造と[ **WDF\_WMI\_インスタンス\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/ns-wdfwmi-_wdf_wmi_instance_config)構造体。 この 1 回の呼び出し両方は、1 つ framework の WMI プロバイダー オブジェクトを構成し、WMI インスタンス オブジェクトを作成します。

ドライバーが両方を呼び出す必要があります、ドライバーは、その WMI データ ブロックの複数のインスタンスを作成する場合[ **WdfWmiProviderCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nf-wdfwmi-wdfwmiprovidercreate)と[ **WdfWmiInstanceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nf-wdfwmi-wdfwmiinstancecreate)

### <a href="" id="registering-provider-instances"></a> プロバイダーのインスタンスを登録します。

WMI クライアントがアクセスできるは、ドライバーの WMI データのブロック、前に、ドライバーは、システムの WMI サービスとそのプロバイダーのインスタンスを登録する必要があります。 ドライバーは、プロバイダーのインスタンスの登録を次の手法のいずれかを使用できます。

-   設定、**登録**プロバイダーのインスタンスのメンバー [ **WDF\_WMI\_インスタンス\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/ns-wdfwmi-_wdf_wmi_instance_config) 構造**TRUE**します。

    ドライバーが設定されている場合**登録**に**TRUE**フレームワークに自動的にインスタンスを登録、初めての作業 (D0) の状態は、デバイスの入力をします。

-   呼び出す、 [ **WdfWmiInstanceRegister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nf-wdfwmi-wdfwmiinstanceregister)メソッド。

    ドライバーを呼び出す場合[ **WdfWmiInstanceRegister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nf-wdfwmi-wdfwmiinstanceregister)呼び出した後[ **WdfWmiInstanceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nf-wdfwmi-wdfwmiinstancecreate)フレームワークは、インスタンスを登録します。後、デバイスがその作業 (D0) 状態です。

フレームワークに自動的に登録を解除します各プロバイダーのインスタンス、インスタンスのデバイスが削除されると (し、呼び出す前に、 [ *EvtDeviceSelfManagedIoCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)イベント コールバック関数)。 フレームワークがドライバーのコールバック関数を呼び出す順序については、次を参照してください。 [PnP および電源管理のシナリオ](pnp-and-power-management-scenarios.md)します。

ドライバーは呼び出すことによって、いつでもインスタンスを登録することができます[ **WdfWmiInstanceDeregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nf-wdfwmi-wdfwmiinstancederegister)します。

 

 





