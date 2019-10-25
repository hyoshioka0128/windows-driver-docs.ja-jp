---
title: フェンス識別子の提供
description: フェンス識別子の提供
ms.assetid: 0ec8a4eb-c441-47ae-b5de-d86e6065ffd4
keywords:
- フェンス識別子 WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66e618d1a263af6ca22683625ea1fe4662d77fe8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829415"
---
# <a name="supplying-fence-identifiers"></a>フェンス識別子の提供


Microsoft DirectX graphics カーネルサブシステムでは、 [**dxgkarg\_PATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_patch)と[**dxgkarg\_Submitgkarg**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_submitcommand)の**SubmissionFenceId**メンバーに同じフェンス識別子が提供されます。ミニポートドライバーの[**DxgkDdiPatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)関数と[**DxgkDdiSubmitCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)関数。 グラフィックスハードウェアの実装方法によっては、ドライバーは、次の理由により、 *DxgkDdiPatch*または*DxgkDdiSubmitCommand*関数のいずれかに渡されるフェンス識別子を使用する必要があります。

-   ドライバーは、 *DxgkDdiPatch*に渡されたフェンス識別子を使用して、ダイレクトメモリアクセス (DMA) バッファーの末尾に書き込みます。

-   ドライバーは、 *DxgkDdiSubmitCommand*に渡されたフェンス識別子を使用してリングバッファーに書き込みます。これは、dma バッファーがグラフィックス処理装置 (gpu) によって実行されるようにキューに置かれるバッファーです (ほとんどの gpu 型は dma バッファーキューモデルを使用します)。

 

 





