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
ms.openlocfilehash: a28d1ca7dc86a575658eec00125f8a0bfd2df826
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378647"
---
# <a name="resolving-host-names-and-ip-addresses"></a>ホスト名と IP アドレスの解決


Windows 7 以降、*カーネルの名前解決*機能は、Unicode のホスト名とトランスポート アドレスの間のプロトコルに依存しない変換を実行するカーネル モード コンポーネントを使用できます。 以下を使用する[Winsock カーネル (WSK)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)この名前解決を実行するクライアント レベルの機能。

-   [**WskFreeAddressInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_free_address_info)

-   [**WskGetAddressInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_get_address_info)

-   [**WskGetNameInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_get_name_info)

これらの関数と同様に、ユーザー モードの関数の名前からアドレス変換を実行する[ **FreeAddrInfoW**](https://docs.microsoft.com/windows/desktop/api/ws2tcpip/nf-ws2tcpip-freeaddrinfow)、 [ **GetAddrInfoW**](https://docs.microsoft.com/windows/desktop/api/ws2tcpip/nf-ws2tcpip-getaddrinfow)、[ **GetNameInfoW**](https://docs.microsoft.com/windows/desktop/api/ws2tcpip/nf-ws2tcpip-getnameinfow)、それぞれします。

この機能を利用するには、コンパイルまたは、NTDDI にドライバーを再コンパイルする必要があります\_バージョン マクロ設定 NTDDI\_WIN7 以上。

次の呼び出しシーケンスを実行すると、ドライバーのカーネルの名前解決機能を使用するためがあります。

1.  呼び出す[ **WskRegister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskregister) WSK に登録します。

2.  呼び出す[ **WskCaptureProviderNPI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskcaptureprovidernpi) WSK プロバイダーをキャプチャする[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)します。

3.  完了したら NPI WSK プロバイダーを使用して、呼び出す[ **WskReleaseProviderNPI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskreleaseprovidernpi)解放 WSK プロバイダー NPI します。

4.  呼び出す[ **WskDeregister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskderegister) WSK アプリケーションの登録を解除します。

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

 

 





