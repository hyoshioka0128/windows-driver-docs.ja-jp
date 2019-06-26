---
title: フェンス識別子の提供
description: フェンス識別子の提供
ms.assetid: 0ec8a4eb-c441-47ae-b5de-d86e6065ffd4
keywords:
- フェンス識別子 WDK を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e9a60919c4ef9e6e3d1797c4120df0418998dcd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383081"
---
# <a name="supplying-fence-identifiers"></a>フェンス識別子の提供


Microsoft DirectX グラフィックスのカーネル サブシステムと同じフェンスの識別子を提供する、 **SubmissionFenceId**のメンバー、 [ **DXGKARG\_PATCH** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_patch)と[ **DXGKARG\_SUBMITCOMMAND** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_submitcommand)ディスプレイ ミニポート ドライバーの呼び出しで構造[ **DxgkDdiPatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)と[ **DxgkDdiSubmitCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)関数。 グラフィックス ハードウェアの実装方法に応じて、ドライバーはのいずれかに渡されたフェンス識別子を使用する必要のみが、 *DxgkDdiPatch*または*DxgkDdiSubmitCommand*関数を次の理由:

-   ドライバーに渡されたフェンス識別子を使用して*DxgkDdiPatch*ダイレクト メモリ アクセス (DMA) バッファーの末尾に書き込む。

-   ドライバーに渡されたフェンス識別子を使用して*DxgkDdiSubmitCommand* DMA バッファー キューに入れられた実行 (ほとんどの種類の GPU を使用して、DMA バッファー、グラフィックス処理装置 (GPU) で、バッファーは、リング バッファーに書き込むキュー モデル)。

 

 





