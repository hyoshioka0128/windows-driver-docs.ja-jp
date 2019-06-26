---
title: コールアウト ドライバーのアンロード
description: コールアウト ドライバーのアンロード
ms.assetid: a8c1bb33-41f8-420c-a761-669864eb9444
keywords:
- Windows Filtering Platform コールアウト ドライバー WDK、アンロード
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォーム、アンロード
- アンロード ドライバー WDK Windows フィルタ リング プラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 419babaf2c99b35bfb2f645317818cd4ef5fb618
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386001"
---
# <a name="unloading-a-callout-driver"></a>コールアウト ドライバーのアンロード


コールアウト ドライバーをアンロードするには、は、オペレーティング システムは、コールアウト ドライバーのアンロード関数を呼び出します。 コールアウト ドライバーのアンロード関数を指定する方法の詳細については、次を参照してください。 [、アンロード関数を指定する](specifying-an-unload-function.md)します。

コールアウト ドライバーのアンロード関数では、コールアウト ドライバーがシステム メモリからアンロードの直前には、コールアウト ドライバーのコールアウトはフィルター エンジンから登録しないことを保証します。 コールアウト ドライバーを呼び出すか、 [ **FwpsCalloutUnregisterById0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpscalloutunregisterbyid0)関数または[ **FwpsCalloutUnregisterByKey0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpscalloutunregisterbykey0)関数フィルター エンジンからの引き出し線の登録を解除します。 コールアウト ドライバーはする必要があります、フィルター エンジンからそのすべての吹き出しを登録解除が正常にした後、まで、アンロード関数から返されません。

コールアウト ドライバーは、フィルター エンジンからそのすべてのコールアウトの登録を解除、デバイスを削除する必要がありますが、最初の吹き出しを登録する前に、作成されたオブジェクトします。 Windows Driver Model (WDM) の呼び出しに基づいているコールアウト ドライバー、 [ **IoDeleteDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)デバイス オブジェクトを削除する関数。 Windows Driver Frameworks (WDF) の呼び出しに基づいているコールアウト ドライバー、 [ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete) framework デバイス オブジェクトを削除する関数。

コールアウト ドライバーをする必要がありますを呼び出して以前に作成したいずれかのパケット インジェクション ハンドルを破棄しても、 [ **FwpsInjectionHandleDestroy0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsinjectionhandledestroy0)アンロード、関数から返す前に機能します。

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

前の例は、WDM ベースのコールアウト ドライバーを想定しています。 WDF ベースのコールアウト ドライバーの場合は、唯一の違いは、コールアウト ドライバーのアンロード関数とコールアウト ドライバーが framework デバイス オブジェクトを削除する方法に渡されるパラメーターです。

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

 

 





