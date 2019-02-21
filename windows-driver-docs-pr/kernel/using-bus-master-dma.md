---
title: バス マスター DMA を使用してください。
description: バス マスター DMA を使用してください。
ms.assetid: 08357a55-aec2-4454-923f-6daaf1583a25
keywords:
- AdapterControl ルーチン、バス マスター DMA
- バス マスター DMA WDK カーネル
- DMA は、WDK カーネル、バス マスター DMA を転送します。
- アダプター オブジェクトの WDK カーネル、バス マスター DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f83451eeae3184bd7ef0438443ff3a92c95f8a1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549395"
---
# <a name="using-bus-master-dma"></a>バス マスター DMA を使用してください。





バス マスター DMA のデバイスのドライバーでは、次の種類のシステム提供の DMA サポートを使用できます。

-   パケットに基づく DMA バス マスター アダプター DMA の転送操作が完了するとや特定の IRP のもう 1 つの転送操作を開始するタイミングを判断するドライバーを使用する場合。 参照してください[Using Packet-Based バス マスター DMA](using-packet-based-bus-master-dma.md)詳細についてはします。

-   一般的なバッファーの DMA (とも呼ばれる*継続的な DMA*) バス マスター アダプターは、ドライバー、転送操作が開始されますか、転送が完了すると、すぐに判断するための手段を提供していない場合、または 1 つのバッファー領域を使用する場合継続的にまたは繰り返し DMA 転送します。 参照してください[を使用して一般的なバッファーのバス マスター DMA](using-common-buffer-bus-master-dma.md)詳細についてはします。

、バス マスター アダプターの性質に応じてドライバーによってパケットに基づく DMA を排他的に使用して、排他的に一般的なバッファー DMA を使用していくつか両方を使用していくつか。 たとえば、ステータス情報およびコマンドは、ドライバーとデータのパケットに基づく DMA と共にそのアダプター間で共有メールボックスの一般的なバッファーを使用可能性がありますを通信するために、メールボックスのスキームを使用するバス マスター アダプターのドライバーを転送します。

 

 




