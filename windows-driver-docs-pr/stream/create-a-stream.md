---
title: ストリームの作成
description: ストリームの作成
ms.assetid: 9984275f-7ead-4df2-aa98-a3b4e5e85ae0
keywords:
- Avcstrm .sys ストリーミングフィルタードライバー WDK、ストリームの作成
- stream 作成 WDK AV/C streaming
- コンテキスト WDK AV/C ストリーミング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3191e828bda2a6a26a0ea11c1e590d586ae4058
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827126"
---
# <a name="create-a-stream"></a>ストリームの作成





データストリームコンテキストは、AV/C ストリーミングフィルタードライバー ( *Avcstrm .sys*) がサービスを提供する前に作成する必要があります。 コンテキストは、ストリーム拡張と同様に、要求されたデータ形式、データストリームの状態、およびプロパティを含む不透明な構造体を指します。 データ形式の構造とデータフローの方向は、入力パラメーターです。 ストリームを正常に作成できる場合は、ストリームコンテキストが返されます。 このコンテキストは、サブユニットドライバーによってキャッシュされ、後続の AV/C ストリーミング要求に使用されます。

これは同期操作です。 操作は、ストリームを開くためのストリーム要求構造を最初に作成します。 次に、ユーザー定義の IRP 同期ルーチンを呼び出して下位ドライバーを呼び出し、 [**Avcstrm\_形式\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avcstrm_format_info)で定義されているデータフローの方向とデータ形式に基づいてデータストリームを作成します。 次のコードサンプルは、データストリームコンテキストを開く方法を示しています。

```cpp
#include <avcstrm.h>

INIT_AVCSTRM_HEADER(pAVCStrmReq, AVCSTRM_OPEN);
pAVCStrmReq->CommandData.OpenStruct.AVCFormatInfo =            &AVCStrmFormatInfoTable[pDevExt->VideoFormatIndex]; 
pAVCStrmReq->CommandData.OpenStruct.AVCStreamContext = NULL;
pAVCStrmReq->CommandData.OpenStruct.DataFlow         = DataFlow;

Status = 
    AVCStrmReqSubmitIrpSynch( 
        pDevExt->pBusDeviceObject,
        pStrmExt->pIrpReq,
        pAVCStrmReq
        );

if(STATUS_SUCCESS == Status) {
    // Save the context, which is used for a 
    // Subsequent call to the AVCStrm filter driver    
    pStrmExt->AVCStreamContext = 
        pAVCStrmReq->CommandData.OpenStruct.AVCStreamContext;
}
```

 

 




