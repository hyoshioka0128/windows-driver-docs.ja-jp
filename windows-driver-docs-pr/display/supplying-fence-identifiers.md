---
title: フェンスの識別子を指定します。
description: フェンスの識別子を指定します。
ms.assetid: 0ec8a4eb-c441-47ae-b5de-d86e6065ffd4
keywords:
- フェンス識別子 WDK を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 715ace0caaad49ceca450485fc5f40819fcabe3a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557502"
---
# <a name="supplying-fence-identifiers"></a>フェンスの識別子を指定します。


Microsoft DirectX グラフィックスのカーネル サブシステムと同じフェンスの識別子を提供する、 **SubmissionFenceId**のメンバー、 [ **DXGKARG\_PATCH** ](https://msdn.microsoft.com/library/windows/hardware/ff557610)と[ **DXGKARG\_SUBMITCOMMAND** ](https://msdn.microsoft.com/library/windows/hardware/ff559490)ディスプレイ ミニポート ドライバーの呼び出しで構造[ **DxgkDdiPatch**](https://msdn.microsoft.com/library/windows/hardware/ff559737)と[ **DxgkDdiSubmitCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff560790)関数。 グラフィックス ハードウェアの実装方法に応じて、ドライバーはのいずれかに渡されたフェンス識別子を使用する必要のみが、 *DxgkDdiPatch*または*DxgkDdiSubmitCommand*関数を次の理由:

-   ドライバーに渡されたフェンス識別子を使用して*DxgkDdiPatch*ダイレクト メモリ アクセス (DMA) バッファーの末尾に書き込む。

-   ドライバーに渡されたフェンス識別子を使用して*DxgkDdiSubmitCommand* DMA バッファー キューに入れられた実行 (ほとんどの種類の GPU を使用して、DMA バッファー、グラフィックス処理装置 (GPU) で、バッファーは、リング バッファーに書き込むキュー モデル)。

 

 





