---
title: 記憶域クラス ドライバーの SplitTransferRequest ルーチン
description: 記憶域クラス ドライバーの SplitTransferRequest ルーチン
ms.assetid: 4f449d3b-9a0a-4ff9-a7fb-bfa21b8a56c0
keywords:
- SplitTransferRequest
- WDK の記憶域を連続していないページ
- 分割の転送要求
- 譲渡要求は WDK ストレージの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bfe1b3a3c36c55b8119b0e0a841454c8f96496c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339010"
---
# <a name="storage-class-drivers-splittransferrequest-routine"></a>記憶域クラス ドライバーの SplitTransferRequest ルーチン


## <span id="ddk_storage_class_drivers_splittransferrequest_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_SPLITTRANSFERREQUEST_ROUTINE_KG"></span>


記憶域\_アダプター\_に返されるデータの記述子、*いる出力*ルーチンをクラス ドライバーを特定の HBA の転送機能を示します。 具体的には、このデータを示します、 **MaximumTransferLength** (バイト単位) と**MaximumPhysicalPages**: は、非連続のページ数、HBA で管理できる、システムのバックアップの物理メモリバッファー (つまり、スキャッター/ギャザーのサポートのエクステント)。

ほとんどのクラス ドライバーでは、記憶域クラス ドライバーはデータを転送する HBA の機能を超えるすべての転送要求を分割するために各デバイス オブジェクトの拡張機能でデバイスこの構成データへのポインターを格納します。 つまり、クラス ドライバーの[ **DispatchReadWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンが各 IRP が HBA が 1 つの転送操作で処理できるよりも多くの転送を要求するかどうかを特定する必要があります。

たとえば、このような*DispatchReadWrite*ルーチンは、次のようなコードがある可能性があります。

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

クラス ドライバーは、バッファーは、その転送には、各ページは連続していないし、許可されている物理的な改行の数と、ページの数を比較が想定する必要がありますのでしたら、それがマップされている必要がどのように多くの物理区切りを見分けることはできません。

このようなドライバーに注意してください*DispatchReadWrite*ルーチンの呼び出し**IoMarkIrpPending**ステータスを返す\_への呼び出し後すぐに保留その*SplitTransferRequest*元 IRP ルーチン。

ドライバーの元の転送要求を実行するために*SplitTransferRequest*ルーチンに HBA の機能に合わせて大きさを subbuffers を処理するために 1 つまたは複数の Irp を作成します。 このような IRP の*SplitTransferRequest*ルーチン。

-   内部で呼び出すことによって、通常、SRB を設定*BuildRequest*ルーチン (を参照してください[記憶域クラス ドライバー BuildRequest ルーチン](storage-class-driver-s-buildrequest-routine.md))

-   MDL のコピーが新しい IRP を元の IRP からアドレスします。

-   セット、 **DataBuffer**転送のこの部分の MDL にバイトのオフセットに SRB で

-   設定その*IoCompletion*ポート ドライバーに IRP を送信する前に日常的な[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)

転送の各部分を追跡するために*SplitTransferRequest*登録、 *IoCompletion*下ドライバーに送信する各ドライバーに割り当てられた IRP の日常的な。 *IoCompletion*ルーチンでは、元の IRP では、部分的な転送が完了した要求の数を保持するを使用して**InterlockedIncrement**と**InterlockedDecrement**に数が正確であることを確認します。

このような*IoCompletion*れた Irp とされる Srb ドライバーが割り当てられているし、すべての要求されたデータが転送されたとき、またはクラス ドライバーは IRP の再試行回数が不足し、失敗する必要があります、元の IRP を完了する必要がありますルーチンを解放する必要がありますデバイスの転送エラーのためにします。

 

 




