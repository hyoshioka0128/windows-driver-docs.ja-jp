---
title: 構成情報へのアクセス
description: 構成情報へのアクセス
ms.assetid: ABEC75AE-9CE3-4574-B388-BC48D2BC8154
keywords:
- NetAdapterCx NetCx 構成情報へのアクセスの構成情報にアクセスします。
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f2e09537287771d493419bd55d84051b6beba4a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386372"
---
# <a name="accessing-configuration-information"></a>構成情報へのアクセス

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx クラスの拡張機能には、一連のクライアント ドライバーのレジストリ パラメーターへのアクセスを提供する関数がサポートしています。

通常、クライアント ドライバーがから構成情報を読み取り、 [ *EVT_WDF_DRIVER_DEVICE_ADD* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数。

NetAdapter オブジェクトで呼び出すことによって開始[ **NetAdapterOpenConfiguration** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapteropenconfiguration)構成オブジェクトを識別するハンドルを取得します。  これを照会できます。

```C++
NETCONFIGURATION configuration;

status = NetAdapterOpenConfiguration(NetAdapter, 
                                     WDF_NO_OBJECT_ATTRIBUTES, 
                                     &configuration);
if (!NT_SUCCESS(status)) {
    return status;
}

status = NetConfigurationQueryUlong(configuration, 
                                    NET_CONFIGURATION_QUERY_ULONG_NO_FLAGS, 
                                    &SomeValue, 
                                    &myvalue);

NetConfigurationClose(configuration);
```

開くと、ネットワーク デバイスの構成オブジェクトのクエリを実行するには、似ています。

```C++
status = NetDeviceOpenConfiguration(Device, 
                                    WDF_NO_OBJECT_ATTRIBUTES, 
                                    &configuration);
if(!NT_SUCCESS(status))
{
    return status;
}

WDFCOLLECTION myStrings;

DECLARE_CONST_UNICODE_STRING(myValueName, L"ExampleValueName");

status = NetConfigurationQueryMultiString(configuration,
                                          myValueName,
                                          WDF_NO_OBJECT_ATTRIBUTES,
                                          myStrings);
```

ある`NetConfiguration*`ULONG データ、文字列、(REG_MULTI_SZ と同様に) 複数の文字列、バイナリの blob、およびソフトウェア構成可能なネットワーク アドレスを照会するための機能。

* [**NetConfigurationAssignBinary**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationassignbinary)
* [**NetConfigurationAssignMultiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationassignmultistring)
* [**NetConfigurationAssignUlong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationassignulong)
* [**NetConfigurationAssignUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationassignunicodestring)
* [**NetConfigurationClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationclose)
* [**NetConfigurationOpenSubConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationopensubconfiguration)
* [**NetConfigurationQueryBinary**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationquerybinary)
* [**NetConfigurationQueryMultiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationquerymultistring)
* [**NetConfigurationQueryLinkLayerAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationquerylinklayeraddress)
* [**NetConfigurationQueryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationquerystring)
* [**NetConfigurationQueryUlong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationqueryulong)
