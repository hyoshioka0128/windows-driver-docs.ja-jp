---
title: オフロードされたオーディオに関するグリッチ レポート
description: このトピックでは、関連によるハードウェア オフロードされたオーディオ ストリームの故障エラーを報告する必要があるときに、オーディオ ドライバーを使用する必要があるメカニズムについて説明します。
ms.assetid: 9FF2A5D6-9382-4EE6-AA21-DCF47210F73B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e66ba18463051808df80b5c499a235f1b8b83645
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575017"
---
# <a name="glitch-reporting-for-offloaded-audio"></a>オフロードされたオーディオに関するグリッチ レポート


このトピックでは、関連によるハードウェア オフロードされたオーディオ ストリームの故障エラーを報告する必要があるときに、オーディオ ドライバーを使用する必要があるメカニズムについて説明します。

オーディオ ドライバーに故障のエラーが検出されたときに、エラーを報告する Event Tracing for Windows (ETW) イベントが発生する必要があります。 このイベントでオーディオ ストリームを使用して、DMA バッファーに関する情報と共に、故障の理由を含める必要があります。

次の列挙型には、障害エラーの報告に使用するオーディオ ドライバーに定義されているイベントが表示されます。

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

この列挙型の詳細については、次を参照してください。 [ **EPcMiniportEngineEvent**](https://msdn.microsoft.com/library/windows/hardware/dn302036)します。

によるハードウェア オフロードされたオーディオ ストリームを処理できるドライバーを開発する方法の詳細については、次を参照してください。 および[ドライバーの実装詳細](driver-implementation-details.md)します。

 

 




