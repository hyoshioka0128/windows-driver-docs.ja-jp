---
title: Stream を作成します。
description: Stream を作成します。
ms.assetid: 9984275f-7ead-4df2-aa98-a3b4e5e85ae0
keywords:
- Avcstrm.sys フィルター ドライバー WDK のストリーミング、ストリームを作成します。
- 作成 C/WDK AV ストリーミングをストリーミングします。
- C/WDK AV ストリーミングのコンテキスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e465d05ce37b2c9e15efe02d589a04983eae3d8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539209"
---
# <a name="create-a-stream"></a>Stream を作成します。





AV/C ストリーミング フィルター ドライバーで、前にデータのストリーム コンテキストを作成する必要があります*Avcstrm.sys*サービスを提供することができます。 コンテキストは、要求されたデータ形式、データ ストリームの状態、およびストリームの拡張機能のようなプロパティを含む非透過構造体を指します。 データ形式の構造とデータ フローの方向は、その入力パラメーターが。 ストリームを正常に作成できる場合は、ストリーム コンテキストを返します。 このコンテキストでは、サブユニット ドライバーによってキャッシュされ、AV/C ストリーミングの後続の要求のために使用します。

これは、同期操作です。 操作は、最初のストリームを開くストリーム要求の構造を作成します。 ユーザー定義 IRP 同期ルーチンを呼び出す特定のデータ フローの方向とで定義されているデータ形式に基づいているデータ ストリームを作成する下位のドライバーを呼び出して[ **AVCSTRM\_形式\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff554117). 次のコード サンプルでは、データのストリーム コンテキストを開く方法を示します。

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

 

 




