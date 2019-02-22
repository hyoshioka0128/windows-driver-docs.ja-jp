---
title: チェックのビルドを使用しての副作用
description: チェックのビルドを使用しての副作用
ms.assetid: 8c08d4f3-1221-4858-afd4-249d966c14a7
keywords:
- チェック ビルド WDK、パフォーマンスに与える影響
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 143270b884efea157d98b35c3c50d6e9e7fc3205
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539275"
---
# <a name="side-effects-of-using-the-checked-build"></a>チェックのビルドを使用しての副作用


## <span id="ddk_side_effects_of_using_the_checked_build_tools"></span><span id="DDK_SIDE_EFFECTS_OF_USING_THE_CHECKED_BUILD_TOOLS"></span>


チェックされているオペレーティング システムのコンポーネントには、以下の最適化と無料のコンポーネントをそれ以外の場合と同じよりもより多くのデバッグ チェックが含まれています。 そのため、チェックされているコンポーネントは無料の対応するよりもかなり遅く実行します。

この実行速度が遅くによりタイミングの関係のコード パスの変更が生じる可能性があることを覚えておくドライバー作成者が重要です。 そのため、チェック ビルドは、無料のビルドで明らかになる可能性があります (競合状態やデッドロック) タイミングの問題を非表示にすることができます。 したがって、すべての無料のビルドとリリースの前に、オペレーティング システムのチェック ビルドの両方で、ドライバーをテストする必要があります。

 

 





