---
title: Stream を中止します。
description: Stream を中止します。
ms.assetid: 46c726b6-8553-4588-9be1-2cf7779efec5
keywords:
- Avcstrm.sys フィルター ドライバー WDK のストリーミング、ストリームを中止しています
- ストリーム C/WDK AV ストリーミングを中止します。
- C/WDK AV ストリーミングのストリーミングを停止します。
- WDK AV/C ストリーミング ストリームを中止します。
- ストリームのキャンセル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48ec5181a900d67261bb34f235729d5d1f2bee4c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551204"
---
# <a name="abort-a-stream"></a>Stream を中止します。





サブユニットは、ストリーム データ IOCTL キャンセルの場合は、デバイスの削除などの特別な条件を検出すると、ストリーミングの操作が中断されます。 中止操作*要求*は、同期ですが中止完了ではありません。 最初の中止のストリーム要求のみが受け入れられたり、処理されます。重複する要求が無視されますが、状態と共に返される\_成功します。 AV/C ストリーミング フィルター ドライバー、 *Avcstrm.sys、* ストリーミングを中止する作業項目のスケジュールを設定します。 完了する開始ストリームが中止されたときに、 [ **AVCSTRM\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff554130)/[**AVCSTRM\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff554135)状態要求\_キャンセルします。 中止要求では、ストリームの状態は変更されませんし、データ ストリームも閉じる必要がありますをクリーンアップして、リソースを解放します。

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

 

 




