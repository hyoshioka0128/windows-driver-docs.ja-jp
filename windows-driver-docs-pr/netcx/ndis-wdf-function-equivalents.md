---
title: NDIS-WDF 関数に対応する関数
description: NDIS-WDF 関数に対応する関数
ms.assetid: 28C8DFA3-5602-422D-89AA-6EA05F501E15
keywords:
- NetAdapterCx WDF 関数に相当する、NetCx NDIS-WDF 関数と同等の機能
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73af2e05a8440c9d6d582d61a3bdc03519b044c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835528"
---
# <a name="ndis-wdf-function-equivalents"></a>NDIS-WDF 関数に対応する関数

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

次の表に、NDIS 関数とそれに相当する WDF を示します。

|NDIS API ファミリ|同等の WDF|
|-|-|
|[**NdisAllocateIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem)|[**WdfWorkItemCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)|
|[**NdisAllocateTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatetimerobject)|[**WdfTimerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimercreate)|
|[**NdisAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirespinlock)|[**WdfSpinLockAcquire**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))|
|[**NdisInterlockedIncrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinterlockedincrement)|[**InterlockedIncrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedincrement)|
|[**NdisInitializeEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializeevent)|[**KeInitializeEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeevent)|
|[**NdisMInitializeScatterGatherDma**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553543(v=vs.85))|[**WdfDmaEnablerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)|
|[**NdisInitializeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializestring)|[**WdfStringCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfstring/nf-wdfstring-wdfstringcreate)|
|[**NdisSystemActiveProcessorCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissystemactiveprocessorcount)|[**Kegetcurrentprocessornumber ex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kegetcurrentprocessornumberex) (カーネル)|
|[**NdisWriteRegisterUchar**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswriteregisteruchar)|[**WDF_WRITE_REGISTER_UCHAR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfhwaccess/nf-wdfhwaccess-wdf_write_register_uchar)|
