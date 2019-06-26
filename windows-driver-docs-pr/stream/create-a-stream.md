---
title: ストリームの作成
description: ストリームの作成
ms.assetid: 9984275f-7ead-4df2-aa98-a3b4e5e85ae0
keywords:
- Avcstrm.sys フィルター ドライバー WDK のストリーミング、ストリームを作成します。
- 作成 C/WDK AV ストリーミングをストリーミングします。
- C/WDK AV ストリーミングのコンテキスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88034e603e687d16be8ddf832c2272e7968c8b44
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378392"
---
# <a name="create-a-stream"></a>ストリームの作成





AV/C ストリーミング フィルター ドライバーで、前にデータのストリーム コンテキストを作成する必要があります*Avcstrm.sys*サービスを提供することができます。 コンテキストは、要求されたデータ形式、データ ストリームの状態、およびストリームの拡張機能のようなプロパティを含む非透過構造体を指します。 データ形式の構造とデータ フローの方向は、その入力パラメーターが。 ストリームを正常に作成できる場合は、ストリーム コンテキストを返します。 このコンテキストでは、サブユニット ドライバーによってキャッシュされ、AV/C ストリーミングの後続の要求のために使用します。

これは、同期操作です。 操作は、最初のストリームを開くストリーム要求の構造を作成します。 ユーザー定義 IRP 同期ルーチンを呼び出す特定のデータ フローの方向とで定義されているデータ形式に基づいているデータ ストリームを作成する下位のドライバーを呼び出して[ **AVCSTRM\_形式\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/ns-avcstrm-_avcstrm_format_info). 次のコード サンプルでは、データのストリーム コンテキストを開く方法を示します。

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

 

 




