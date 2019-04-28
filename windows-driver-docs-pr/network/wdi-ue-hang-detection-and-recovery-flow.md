---
title: UE ハングアップ検出と復旧フロー
description: この図は、UE ハングアップ検出とリセット フローを示しています。
ms.assetid: 49B73223-91BA-4140-BB2B-8AB0CB355406
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f9ac505dfc6aa51305cc00e1b7ab0dbde515605
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368210"
---
# <a name="ue-hang-detection-and-recovery-flow"></a>UE ハングアップ検出と復旧フロー


この図は、UE ハングアップ検出とリセット フローを示しています。

![wdi ハングアップ検出と復旧フロー](images/wdi-hang-detection-recovery-flow.png)

図は、主要なフェーズで構成されます。

1.  ハング検出
2.  Log
3.  リセット: 突然削除処理

この機能がファームウェアのハングをアドレスを念頭に重要です。 ドライバーのハングを IHV は解決されません。 ドライバーするハングを IHV は、ハード リブートでのみ解決できます。 ドライバーは、読み込まれたことができる前にすべてのハンドルとその他のリソースを解放する必要があります。 ドライバーをアンロードすることはできません、回復は機能しません。

このフロー図は、すべての NDIS Oid とミニポートへのコールバックに一般的に適用します。 NDIS またはバスできませんリセット回復をサポートして完全場合リセット recovery の復旧の一部は機能しないという例外的なケースである可能性があります。 2 つのケースの例では、ミニポートの初期化中には、または、ミニポート中に処理を中断します。

## <a name="related-topics"></a>関連トピック


[UE ハング検出: 1 ~ 14 のステップ](wdi-ue-hang-detection--step-1-to-step-14.md)

[(突然の削除) のリセット: 15 ~ 20 のステップ](wdi-reset--surprise-remove---steps-15-20.md)

 

 






