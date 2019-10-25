---
title: レンダリング操作のオプションに対するサポートのレポート
description: レンダリング操作のオプションに対するサポートのレポート
ms.assetid: 97a0b8c6-7ff8-47df-97df-4e9714ebc903
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e53f898c34ac57a20bb8cb631178ff5c88afd7c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825932"
---
# <a name="reporting-optional-support-for-rendering-operations"></a>レンダリング操作のオプションに対するサポートのレポート


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


Windows 7 以降では、ディスプレイミニポートドライバーは、ドライバーがサポートできる、またはサポートできない特定のレンダリング操作を示すために、 [**DXGK\_のプレゼンテーション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)の構造体に追加のメンバーを設定できます。

使用可能な表示機能の設定の詳細については、「 [**DXGK\_のプレゼンテーションキャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)」を参照してください。

 

 





