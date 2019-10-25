---
title: オフロードされたオーディオに関するグリッチ レポート
description: このトピックでは、ハードウェアオフロードオーディオストリームとの接続で glitching エラーを報告する必要がある場合に、オーディオドライバーが使用する必要があるメカニズムについて説明します。
ms.assetid: 9FF2A5D6-9382-4EE6-AA21-DCF47210F73B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afe634775051d8207ed442aef964ecb4fe0bc952
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833363"
---
# <a name="glitch-reporting-for-offloaded-audio"></a>オフロードされたオーディオに関するグリッチ レポート


このトピックでは、ハードウェアオフロードオーディオストリームとの接続で glitching エラーを報告する必要がある場合に、オーディオドライバーが使用する必要があるメカニズムについて説明します。

オーディオドライバーは、glitching エラーを検出すると、エラーを報告するために Windows イベントトレーシング (ETW) イベントを発生させる必要があります。 このイベントには、エラーの理由、およびオーディオストリームで使用されている DMA バッファーに関する情報が含まれている必要があります。

次の列挙は、エラー報告に使用するオーディオドライバーに対して定義されているイベントを示しています。

```ManagedCPlusPlus
typedef enum 
{
    eMINIPORT_IHV_DEFINED = 0, 
    eMINIPORT_BUFFER_COMPLETE,
    eMINIPORT_PIN_STATE,
    eMINIPORT_GET_STREAM_POS,
    eMINIPORT_SET_WAVERT_BUFFER_WRITE_POS,
    eMINIPORT_GET_PRESENTATION_POS,
    eMINIPORT_PROGRAM_DMA,
    eMINIPORT_GLITCH_REPORT
} EPcMiniportEngineEvent;
```

この列挙型の詳細については、「 [**EPcMiniportEngineEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ne-portcls-epcminiportengineevent)」を参照してください。

ハードウェアオフロードオーディオストリームを処理できるドライバーを開発する方法の詳細については、「[ドライバーの実装の詳細](driver-implementation-details.md)」を参照してください。

 

 




