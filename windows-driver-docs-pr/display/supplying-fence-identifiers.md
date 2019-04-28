---
title: フェンス識別子の提供
description: フェンス識別子の提供
ms.assetid: 0ec8a4eb-c441-47ae-b5de-d86e6065ffd4
keywords:
- フェンス識別子 WDK を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 715ace0caaad49ceca450485fc5f40819fcabe3a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375949"
---
# <a name="supplying-fence-identifiers"></a>フェンス識別子の提供


Microsoft DirectX グラフィックスのカーネル サブシステムと同じフェンスの識別子を提供する、 **SubmissionFenceId**のメンバー、 [ **DXGKARG\_PATCH** ](https://msdn.microsoft.com/library/windows/hardware/ff557610)と[ **DXGKARG\_SUBMITCOMMAND** ](https://msdn.microsoft.com/library/windows/hardware/ff559490)ディスプレイ ミニポート ドライバーの呼び出しで構造[ **DxgkDdiPatch**](https://msdn.microsoft.com/library/windows/hardware/ff559737)と[ **DxgkDdiSubmitCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff560790)関数。 グラフィックス ハードウェアの実装方法に応じて、ドライバーはのいずれかに渡されたフェンス識別子を使用する必要のみが、 *DxgkDdiPatch*または*DxgkDdiSubmitCommand*関数を次の理由:

-   ドライバーに渡されたフェンス識別子を使用して*DxgkDdiPatch*ダイレクト メモリ アクセス (DMA) バッファーの末尾に書き込む。

-   ドライバーに渡されたフェンス識別子を使用して*DxgkDdiSubmitCommand* DMA バッファー キューに入れられた実行 (ほとんどの種類の GPU を使用して、DMA バッファー、グラフィックス処理装置 (GPU) で、バッファーは、リング バッファーに書き込むキュー モデル)。

 

 





