---
title: 記憶域クラス ドライバーの SplitTransferRequest ルーチン
description: 記憶域クラス ドライバーの SplitTransferRequest ルーチン
ms.assetid: 4f449d3b-9a0a-4ff9-a7fb-bfa21b8a56c0
keywords:
- SplitTransferRequest
- 非連続ページ WDK storage
- 転送要求の分割
- 転送要求の分割 WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3420d968d87a9822cb1c8bd377a17f839e80d81d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841606"
---
# <a name="storage-class-drivers-splittransferrequest-routine"></a>記憶域クラス ドライバーの SplitTransferRequest ルーチン


## <span id="ddk_storage_class_drivers_splittransferrequest_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_SPLITTRANSFERREQUEST_ROUTINE_KG"></span>


*Getdescriptor*ルーチンに返されるストレージ\_アダプター\_記述子データは、特定の HBA のクラスドライバーへの転送機能を示します。 具体的には、このデータは **、システム**バッファーをバッキングする物理メモリ内で HBA が管理できる連続したページの数 (バイト数) と**maximumtransferlength**(たとえば、散布図/の範囲) を示します。収集のサポート)。

ほとんどのクラスドライバーは、この構成データへのポインターを各デバイスオブジェクトのデバイス拡張に格納します。これは、記憶域クラスドライバーが、データ転送のために HBA の機能を超えるすべての転送要求を分割するためです。 言い換えると、クラスドライバーの[**DispatchReadWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、各 IRP が1回の転送操作で処理できるよりも多くの転送を要求するかどうかを判断する必要があります。

たとえば、このような*DispatchReadWrite*ルーチンは、次のようなコードを持つことができます。

```cpp
PSTORAGE_ADAPTER_DESCRIPTOR adapterDescriptor = 
    commonExtension->PartitionZeroExtension->AdapterDescriptor;
ULONG transferPages;
ULONG maximumTransferLength = 
    adapterDescriptor->MaximumTransferLength;
    :        : 
// 
// Calculate number of pages in this transfer 
// 
transferPages = ADDRESS_AND_SIZE_TO_SPAN_PAGES( 
                    MmGetMdlVirtualAddress(Irp->MdlAddress), 
                        currentIrpStack->Parameters.Read.Length);
// 
// Check whether requested length is greater than the maximum number 
// of bytes that can be transferred in a single operation 
// 
if (currentIrpStack->Parameters.Read.Length > maximumTransferLength ||
        transferPages > adapterDescriptor->MaximumPhysicalPages) { 
    transferPages = adapterDescriptor->MaximumPhysicalPages - 1;
    if (maximumTransferLength > transferPages << PAGE_SHIFT) { 
        maximumTransferLength = transferPages << PAGE_SHIFT; 
    } 
    IoMarkIrpPending(Irp); 
    SplitTransferRequest(DeviceObject, 
                            Irp, 
                            maximumTransferLength); 
    return STATUS_PENDING; 
} 
    :        : 
```

クラスドライバーは、バッファーが割り当てられた後の物理中断の数を判断できません。そのため、転送の各ページが連続していないと想定し、ページ数と、許可されている物理中断の数を比較する必要があります。

このようなドライバーの*DispatchReadWrite*ルーチンは**Iomarkirppending**を呼び出し、元の IRP との*splittransferrequest*ルーチンの呼び出しの直後に、ステータス\_を返します。

元の転送要求を実行するために、ドライバーの*Splittransferrequest*ルーチンは、HBA の機能に合わせてサイズが設定されたサブバッファーを処理する1つ以上の irp を作成します。 このような IRP の場合、 *Splittransferrequest*ルーチンは次のようになります。

-   SRB を設定します。通常は内部*Buildrequest*ルーチンを呼び出します (「[ストレージクラスドライバーの buildrequest ルーチン](storage-class-driver-s-buildrequest-routine.md)」を参照してください)。

-   元の IRP の MDL アドレスを新しい IRP にコピーします。

-   この転送のために、SRB の**DataBuffer**をバイト単位のオフセットに設定します。

-   [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)で IRP をポートドライバーに送信する前に、その*iocompletion*ルーチンを設定します。

転送の各部分を追跡するために、 *Splittransferrequest*は、ドライバーによって割り当てられた各 IRP に対して、次の下位のドライバーに送信する*iocompletion*ルーチンを登録します。 *Iocompletion*ルーチンは、 **InterlockedIncrement**と**InterlockedDecrement**を使用して、カウントが正確であることを確認するために、元の IRP で完了した部分転送要求の数を保持します。

このような*Iocompletion*ルーチンでは、ドライバーが割り当てたすべての Irp や SRBs を解放する必要があります。また、要求されたすべてのデータが転送されたとき、またはクラスドライバーが irp の再試行を終了し、デバイスのために失敗する必要がある場合は、元の irp を完了する必要があります。転送エラー。

 

 




