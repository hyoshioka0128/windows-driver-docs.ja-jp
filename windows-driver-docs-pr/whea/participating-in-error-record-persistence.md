---
title: エラー レコードの永続化への参加
description: エラー レコードの永続化への参加
ms.assetid: 06cbcccf-7cda-468d-aa6e-b8ecf95adf16
keywords:
- Windows ハードウェア アーキテクチャ WDK のエラー、エラー レコードの永続化
- WHEA WDK、エラー レコードの永続化
- ハードウェア エラー WDK WHEA、エラー レコードの永続化
- WDK WHEA、エラー レコードの永続化エラー
- プラットフォーム固有のハードウェア エラー ドライバー プラグインを WDK WHEA、エラー レコードの永続化
- PSHED プラグイン WDK WHEA、エラー レコードの永続化
- WDK WHEA を永続化エラー レコード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28a312a03f6b93a9f5abc4de84251ff612d0eca1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340773"
---
# <a name="participating-in-error-record-persistence"></a>エラー レコードの永続化への参加


エラー レコードの永続化に参加するには、プラグイン PSHED は次のコールバック関数を実装する必要があります。

[*WriteErrorRecord*](https://msdn.microsoft.com/library/windows/hardware/ff560678)

[*ReadErrorRecord*](https://msdn.microsoft.com/library/windows/hardware/ff559476)

[*ClearErrorRecord*](https://msdn.microsoft.com/library/windows/hardware/ff559269)

次のコード例では、これらのコールバック関数を実装する方法を示します。

```cpp
//
// The PSHED plug-in's WriteErrorRecord callback function
//
NTSTATUS
  WriteErrorRecord(
    IN OUT PVOID PluginContext,
    IN ULONG Flags,
    IN ULONG RecordLength,
    IN PWHEA_ERROR_RECORD ErrorRecord
    )
{
  // Check if dummy write operation
  if (Flags & WHEA_WRITE_FLAG_DUMMY)
  {
    return STATUS_SUCCESS;
  }

  // Write the error record to the persistent data storage
  ...

  // If successful, return success status
  if (...)
  {
    return STATUS_SUCCESS;
  }

  // Failed to write the error record
  else
  {
    return STATUS_UNSUCCESSFUL;
  }
}

//
// The PSHED plug-in's ReadErrorRecord callback function
//
NTSTATUS
  ReadErrorRecord(
    IN OUT PVOID PluginContext,
    IN ULONG Flags,
    IN ULONGLONG ErrorRecordId,
    OUT ULONGLONG NextErrorRecordId,
    IN OUT PULONG RecordLength,
    IN OUT PWHEA_ERROR_RECORD ErrorRecord
    )
{
  ULONG Length;
  PWHEA_ERROR_RECORD Record;

  // Check if an error record that matches the
  // identifier in the ErrorRecordId parameter
  // exists in the persistent data storage
  if (...)
  {
    // Retrieve the length of the specified error
    // record from the persistent data storage
    Length = ...;

    // Check if the buffer is too small to contain
    // the error record
    if (*RecordLength < Length)
    {
      // Set the RecordLength to the required length
      *RecordLength = Length;

      // Return error status
      return STATUS_BUFFER_TOO_SMALL;
    }

    // Retrieve the error record from the
    // persistent data storage and copy it
    // into the buffer pointed to by the
    // ErrorRecord parameter.
    ...

    // If successful
    if (...)
    {
      // Set RecordLength to the length of the
      // error record
      *RecordLength = Length;

      // Check if there are any other error records
      // in the persistent data storage
      if (...)
      {
        // Return the identifier of the next
        // error record
        *NextErrorRecordId = ...;
      }

      // No other error records
      else
      {
        // Return the identifier of this error record
        *NextErrorRecordId = ErrorRecordId;
      }

      // Return success status
      return STATUS_SUCCESS;
    }

    // Failed to read the error record
    else
    {
      // Return error status
      return STATUS_UNSUCCESSFUL;
    }
  }

  // The error record does not exist in the
  // persistent data storage
  else
  {
    // Return error status
    return STATUS_OBJECT_NOT_FOUND;
  }
}

//
// The PSHED plug-in's ClearErrorRecord callback function
//
NTSTATUS
  ClearErrorRecord(
    IN OUT PVOID PluginContext,
    IN ULONG Flags,
    IN ULONGLONG ErrorRecordId
    )
{
  // Clear the error record that matches the specified
  // error record identifier from the persistent data
  // storage.
  ...

  // If successful, return success status
  if (...)
  {
    return STATUS_SUCCESS;
  }

  // Failed to clear the error record
  else
  {
    return STATUS_UNSUCCESSFUL;
  }
}
```

エラー レコードの永続化に参加している PSHED プラグインを指定する必要があります、 **PshedFAErrorRecordPersistence**フラグを付けるときに、[登録](registering-a-pshed-plug-in.md)自体と、オペレーティング システムを使用します。

エラー レコードの永続化の詳細については、次を参照してください。[エラー レコードの永続化メカニズム](error-record-persistence-mechanism.md)します。

 

 




