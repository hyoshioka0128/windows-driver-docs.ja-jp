---
title: ドライバーでの WMI サポートの初期化
description: ドライバーでの WMI サポートの初期化
ms.assetid: cf79176c-8e08-45f9-b2fb-a82707d8667b
keywords:
- WMI WDK KMDF, 初期化サポート
- プロバイダーインスタンス WDK KMDF
- 複数のプロバイダーインスタンス WDK KMDF
- 単一プロバイダーインスタンス WDK KMDF
- MOF リソース名 WDK KMDF を登録しています
- MOF リソース名 WDK KMDF
- WMI の初期化サポート WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3048221c9d2fc7b814cdbb409240709c4e64f44b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845439"
---
# <a name="initializing-wmi-support-in-your-driver"></a>ドライバーでの WMI サポートの初期化


\[は KMDF にのみ適用され\]

フレームワークベースのドライバーである WMI データブロックをサポートするには、次のようにします。

-   *Wmicore*で定義されていない、カスタマイズされた WMI データプロバイダーの管理オブジェクトフォーマット (MOF) リソース名を登録します。

-   読み取りまたは書き込みが可能なデータブロックを表す1つ以上の WMI インスタンスオブジェクトを作成します。

-   必要に応じて、ドライバーが提供する WMI データを提供する1つ以上のイベントコールバック関数を実装します。

-   各 WMI インスタンスオブジェクトを登録して、WMI クライアントで使用できるようにします。

WMI サポートを初期化するには、KMDF ドライバーが次の手順を実行します。通常は、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)または[*Evtdeviceselfmanagedioinit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)コールバック内で行います。

1.  カスタマイズされた WMI データプロバイダーをサポートするための MOF ファイルを提供するドライバーは、データプロバイダーを表す WMI プロバイダーオブジェクトを作成する前に、 [**WdfDeviceAssignMofResourceName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignmofresourcename)メソッドを呼び出して mof リソース名を登録する必要があります。

2.  WMI プロバイダーの構成構造を初期化し、必要に応じて WMI プロバイダーオブジェクト (WDFWMIPROVIDER) を作成します。
3.  WMI インスタンスの構成構造を初期化し、WMI インスタンスオブジェクト (WDFWMIINSTANCE) を作成します。

既定では、KMDF ドライバーによって最初の WMI インスタンスが作成されるときに、フレームワークによって WMI プロバイダーが作成されます。 したがって、ドライバーが必要とする WMI プロバイダーが1つだけの場合は、プロバイダーの作成メソッド ([**WdfWmiProviderCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiprovidercreate)) を呼び出す必要はありません。 ただし、この構造体は、インスタンスの作成時にフレームワークが使用するプロバイダーに関する情報を提供するため、プロバイダーの構成構造を設定する必要があります。

ドライバーがサポートしている各 WMI データブロックの1つのインスタンスを作成する場合、ドライバーは[**WdfWmiInstanceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiinstancecreate)を呼び出し、 [**WDF\_wmi\_プロバイダー\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/ns-wdfwmi-_wdf_wmi_provider_config)構造体と WDF\_wmi の両方を渡し[ **\_インスタンス\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/ns-wdfwmi-_wdf_wmi_instance_config)構造体。 この1回の呼び出しでは、単一のフレームワークによって提供される WMI プロバイダーオブジェクトが構成され、WMI インスタンスオブジェクトが作成されます。

ドライバーが WMI データブロックの複数のインスタンスを作成する場合、ドライバーは[**WdfWmiProviderCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiprovidercreate)と[**WdfWmiInstanceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiinstancecreate)の両方を呼び出す必要があります。

### <a href="" id="registering-provider-instances"></a>プロバイダーインスタンスの登録

WMI クライアントがドライバーの WMI データブロックにアクセスできるようにするには、ドライバーがそのプロバイダーのインスタンスをシステムの WMI サービスに登録する必要があります。 ドライバーは、次のいずれかの方法を使用してプロバイダーインスタンスを登録できます。

-   プロバイダーインスタンスの[**WDF\_WMI\_\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/ns-wdfwmi-_wdf_wmi_instance_config)の**レジスタ**メンバーを**TRUE**に設定します。

    ドライバーで**Register**が**TRUE**に設定されている場合、デバイスが最初に動作 (D0) 状態になったときに、フレームワークによってインスタンスが自動的に登録されます。

-   [**WdfWmiInstanceRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiinstanceregister)メソッドを呼び出します。

    ドライバーが[**WdfWmiInstanceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiinstancecreate)を呼び出した後に[**WdfWmiInstanceRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiinstanceregister)を呼び出すと、デバイスが動作 (D0) 状態になった後にインスタンスが登録されます。

フレームワークは、インスタンスのデバイスが削除されると (および、 [*Evtdeviceselfmanagediocleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)イベントコールバック関数を呼び出す前に)、各プロバイダーインスタンスを自動的に解除します。 フレームワークがドライバーのコールバック関数を呼び出す順序の詳細については、「 [PnP および電源管理のシナリオ](pnp-and-power-management-scenarios.md)」を参照してください。

ドライバーは、 [**WdfWmiInstanceDeregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiinstancederegister)を呼び出すことによって、いつでもインスタンスの登録を解除できます。

 

 





