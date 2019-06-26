---
title: ストリームの中止
description: ストリームの中止
ms.assetid: 46c726b6-8553-4588-9be1-2cf7779efec5
keywords:
- Avcstrm.sys フィルター ドライバー WDK のストリーミング、ストリームを中止しています
- ストリーム C/WDK AV ストリーミングを中止します。
- C/WDK AV ストリーミングのストリーミングを停止します。
- WDK AV/C ストリーミング ストリームを中止します。
- ストリームのキャンセル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe10de891ab4c5c18429655c53a93ad440d82d4b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386781"
---
# <a name="abort-a-stream"></a>ストリームの中止





サブユニットは、ストリーム データ IOCTL キャンセルの場合は、デバイスの削除などの特別な条件を検出すると、ストリーミングの操作が中断されます。 中止操作*要求*は、同期ですが中止完了ではありません。 最初の中止のストリーム要求のみが受け入れられたり、処理されます。重複する要求が無視されますが、状態と共に返される\_成功します。 AV/C ストリーミング フィルター ドライバー、 *Avcstrm.sys、* ストリーミングを中止する作業項目のスケジュールを設定します。 完了する開始ストリームが中止されたときに、 [ **AVCSTRM\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/stream/avcstrm-read)/[**AVCSTRM\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/stream/avcstrm-write)状態要求\_キャンセルします。 中止要求では、ストリームの状態は変更されませんし、データ ストリームも閉じる必要がありますをクリーンアップして、リソースを解放します。

中止作業項目のルーチンで AV/C ストリーミング isochronous データ転送を停止最初しますが、ストリームの状態は影響しません。 接続されているストリームのデータ キューをストリーム バッファーをデタッチ状態に戻すを通過 AV/C をストリーミングし\_キャンセルします。

この要求を発行する/C AV ストリーミングの要求はで初期化、 **AVCSTRM\_中止\_ストリーミング**要求とデータのストリーム コンテキスト。

```cpp
INIT_AVCSTRM_HEADER(pAVCStrmReq, AVCSTRM_ABORT_STREAMING);
pAVCStrmReq->AVCStreamContext = pStrmExt->AVCStreamContext;  // From cached context saved in OPEN_STREAM request

Status = 
    AVCStrmReqSubmitIrpSynch( 
        pStrmExt->pDevExt->pBusDeviceObject,
        pStrmExt->pIrpAbort,
        pAVCStrmReq
        );
```

データ ストリームが中止されたときにその後に再開できます (デバイスが削除されていない) 場合に、ストリームの状態がリセットされました**KSSTATE\_停止**そのクライアント アプリケーションでします。

 

 




