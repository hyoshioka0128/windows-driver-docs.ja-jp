---
title: 共通バッファー バス マスター DMA
description: 共通バッファー バス マスター DMA
ms.assetid: 4758e084-1d9e-4e17-8627-05edc6b664ba
keywords:
- バス マスターの DMA WDK ビデオのミニポート、一般的なバッファー
- DMA バス マスター WDK ビデオのミニポート、一般的なバッファー
- 一般的なバッファーの DMA WDK ビデオのミニポート、説明
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 392a2f1b98539f5f4136b836bede6c659c056943
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343022"
---
# <a name="common-buffer-bus-master-dma"></a>共通バッファー バス マスター DMA


## <span id="ddk_common_buffer_bus_master_dma_gg"></span><span id="DDK_COMMON_BUFFER_BUS_MASTER_DMA_GG"></span>


ミニポート ドライバーでは、次の一連の一般的なバッファー DMA を使用する操作を実行します。

1.  アダプター オブジェクトを取得します。

    ミニポート ドライバー呼び出しビデオ ポート ドライバーの[ **VideoPortGetDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff570312)関数は、通常、ミニポート ドライバーの[ *HwVidFindAdapter*](https://msdn.microsoft.com/library/windows/hardware/ff567332)へのポインターを取得する、ルーチン、 [**担当副社長\_DMA\_アダプター** ](https://msdn.microsoft.com/library/windows/hardware/ff570570)構造体。 ミニポート ドライバーでは、このポインターを使用して、残りの DMA 操作。

2.  一般的なバッファーを割り当てます。

    ミニポート ドライバー呼び出しビデオ ポート ドライバーの[ **VideoPortAllocateCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff570178)関数は、前の手順で取得したポインターを使用します。

3.  一般的なバッファーを解放します。

    ビデオ ポート ドライバーの呼び出し、ミニポート ドライバーでは、共通のバッファーが必要なくなる、 [ **VideoPortReleaseCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff570355)関数。

4.  アダプター オブジェクトを破棄します。

    この手順は省略可能です。 ビデオ ポート ドライバーを呼び出すことによって、DMA アダプター オブジェクトを破棄する必要があります、何らかの理由で、ミニポート ドライバー決定した場合があるない有効期間の残りの部分の DMA 操作をさらに、 [ **VideoPortPutDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff570335)関数。

 

 





