---
title: ホスト名と IP アドレスの解決
description: ホスト名と IP アドレスの解決
ms.assetid: 4a5f421c-6827-4ca2-be88-67ec43dc84b2
keywords:
- ネットワーク、WSK WDK 名前解決
- Winsock カーネル WDK がネットワーク、名前解決
- トランスポート アドレス WDK Winsock カーネルにホスト名の変換
- ホスト名 WDK Winsock Kernel するトランスポート アドレス変換
- トランスポート アドレス WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f654e81cc13c0666f0220edce0fdc7a8f776769
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347301"
---
# <a name="resolving-host-names-and-ip-addresses"></a>ホスト名と IP アドレスの解決


Windows 7 以降、*カーネルの名前解決*機能は、Unicode のホスト名とトランスポート アドレスの間のプロトコルに依存しない変換を実行するカーネル モード コンポーネントを使用できます。 以下を使用する[Winsock カーネル (WSK)](https://msdn.microsoft.com/library/windows/hardware/ff571083)この名前解決を実行するクライアント レベルの機能。

-   [**WskFreeAddressInfo**](https://msdn.microsoft.com/library/windows/hardware/ff571131)

-   [**WskGetAddressInfo**](https://msdn.microsoft.com/library/windows/hardware/ff571132)

-   [**WskGetNameInfo**](https://msdn.microsoft.com/library/windows/hardware/ff571134)

これらの関数と同様に、ユーザー モードの関数の名前からアドレス変換を実行する[ **FreeAddrInfoW**](https://msdn.microsoft.com/library/windows/desktop/ms737912)、 [ **GetAddrInfoW**](https://msdn.microsoft.com/library/windows/desktop/ms738519)、[ **GetNameInfoW**](https://msdn.microsoft.com/library/windows/desktop/ms738531)、それぞれします。

この機能を利用するには、コンパイルまたは、NTDDI にドライバーを再コンパイルする必要があります\_バージョン マクロ設定 NTDDI\_WIN7 以上。

次の呼び出しシーケンスを実行すると、ドライバーのカーネルの名前解決機能を使用するためがあります。

1.  呼び出す[ **WskRegister** ](https://msdn.microsoft.com/library/windows/hardware/ff571143) WSK に登録します。

2.  呼び出す[ **WskCaptureProviderNPI** ](https://msdn.microsoft.com/library/windows/hardware/ff571122) WSK プロバイダーをキャプチャする[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)します。

3.  完了したら NPI WSK プロバイダーを使用して、呼び出す[ **WskReleaseProviderNPI** ](https://msdn.microsoft.com/library/windows/hardware/ff571145)解放 WSK プロバイダー NPI します。

4.  呼び出す[ **WskDeregister** ](https://msdn.microsoft.com/library/windows/hardware/ff571128) WSK アプリケーションの登録を解除します。

次のコード例は、WSK アプリケーションを呼び出す方法を表示する上記の呼び出しの順序を使用して、 **WskGetAddressInfo**トランスポート アドレスのホスト名を変換する関数。

```C++
NTSTATUS
SyncIrpCompletionRoutine(
    __in PDEVICE_OBJECT Reserved,
    __in PIRP Irp,
    __in PVOID Context
    )
{    
    PKEVENT compEvent = (PKEVENT)Context;
    UNREFERENCED_PARAMETER(Reserved);
    UNREFERENCED_PARAMETER(Irp);
    KeSetEvent(compEvent, 2, FALSE);    
    return STATUS_MORE_PROCESSING_REQUIRED;
}

NTSTATUS
KernelNameResolutionSample(
    __in PCWSTR NodeName,
    __in_opt PCWSTR ServiceName,
    __in_opt PADDRINFOEXW Hints,
    __in PWSK_PROVIDER_NPI WskProviderNpi
    )
{
    NTSTATUS status;
    PIRP irp;
    KEVENT completionEvent;
    UNICODE_STRING uniNodeName, uniServiceName, *uniServiceNamePtr;
    PADDRINFOEXW results;

    PAGED_CODE();
    //
    // Initialize UNICODE_STRING structures for NodeName and ServiceName 
    //
 
    RtlInitUnicodeString(&uniNodeName, NodeName);

    if(ServiceName == NULL) {
        uniServiceNamePtr = NULL;
    }
    else {
        RtlInitUnicodeString(&uniServiceName, ServiceName);
        uniServiceNamePtr = &uniServiceName;
    }

    //
    // Use an event object to synchronously wait for the 
    // WskGetAddressInfo request to be completed. 
    //
 
    KeInitializeEvent(&completionEvent, SynchronizationEvent, FALSE);

    //
    // Allocate an IRP for the WskGetAddressInfo request, and set the 
    // IRP completion routine, which will signal the completionEvent
    // when the request is completed.
    //
 
    irp = IoAllocateIrp(1, FALSE);
    if(irp == NULL) {
        return STATUS_INSUFFICIENT_RESOURCES;
    }        

    IoSetCompletionRoutine(irp, SyncIrpCompletionRoutine, 
  &completionEvent, TRUE, TRUE, TRUE);

    //
    // Make the WskGetAddressInfo request.
    //
 
    WskProviderNpi->Dispatch->WskGetAddressInfo (
        WskProviderNpi->Client,
        &uniNodeName,
        uniServiceNamePtr,
        NS_ALL,
        NULL, // Provider
        Hints,
        &results, 
        NULL, // OwningProcess
        NULL, // OwningThread
        irp);

    //
    // Wait for completion. Note that processing of name resolution results
    // can also be handled directly within the IRP completion routine, but
    // for simplicity, this example shows how to wait synchronously for 
    // completion.
    //
 
    KeWaitForSingleObject(&completionEvent, Executive, 
                        KernelMode, FALSE, NULL);

    status = irp->IoStatus.Status;

    IoFreeIrp(irp);

    if(!NT_SUCCESS(status)) {
        return status;
    }

    //
    // Process the name resolution results by iterating through the addresses
    // within the returned ADDRINFOEXW structure.
    //
 
   results; // your code here

    //
    // Release the returned ADDRINFOEXW structure when no longer needed.
    //
 
    WskProviderNpi->Dispatch->WskFreeAddressInfo(
        WskProviderNpi->Client,
        results);

    return status;
} 
```

 

 





