---
title: NDIS-WDF 関数に対応する関数
description: NDIS-WDF 関数に対応する関数
ms.assetid: 28C8DFA3-5602-422D-89AA-6EA05F501E15
keywords:
- NetAdapterCx の NDIS WDF 関数、対応する NetCx の NDIS WDF 関数と同等
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85d3e92388673a2eece195702a197a1227198026
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360258"
---
# <a name="ndis-wdf-function-equivalents"></a>NDIS-WDF 関数に対応する関数

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

次の表は、NDIS 関数と同等の WDF を示します。

|NDIS API ファミリ|WDF のと同じ|
|-|-|
|[**NdisAllocateIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocateioworkitem)|[**WdfWorkItemCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)|
|[**NdisAllocateTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatetimerobject)|[**WdfTimerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nf-wdftimer-wdftimercreate)|
|[**NdisAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisacquirespinlock)|[**WdfSpinLockAcquire**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))|
|[**NdisInterlockedIncrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisinterlockedincrement)|[**InterlockedIncrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-interlockedincrement)|
|[**NdisInitializeEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisinitializeevent)|[**KeInitializeEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializeevent)|
|[**NdisMInitializeScatterGatherDma**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553543(v=vs.85))|[**WdfDmaEnablerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)|
|[**NdisInitializeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisinitializestring)|[**WdfStringCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfstring/nf-wdfstring-wdfstringcreate)|
|[**NdisSystemActiveProcessorCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissystemactiveprocessorcount)|[**KeGetCurrentProcessorNumberEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-kegetcurrentprocessornumberex) (カーネル)|
|[**NdisWriteRegisterUchar**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiswriteregisteruchar)|[**WDF_WRITE_REGISTER_UCHAR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfhwaccess/nf-wdfhwaccess-wdf_write_register_uchar)|
