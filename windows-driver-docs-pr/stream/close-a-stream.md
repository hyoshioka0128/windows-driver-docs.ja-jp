---
title: ストリームを閉じる
description: ストリームを閉じる
ms.assetid: 1ed9b07c-8d22-485f-a7e8-3a27ca3768b0
keywords:
- Avcstrm.sys フィルター ドライバー WDK のストリーミング、ストリームを閉じる
- ストリームの WDK AV/C のストリーミングを閉じる
- ストリームを閉じる
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6713a9e053d918b2569663ac7b0e9ae24b8e9ff3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372361"
---
# <a name="close-a-stream"></a>ストリームを閉じる

ストリームの処理が完了すると、ストリームを開く要求によって割り当てられたリソースを解放するデータ ストリームを閉じる必要があります。

場合、ストリーム*状態*が停止されていない保留中の I/O があるか、ストリームを閉じる要求は、データの要求を完了し、状態に IRP の状態を設定\_キャンセルします。

```cpp
INIT_AVCSTRM_HEADER(pAVCStrmReq, AVCSTRM_CLOSE);
pAVCStrmReq->AVCStreamContext = pStrmExt->AVCStreamContext;  // From cached context saved in OPEN_STREAM request
Status = 
    AVCStrmReqSubmitIrpSynch( 
        pDevExt->pBusDeviceObject,
        pStrmExt->pIrpReq,
        pAVCStrmReq
        );
```
