---
title: 複数ヘッドによるプレゼンテーション
description: 複数ヘッドによるプレゼンテーション
ms.assetid: 60405ea7-91d5-4deb-9161-8890faa7e897
keywords:
- 複数ヘッド ハードウェア WDK DirectX 9.0、プレゼンテーション
- WDK DirectX 9.0 のプレゼンテーション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e37ca5e1535322dd7fbf81e500c4e1ced7ffc7b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578173"
---
# <a name="presentation-with-multiple-heads"></a>複数ヘッドによるプレゼンテーション


## <span id="ddk_presentation_with_multiple_heads_gg"></span><span id="DDK_PRESENTATION_WITH_MULTIPLE_HEADS_GG"></span>


アプリケーションが呼び出すことができます、**存在**メソッドすべてのヘッドのバック バッファーの内容を一度に表示するか、個々 の head バック バッファーを提示します。 詳細については**存在**、DirectX SDK の最新のドキュメントを参照してください。

ランタイムは、ドライバーの独立した連続した呼び出しをさらに、 [ *DdFlip* ](https://msdn.microsoft.com/library/windows/hardware/ff549306)または[ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205)関数。 各ヘッドの表示モードとリフレッシュ レートが異なる可能性があります、ため、これらの呼び出しは DDI レベルで独立して常に。

 

 





