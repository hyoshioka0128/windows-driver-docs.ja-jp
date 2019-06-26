---
title: 品質管理
description: 品質管理
ms.assetid: 359e6e12-903f-4037-8f35-b090ce41f770
keywords:
- ストリーミングの品質管理 WDK カーネル
- KSPROPERTY_STREAM_QUALITY
- KSQUALITY_MANAGER
- 通知の WDK カーネル ストリーミング
- ストリーミングの苦情 WDK カーネル
- カーネルの WDK、品質管理のストリーミング
- KS WDK、品質管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd514deeb1f421bb4fc7a4523db04ecd08366bc5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385685"
---
# <a name="quality-management"></a>品質管理





ストリーミング アーキテクチャ カーネルでは、品質管理のオプションのサポートを提供します。 このメカニズムでは、リソースの制約に一致するようにフロー制御を調整し、フィルターのグラフでの低下のニーズを決定します。 品質管理の通知は、カーネル モード プロキシを介して送信されます。

品質管理の問題のサポートを報告する pin、 [ **KSPROPERTY\_ストリーム\_品質**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-quality)プロパティ。 これは、QM 苦情のシンクのハンドルとコンテキスト パラメーターに、pin を設定できるオプションの書き込み専用プロパティです。 これを行うには、pin は型の構造体を提供します[ **KSQUALITY\_MANAGER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksquality_manager)この情報を格納します。 暗証番号 (pin) の接続がさらにこの情報を使用して使用して問題の品質マネージャー通知、 [ **KSQUALITY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksquality)特定のコンテキスト パラメーターを含む構造体。

品質管理苦情を送信するユーザー モードのクライアントを許可するのには、ミニドライバーは、プロパティをサポートしています。 [KSPROPSETID\_品質](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-quality)します。

Pin では、パフォーマンス低下の戦略を許可している場合、ミニドライバーをサポートしています、 [ **KSPROPERTY\_ストリーム\_低下**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-degradation)プロパティ。

詳細については、次を参照してください。 [ **KSDEGRADE** ](https://docs.microsoft.com/previous-versions/ff561671(v=vs.85))と[ **KSDEGRADE\_標準**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-ksdegrade_standard)します。

 

 




