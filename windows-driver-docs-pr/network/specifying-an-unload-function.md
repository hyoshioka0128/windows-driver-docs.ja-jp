---
title: アンロード関数の指定
description: アンロード関数の指定
ms.assetid: 3bfac8a5-1367-40bd-81b5-4a7fb9aaaece
keywords:
- Windows フィルタリングプラットフォームのコールアウトドライバーの WDK、初期化
- コールアウトドライバー WDK Windows フィルタリングプラットフォーム、初期化
- コールアウトドライバーの初期化 WDK Windows フィルタリングプラットフォーム
- WDM ベースのコールアウトドライバーの WDK Windows フィルタリングプラットフォーム
- WDF ベースのコールアウトドライバー (WDK Windows フィルタリングプラットフォーム)
- unload 関数 WDK Windows Filtering Platform
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab42a478ead3b77a2fc49b295322877f51b97670
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841872"
---
# <a name="specifying-an-unload-function"></a>アンロード関数の指定


コールアウトドライバーは、unload 関数を提供する必要があります。 システムからコールアウトドライバーがアンロードされると、オペレーティングシステムはこの関数を呼び出します。 コールアウトドライバーの unload 関数は、コールアウトドライバーがシステムメモリからアンロードされる前に、フィルターエンジンからコールアウトドライバーのコールアウトが登録解除されることを保証する必要があります。 コールアウトドライバーが unload 関数を提供していない場合、システムからはそのドライバーをアンロードできません。

コールアウトドライバーが unload 関数を指定する方法は、コールアウトドライバーが Windows Driver Model (WDM) と Windows ドライバーフレームワーク (WDF) のどちらに基づいているかによって異なります。

### <a name="wdm-based-callout-drivers"></a>WDM ベースのコールアウトドライバー

コールアウトドライバーが WDM に基づいている場合は、その[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数に[**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)関数を指定します。 次に、例を示します。

```C++
VOID
 Unload(
    IN PDRIVER_OBJECT DriverObject
    );

NTSTATUS
 DriverEntry(
    IN PDRIVER_OBJECT DriverObject,
    IN PUNICODE_STRING RegistryPath
    )
{
  ...

  // Specify the callout driver's Unload function
 DriverObject->DriverUnload = Unload;

  ...
}
```

### <a name="wdf-based-callout-drivers"></a>WDF ベースのコールアウトドライバー

コールアウトドライバーが WDF に基づいている場合は、その[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数で[*Evtdriverunload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)関数を指定します。 次に、例を示します。

```C++
VOID
 Unload(
    IN WDFDRIVER Driver
    );

NTSTATUS
 DriverEntry(
    IN PDRIVER_OBJECT DriverObject,
    IN PUNICODE_STRING RegistryPath
    )
{
  NTSTATUS status;
  WDF_DRIVER_CONFIG config;
  WDFDRIVER driver;

  ...

  // Initialize the driver config structure
  WDF_DRIVER_CONFIG_INIT(&config, NULL);

  // Indicate that this is a non-PNP driver
 config.DriverInitFlags = WdfDriverInitNonPnpDriver;

  // Specify the callout driver's Unload function
 config.EvtDriverUnload = Unload;

  // Create a WDFDRIVER object
 status =
 WdfDriverCreate(
 DriverObject,
 RegistryPath,
      NULL,
      &config,
      &driver
      );

  ...

 return status;
}
```

コールアウトドライバーの unload 関数を実装する方法の詳細については、「[コールアウトドライバーのアンロード](unloading-a-callout-driver.md)」を参照してください。

 

 





