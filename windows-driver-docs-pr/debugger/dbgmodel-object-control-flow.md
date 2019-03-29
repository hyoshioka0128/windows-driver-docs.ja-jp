---
title: Debugger Data Model - 制御フロー オブジェクト
description: 完全分析の逆アセンブリの各基本ブロックには、制御フロー オブジェクトのセットが含まれています。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: b410b04de5f2ad5172bbd1c3fe85498ac71c6f28
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572152"
---
# <a name="control-flow-objects"></a>制御フロー オブジェクト 
## <a name="summary"></a>まとめ
完全分析の逆アセンブリの各`basic block`InboundControlFlows と OutboundControlFlows の両方のプロパティで制御フロー オブジェクトのセットが含まれています。
## <a name="object-properties"></a>オブジェクトのプロパティ
|名前|説明|
|--- |--- |
|LinkedBlock|リンクの反対側に基本的なブロックのオブジェクト。 場合、受信の制御フローは、これは、分岐命令がありましたが、基本的な要素を指します。 場合、送信制御フローは、これは、分岐命令の対象となる基本的な要素を指します。|
|LinkKind|制御フローの種類の結果、2 つの要素間のリンクを示します (例。"FallThrough"または「ブランチ」)。|
|SourceInstruction|制御フローのリンクのソース。 これは、分岐命令または基本的なブロック内の最後の命令です。|
|TargetInstruction|制御フローのリンク先。 これは、分岐のターゲットまたはフォール スルーで基本的なブロックの最後の命令の直後後の命令です。|