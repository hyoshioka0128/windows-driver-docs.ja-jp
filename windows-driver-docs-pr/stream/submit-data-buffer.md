---
title: データ バッファーの送信
description: データ バッファーの送信
ms.assetid: 151f5139-3706-4255-9d71-d8e6e3416b7c
keywords:
- Avcstrm.sys ストリーミング フィルター ドライバー WDK、データ バッファーの送信
- データ バッファーの WDK AV/C ストリーミング
- データ バッファーの C/WDK AV ストリーミングの送信
- バッファーの WDK AV/C ストリーミング
- 保留中のストリーム C/WDK AV ストリーミング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9da43ed6acf278b3ce8ee402e75f0b2206fb3c89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390866"
---
# <a name="submit-data-buffer"></a>データ バッファーの送信





ストリームを開くには、サブユニット ドライバーは AV/C ストリーミング ストリームのサンプルをアタッチを開始できます。 同様に、AV/C ストリーミング フィルター ドライバーに送信できるか、読み取り可能または書き込みがこれらのサンプルと*Avcstrm.sys*します。 このサービスは、現在のストリームの状態とストリーム データの可用性に依存しているため常に非同期です。

```cpp
INIT_AVCSTRM_HEADER(pAVCStrmReq, (pSrb->Command == SRB_READ_DATA) ?      <mark type="enumval">AVCSTRM_READ</mark> : AVCSTRM_WRITE);
pAVCStrmReq->AVCStreamContext = pStrmExt->AVCStreamContext;  // from cached context saved in OPEN_STREAM request

// Avcstrm.sys does not act as a clock provider. The subunit driver must provide this functionality if it wants to be the clock provider.

pAVCStrmReq->CommandData.BufferStruct.StreamHeader = pSrb->CommandData.DataBufferArray;

pAVCStrmReq->CommandData.BufferStruct.FrameBuffer =             
MmGetSystemAddressForMdlSafe(pSrb->Irp->MdlAddress,          NormalPagePriority);

// This is an asynchronous operation
NextIrpStack = IoGetNextIrpStackLocation(pIrpReq);
NextIrpStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;
NextIrpStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_AVCSTRM_CLASS;
NextIrpStack->Parameters.Others.Argument1 = pAVCStrmReq;

// Cannot be canceled! Use <mark type="enumval">AVCSTRM_ABORT_STREAMING</mark> to abort
IoSetCancelRoutine(
    pIrpReq,
    NULL
    );

IoSetCompletionRoutine( 
    pIrpReq,
    AVCTapeReqReadDataCR,
    pDriverReq,
    TRUE,  // Success
    TRUE,  // Error
    TRUE   // or Cancel
    );

pSrb->Status = STATUS_PENDING;

Status = 
    IoCallDriver(
        pDevExt->pBusDeviceObject,
        pIrpReq
        );
```

状態が状態には、操作は非同期であるため\_保留します。 データが完了したら、完了ルーチンが呼び出されます。 完了のルーチンで、サブユニット ドライバーが行えるポスト プロセスや処理されるデータの統計の更新を含む可能性があります、サブユニットがプロバイダーの場合、クロックのプレゼンテーション時間を追加します。

```cpp
// Keep track of the number of frames processed
pStrmExt->FramesProcessed++;

// Retrieve current stream time
if(pStrmExt->hMasterClock) 
    pStrmExt->CurrentStreamTime = pSrb->CommandData.DataBufferArray->PresentationTime.Time;

// Update final status
pSrb->Status = pIrpReq->IoStatus.Status;

// Complete this data SRB
StreamClassStreamNotification( 
    StreamRequestComplete,
    pSrb->StreamObject,
    pSrb 
    );
```
