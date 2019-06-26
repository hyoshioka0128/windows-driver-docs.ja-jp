---
title: アンロード関数の指定
description: アンロード関数の指定
ms.assetid: 3bfac8a5-1367-40bd-81b5-4a7fb9aaaece
keywords:
- Windows Filtering Platform コールアウト ドライバー WDK、初期化しています
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォームの初期化
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォームの初期化
- WDM ベース コールアウト ドライバー WDK Windows フィルタ リング プラットフォーム
- WDF ベース コールアウト ドライバー WDK Windows フィルタ リング プラットフォーム
- 関数 WDK Windows フィルタ リング プラットフォームをアンロードします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95526a041a191e881ce82b40685550e687e3b111
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374711"
---
# <a name="specifying-an-unload-function"></a>アンロード関数の指定


コールアウト ドライバーでは、アンロード、関数を提供する必要があります。 オペレーティング システムは、コールアウト ドライバーがシステムからアンロードされるときに、この関数を呼び出します。 コールアウト ドライバーのアンロード関数は、コールアウト ドライバーがシステム メモリからアンロードする前に、コールアウト ドライバーのコールアウトはフィルター エンジンから登録しないことを保証する必要があります。 コールアウト ドライバーは、アンロード、関数が提供しない場合、システムからアンロードすることはできません。

コールアウト ドライバーが、アンロード関数を指定しますが、コールアウト ドライバーを Windows Driver Model (WDM) または Windows Driver Frameworks (WDF) に基づいているかどうかによって異なります。

### <a name="wdm-based-callout-drivers"></a>WDM ベース コールアウト ドライバー

かどうかコールアウト ドライバーは WDM に基づいていることを示す、 [**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)関数でその[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)関数。 例:

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

### <a name="wdf-based-callout-drivers"></a>WDF ベース コールアウト ドライバー

かどうかコールアウト ドライバーは WDF に基づいていることを示す、 [ *EvtDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)関数でその[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)関数。 以下に例を示します。

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

コールアウト ドライバーのアンロード関数を実装する方法については、次を参照してください。[コールアウト ドライバーをアンロード](unloading-a-callout-driver.md)します。

 

 





