---
title: ホスト名と IP アドレスの解決
description: ホスト名と IP アドレスの解決
ms.assetid: 4a5f421c-6827-4ca2-be88-67ec43dc84b2
keywords:
- WSK WDK ネットワーク、名前解決
- Winsock カーネル WDK ネットワーク、名前解決
- トランスポートアドレス WDK Winsock カーネルへのホスト名の変換
- ホスト名に対するトランスポートアドレスの変換 WDK Winsock カーネル
- トランスポートアドレス WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42fa3ef01bc4cf211708c6287b34dfc3c4dea0ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842022"
---
# <a name="resolving-host-names-and-ip-addresses"></a>ホスト名と IP アドレスの解決


Windows 7 以降では、カーネルの*名前解決*機能により、カーネルモードのコンポーネントは、Unicode ホスト名とトランスポートアドレスの間でプロトコルに依存しない変換を実行できるようになります。 この名前解決を実行するには、次の[Winsock カーネル (WSK)](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)クライアントレベル関数を使用します。

-   [**WskFreeAddressInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_free_address_info)

-   [**WskGetAddressInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_get_address_info)

-   [**WskGetNameInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_get_name_info)

これらの関数は、ユーザーモード関数[**Freeaddrinfow**](https://docs.microsoft.com/windows/desktop/api/ws2tcpip/nf-ws2tcpip-freeaddrinfow)、 [**GetAddrInfoW**](https://docs.microsoft.com/windows/desktop/api/ws2tcpip/nf-ws2tcpip-getaddrinfow)、および[**getnameinfow**](https://docs.microsoft.com/windows/desktop/api/ws2tcpip/nf-ws2tcpip-getnameinfow)と同様に、名前とアドレスの変換を実行します。

この機能を利用するには、NTDDI\_VERSION マクロを NTDDI\_WIN7 以上に設定して、ドライバーをコンパイルまたは再コンパイルする必要があります。

ドライバーでカーネルの名前解決機能を使用するには、次の呼び出しシーケンスを実行する必要があります。

1.  WSK に登録するには、 [**Wskregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister)を呼び出します。

2.  [**WskCaptureProviderNPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskcaptureprovidernpi)を呼び出して、wsk プロバイダーの[ネットワークプログラミングインターフェイス (NPI)](network-programming-interface.md)をキャプチャします。

3.  WSK プロバイダー NPI の使用が完了したら、 [**WskReleaseProviderNPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskreleaseprovidernpi)を呼び出して WSK プロバイダー NPI を解放します。

4.  [**Wskderegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskderegister)を呼び出して wsk アプリケーションを登録解除します。

次のコード例では、上記の呼び出しシーケンスを使用して、WSK アプリケーションが**Wskgetaddressinfo**関数を呼び出してホスト名をトランスポートアドレスに変換する方法を示しています。

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

 

 





