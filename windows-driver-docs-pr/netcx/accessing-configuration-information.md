---
title: 構成情報へのアクセス
description: 構成情報へのアクセス
ms.assetid: ABEC75AE-9CE3-4574-B388-BC48D2BC8154
keywords:
- 構成情報にアクセスする NetAdapterCx、NetCx が構成情報にアクセスする
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 193a2e454fd79ff4cc75042623822427f85fde48
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838294"
---
# <a name="accessing-configuration-information"></a>構成情報へのアクセス

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx クラス拡張は、クライアントドライバーのレジストリパラメーターへのアクセスを提供する一連の関数をサポートしています。

通常、クライアントドライバーは、 [*EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数から構成情報を読み取ります。

NetAdapter オブジェクトの場合は、まず[**NetAdapterOpenConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapteropenconfiguration)を呼び出して、構成オブジェクトへのハンドルを取得します。  その後、次のクエリを実行できます。

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

ネットワークデバイスの構成オブジェクトを開いてクエリを実行すると、次のようになります。

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

ULONG データ、文字列、複数文字列 (REG_MULTI_SZ に似ています)、バイナリ blob、およびソフトウェア構成可能なネットワークアドレスに対してクエリを実行するための `NetConfiguration*` 関数があります。

* [**Netconfiguration割り当てバイナリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationassignbinary)
* [**Netconfiguration割り当ての文字列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationassignmultistring)
* [**Netconfiguration割り当て Ulong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationassignulong)
* [**NetConfigurationAssignUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationassignunicodestring)
* [**NetConfigurationClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationclose)
* [**NetConfigurationOpenSubConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationopensubconfiguration)
* [**NetConfigurationQueryBinary**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationquerybinary)
* [**NetConfigurationQueryMultiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationquerymultistring)
* [**Netconfigurationquerylinkレイヤーアドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationquerylinklayeraddress)
* [**NetConfigurationQueryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationquerystring)
* [**NetConfigurationQueryUlong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationqueryulong)
