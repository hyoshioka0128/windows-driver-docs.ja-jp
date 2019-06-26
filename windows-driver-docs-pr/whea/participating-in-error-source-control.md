---
title: エラー ソース管理への参加
description: エラー ソース管理への参加
ms.assetid: 4b2e3431-348f-48b1-924e-14b9fb5a48f0
keywords:
- Windows ハードウェア アーキテクチャ WDK のエラー、エラーのソース管理
- WHEA WDK、エラーのソース管理
- ハードウェア エラー WDK WHEA、エラーのソース管理
- WDK WHEA、エラーのソース管理のエラー
- プラットフォーム固有のハードウェア エラー ドライバー プラグインを WDK WHEA、エラーのソース管理
- PSHED プラグイン WDK WHEA、エラーのソース管理
- エラー ソース制御 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea98823fdefe85f8fe0745aae3ba8a11fe43fc32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386451"
---
# <a name="participating-in-error-source-control"></a>エラー ソース管理への参加


エラーのソース管理に参加するには、プラグイン PSHED は次のコールバック関数を実装する必要があります。

[*SetErrorSourceInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pshed_pi_set_error_source_info)

[*EnableErrorSource*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pshed_pi_enable_error_source)

[*DisableErrorSource*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pshed_pi_disable_error_source)

次のコード例では、これらのコールバック関数を実装する方法を示します。

```cpp
//
// The PSHED plug-in's SetErrorSourceInfo callback function
//
NTSTATUS
  SetErrorSourceInfo(
    IN OUT PVOID PluginContext,
    IN PWHEA_ERROR_SOURCE_DESCRIPTOR ErrorSource
    )
{
  // Check if the plug-in supports configuring
  // the specified error source.
  if (...)
  {
    // Save the new configuration data for the error
    // source in nonvolatile storage and apply the
    // configuration changes to the error source such
    // that they will become effective after the
    // system is restarted.
    ...

    // If successful, return success status
    if (...)
    {
      return STATUS_SUCCESS;
    }

    // Failed to configure the error source
    else
    {
      return STATUS_UNSUCCESSFUL;
    }
  }

  // Not supported by the plug-in
  else
  {
    return STATUS_NOT_SUPPORTED;
  }
}

//
// The PSHED plug-in's EnableErrorSource callback function
//
NTSTATUS
  EnableErrorSource(
    IN OUT PVOID PluginContext,
    IN PWHEA_ERROR_SOURCE_DESCRIPTOR ErrorSource
    )
{
  // Check if the plug-in supports enabling
  // the specified error source.
  if (...)
  {
    // Enable the error source
    ...

    // If successful
    if (...)
    {
      // Return success status
      return STATUS_SUCCESS;
    }

    // Failed to enable the error source
    else
    {
      return STATUS_UNSUCCESSFUL;
    }
  }

  // Not supported by the plug-in
  else
  {
    return STATUS_NOT_SUPPORTED;
  }
}

//
// The PSHED plug-in's DisableErrorSource callback function
//
NTSTATUS
  DisableErrorSource(
    IN OUT PVOID PluginContext,
    IN PWHEA_ERROR_SOURCE_DESCRIPTOR ErrorSource
    )
{
  // Check if the plug-in supports disabling
  // the specified error source.
  if (...)
  {
    // Disable the error source
    ...

    // If successful
    if (...)
    {
      // Return success status
      return STATUS_SUCCESS;
    }

    // Failed to disable the error source
    else
    {
      return STATUS_UNSUCCESSFUL;
    }
  }

  // Not supported by the plug-in
  else
  {
    return STATUS_NOT_SUPPORTED;
  }
}
```

エラーのソース管理に参加している PSHED プラグインを指定する必要があります、 **PshedFAErrorSourceControl**フラグを付けるときに、[登録](registering-a-pshed-plug-in.md)オペレーティング システム自体。

 

 




