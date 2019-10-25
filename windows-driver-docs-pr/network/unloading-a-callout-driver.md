---
title: コールアウト ドライバーのアンロード
description: コールアウト ドライバーのアンロード
ms.assetid: a8c1bb33-41f8-420c-a761-669864eb9444
keywords:
- Windows フィルタリングプラットフォームのコールアウトドライバーの WDK、アンロード
- コールアウトドライバー WDK Windows フィルタリングプラットフォーム、アンロード
- ドライバーのアンロード (WDK Windows フィルタリングプラットフォーム)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4ed875a75a53a0c4767258212f3e966ffdcdbcb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843015"
---
# <a name="unloading-a-callout-driver"></a>コールアウト ドライバーのアンロード


コールアウトドライバーをアンロードするために、オペレーティングシステムはコールアウトドライバーの unload 関数を呼び出します。 コールアウトドライバーの unload 関数を指定する方法の詳細については、「 [Unload 関数の指定](specifying-an-unload-function.md)」を参照してください。

コールアウトドライバーの unload 関数は、コールアウトドライバーがシステムメモリからアンロードされる前に、コールアウトドライバーのコールアウトがフィルターエンジンから登録解除されることを保証します。 コールアウトドライバーは、 [**FwpsCalloutUnregisterById0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutunregisterbyid0)関数または[**FwpsCalloutUnregisterByKey0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutunregisterbykey0)関数のいずれかを呼び出して、フィルターエンジンからのコールアウトを登録解除します。 コールアウトドライバーは、フィルターエンジンからのすべてのコールアウトが正常に登録解除されるまで、unload 関数から戻ることはできません。

コールアウトドライバーは、フィルターエンジンからのすべてのコールアウトを登録解除した後、そのコールアウトを最初に登録する前に、作成したデバイスオブジェクトを削除する必要があります。 Windows Driver Model (WDM) に基づくコールアウトドライバーは、 [**Iodeletedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)関数を呼び出してデバイスオブジェクトを削除します。 Windows ドライバーフレームワーク (WDF) に基づくコールアウトドライバーは、 [**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)関数を呼び出して、フレームワークデバイスオブジェクトを削除します。

また、コールアウトドライバーは、アンロード関数から制御が戻る前に、 [**FwpsInjectionHandleDestroy0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectionhandledestroy0)関数を呼び出して以前に作成したすべてのパケット挿入ハンドルを破棄する必要があります。

次に、例を示します。

```C++
// Device object
PDEVICE_OBJECT deviceObject;

// Variable for the run-time callout identifier
UINT32 CalloutId;

// Injection handle
HANDLE injectionHandle;

// Unload function
VOID
 Unload(
    IN PDRIVER_OBJECT DriverObject
    )
{
  NTSTATUS status;

  // Unregister the callout
 status =
 FwpsCalloutUnregisterById0(
 CalloutId
      );

  // Check result
 if (status == STATUS_DEVICE_BUSY)
  {
    // For each data flow that is being processed by the
    // callout that has an associated context, clean up
    // the context and then call FwpsFlowRemoveContext0
    // to remove the context from the data flow.
    ...

    // Finish unregistering the callout
 status =
 FwpsCalloutUnregisterById0(
 CalloutId
        );
  }

  // Check status
 if (status != STATUS_SUCCESS)
  {
    // Handle error
    ...
  }

  // Delete the device object
 IoDeleteDevice(
 deviceObject
    );

  // Destroy the injection handle
 status =
 FwpsInjectionHandleDestroy0(
 injectionHandle
      );

  // Check status
 if (status != STATUS_SUCCESS)
  {
    // Handle error
    ...
  }
}
```

前の例では、WDM ベースのコールアウトドライバーが想定されています。 WDF ベースのコールアウトドライバーの場合、唯一の違いは、コールアウトドライバーの unload 関数に渡されるパラメーターと、コールアウトドライバーがフレームワークデバイスオブジェクトを削除する方法です。

```C++
WDFDEVICE wdfDevice;

VOID
 Unload(
    IN WDFDRIVER Driver;
    )
{

  ...

  // Delete the framework device object
 WdfObjectDelete(
 wdfDevice
    );

  ...
}
```

 

 





