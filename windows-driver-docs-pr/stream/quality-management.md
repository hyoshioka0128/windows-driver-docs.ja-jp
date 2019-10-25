---
title: 品質管理
description: 品質管理
ms.assetid: 359e6e12-903f-4037-8f35-b090ce41f770
keywords:
- 品質管理 WDK カーネルストリーミング
- KSPROPERTY_STREAM_QUALITY
- KSQUALITY_MANAGER
- 通知 WDK カーネルストリーミング
- 苦情 WDK カーネルストリーミング
- カーネルストリーミング WDK、品質管理
- KS WDK、品質管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4ee37d46bcd13adc6ac8b2f12585a6fc62bae0a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841662"
---
# <a name="quality-management"></a>品質管理





カーネルストリーミングアーキテクチャでは、品質管理のオプションのサポートが提供されます。 このメカニズムにより、リソース制約に一致するようにフロー制御が調整され、フィルターグラフでの低下の必要性が決まります。 品質管理の通知は、カーネルモードのプロキシを介して送信されます。

品質管理の問題を報告する pin では、 [**Ksk プロパティ\_STREAM\_quality**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-quality)プロパティがサポートされています。 これは、省略可能な書き込み専用プロパティで、pin は、QM 準拠のシンクのハンドルおよびコンテキストパラメーターに設定できます。 これを行うために、pin は、この情報を格納する型[**Ksk quality\_MANAGER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksquality_manager)の構造を提供します。 次に、ピン接続によって、この情報を使用して、指定されたコンテキストパラメーターを持つ[**Ksk 品質**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksquality)構造体を使用して、問題の品質管理者に通知します。

ユーザーモードのクライアントが品質管理の苦情を送信できるようにするために、ミニドライバーは、 [Kspropsetid\_品質](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-quality)のプロパティをサポートしています。

Pin で劣化戦略が許可されている場合、ミニドライバーでは、 [**Ksk プロパティ\_STREAM\_劣化**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-degradation)プロパティがサポートされます。

詳細については、「 [**ksdegrade**](https://docs.microsoft.com/previous-versions/ff561671(v=vs.85))と[**KSK が\_STANDARD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-ksdegrade_standard)」を参照してください。

 

 




