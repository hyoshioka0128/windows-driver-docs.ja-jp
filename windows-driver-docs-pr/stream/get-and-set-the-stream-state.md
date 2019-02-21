---
title: 取得し、Stream の状態を設定
description: 取得し、Stream の状態を設定
ms.assetid: e2fde528-d0cf-4ffe-945a-8672b76db61f
keywords:
- フィルター ドライバー WDK Avcstrm.sys ストリーミング ストリームを状態します。
- ストリーム状態 WDK AV/C ストリーミング
- WDK AV/C ストリーミングの状態します。
- KSSTATE_STOP
- KSSTATE_ACQUIRE
- KSSTATE_PAUSE
- KSSTATE_RUN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 914adb45fbc1fbcc7564abad60c63adb49a403f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530112"
---
# <a name="get-and-set-the-stream-state"></a>取得し、Stream の状態を設定





サブユニットは、ストリームの現在の状態を取得する、または新しいストリームの状態を設定するのには、クライアント アプリケーションからの Ioctl を受信します。 データ ストリームが作成されるときに初期化される、 **KSSTATE\_停止**状態。 アイソクロナス リソースの割り当て、 **KSSTATE\_ACQUIRE**状態、および失敗した場合、状態が返されます\_不十分\_リソース (で宣言されている*Ntstatus.h。*)**KSSTATE\_一時停止**状態。 データのストリーミングが開始、 **KSSTATE\_実行**状態。

次のコード サンプルでは、ストリームを新しい状態に設定します。

```cpp
INIT_AVCSTRM_HEADER(pAVCStrmReq, AVCSTRM_SET_STATE);
pAVCStrmReq->AVCStreamContext = pStrmExt->AVCStreamContext; //  From cached context saved in OPEN_STREAM request
pAVCStrmReq->CommandData.StreamState = StreamState; // New stream state

Status = 
    AVCStrmReqSubmitIrpSynch( 
        pDevExt->pBusDeviceObject,
        pStrmExt->pIrpReq,
        pAVCStrmReq
        );
```

現在のストリームの状態を次のコード サンプル クエリ:

```cpp
INIT_AVCSTRM_HEADER(pAVCStrmReq, AVCSTRM_GET_STATE);
pAVCStrmReq->AVCStreamContext = pStrmExt->AVCStreamContext;  // From cached context saved in OPEN_STREAM request

Status = 
    AVCStrmReqSubmitIrpSynch( 
        DeviceObject,
        pStrmExt->pIrpReq,
        pAVCStrmReq
        );

// If return STATUS_SUCCESS, the current stream state is in
// pAVCStrmReq->CommandData.StreamState 
```

 

 




