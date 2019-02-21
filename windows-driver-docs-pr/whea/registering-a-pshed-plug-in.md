---
title: プラグインの PSHED を登録します。
description: プラグインの PSHED を登録します。
ms.assetid: 8b710aa2-1477-4906-b5cb-d269d821ea28
keywords:
- プラットフォーム固有のハードウェア エラー ドライバー プラグインを WDK WHEA、登録します。
- PSHED プラグイン WDK WHEA を登録します。
- PSHED プラグイン WDK WHEA、登録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85bc147fdf0f860f164480c9c9ba21f6ebc566f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550630"
---
# <a name="registering-a-pshed-plug-in"></a>プラグインの PSHED を登録します。


プラグインの PSHED 自身を登録、PSHED で呼び出すことによって、 [ **PshedRegisterPlugin** ](https://msdn.microsoft.com/library/windows/hardware/ff559466)に初期化されたポインターを渡す関数[ **WHEA\_PSHED\_プラグイン\_登録\_パケット**](https://msdn.microsoft.com/library/windows/hardware/ff560617)構造体。 通常、プラグインの PSHED を呼び出します、 **PshedRegisterPlugin**内でいずれかの関数からその[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)関数またはその[ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)関数。

プラグインの PSHED を呼び出すことができます[ **PshedIsSystemWheaEnabled** ](https://msdn.microsoft.com/library/windows/hardware/ff559465)呼び出し WHEA 有効にする前に、システムは、かどうかを確認するのには**PshedRegisterPlugin**します。

PSHED のプラグインが正常に登録された後自体、PSHED で、オペレーティング システムのセッションの間の登録解除することはできません。 したがって、プラグインの登録済みの PSHED をシステムからアンロードすることはできませんまたはバグ チェックが発生する可能性があります。 そのため、PSHED プラグインを実装しない、 [**アンロード**](https://msdn.microsoft.com/library/windows/hardware/ff564886)関数。

次のコード例では、エラー情報の取得とエラー レコードの永続化に参加している PSHED プラグインの登録を示します。

```cpp
// Prototypes for the callback functions for
// participating in error information retrieval
NTSTATUS
  RetrieveErrorInfo(
    IN OUT PVOID  PluginContext,
    IN PWHEA_ERROR_SOURCE_DESCRIPTOR  ErrorSource,
    IN ULONG64  BufferLength,
    IN OUT PWHEA_ERROR_PACKET  Packet
    );

NTSTATUS
  FinalizeErrorRecord(
    IN OUT PVOID  PluginContext,
    IN PWHEA_ERROR_SOURCE_DESCRIPTOR  ErrorSource,
    IN ULONG  BufferLength,
    IN OUT PWHEA_ERROR_RECORD  ErrorRecord
    );

NTSTATUS
  ClearErrorStatus(
    IN OUT PVOID  PluginContext,
    IN PWHEA_ERROR_SOURCE_DESCRIPTOR  ErrorSource,
    IN ULONG  BufferLength,
    IN PWHEA_ERROR_RECORD  ErrorRecord
    );

// Prototypes for the callback functions for
// participating in error record persistence.
NTSTATUS
  WriteErrorRecord(
    IN OUT PVOID  PluginContext,
    IN ULONG  Flags,
    IN ULONG  RecordLength,
    IN PWHEA_ERROR_RECORD  ErrorRecord
    );

NTSTATUS
  ReadErrorRecord(
    IN OUT PVOID  PluginContext,
    IN ULONG  Flags,
    IN ULONGLONG  ErrorRecordId
    IN PULONGLONG  NextErrorRecordId
 IN OUT PULONG  RecordLength,
    OUT PWHEA_ERROR_RECORD  *ErrorRecord
    );

NTSTATUS
  ClearErrorRecord(
    IN OUT PVOID  PluginContext,
    IN ULONG  Flags,
    IN ULONGLONG  ErrorRecordId
    );

// The PSHED plug-in registration packet
WHEA_PSHED_PLUGIN_REGISTRATION_PACKET RegPacket =
{
  sizeof(WHEA_PSHED_PLUGIN_REGISTRATION_PACKET),
 WHEA_PLUGIN_REGISTRATION_PACKET_VERSION,
 NULL,
 PshedFAErrorInfoRetrieval | PshedFAErrorRecordPersistence,
  0,
  {
    NULL,
    NULL,
    NULL,
    NULL,
    NULL,
    NULL,
    WriteErrorRecord,
    ReadErrorRecord,
    ClearErrorRecord,
    RetrieveErrorInfo,
    FinalizeErrorRecord,
    ClearErrorStatus,
    NULL,
    NULL,
    NULL
  }
}

//
// The PSHED plug-in&#39;s DriverEntry function
//
NTSTATUS
  DriverEntry(
    IN PDRIVER_OBJECT DriverObject,
    IN PUNICODE_STRING RegistryPath
    )
{
  BOOLEAN IsWheaEnabled;
  NTSTATUS Status;

  ...

  // No unload function
  DriverObject->DriverUnload = NULL;

  // Query if the system is WHEA-enabled
  IsWheaEnabled =
    PshedIsSystemWheaEnabled(
      );

  // Check result
  if (IsWheaEnabled == FALSE)
  {
    // Return "not supported" status
    return STATUS_NOT_SUPPORTED;
  }

  // Register the PSHED plug-in
  Status =
    PshedRegisterPlugin(
      &RegPacket
      );

  // Check status
  if (Status != STATUS_SUCCESS)
  {
    // Handle error
    ...
  }

  ...

  // Return success
  return STATUS_SUCCESS;
}
```

 

 




