---
title: 複数ヘッドによるプレゼンテーション
description: 複数ヘッドによるプレゼンテーション
ms.assetid: 60405ea7-91d5-4deb-9161-8890faa7e897
keywords:
- 複数ヘッド ハードウェア WDK DirectX 9.0、プレゼンテーション
- WDK DirectX 9.0 のプレゼンテーション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1de73f1b6d7360ff3f48dc7a1dde9af6b2a6fdfc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363739"
---
# <a name="presentation-with-multiple-heads"></a>複数ヘッドによるプレゼンテーション


## <span id="ddk_presentation_with_multiple_heads_gg"></span><span id="DDK_PRESENTATION_WITH_MULTIPLE_HEADS_GG"></span>


アプリケーションが呼び出すことができます、**存在**メソッドすべてのヘッドのバック バッファーの内容を一度に表示するか、個々 の head バック バッファーを提示します。 詳細については**存在**、DirectX SDK の最新のドキュメントを参照してください。

ランタイムは、ドライバーの独立した連続した呼び出しをさらに、 [ *DdFlip* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip)または[ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)関数。 各ヘッドの表示モードとリフレッシュ レートが異なる可能性があります、ため、これらの呼び出しは DDI レベルで独立して常に。

 

 





