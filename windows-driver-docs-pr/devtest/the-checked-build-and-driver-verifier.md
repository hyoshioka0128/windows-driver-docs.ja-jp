---
title: チェック ビルドとドライバーの検証ツール
description: チェック ビルドとドライバーの検証ツール
ms.assetid: 311a9588-5094-432c-b696-339ff3ff8c35
keywords:
- チェック ビルド WDK、Driver Verifier
- Driver Verifier の WDK チェック ビルドします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab66cf60ab0dc6a0565b1a68b665c51b41a1fcb2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579458"
---
# <a name="the-checked-build-and-driver-verifier"></a>チェック ビルドとドライバーの検証ツール


## <span id="ddk_the_checked_build_and_driver_verifier_tools"></span><span id="DDK_THE_CHECKED_BUILD_AND_DRIVER_VERIFIER_TOOLS"></span>


チェック ビルド中に、 [Driver Verifier](driver-verifier.md)重なっているため、のお勧め補完的なレベルのチェックを提供するものとして捉えることをいくつかがチェックを提供します。 チェック ビルドとドライバーのテストは、Driver Verifier でのテストに代わるものではありません。 同様に、ドライバーの検証ツールでのテストは提供されませんチェック ビルドを使用して、テスト カバレッジの正確に同じレベル。

Driver Verifier チェック ビルドで実行されると、多くの場合、デバッガーで追加情報を表示、問題が検出された場合。 さらに、デバッガーがアタッチされると、多くの場合 Driver Verifier 実行バグ チェックでシステムを停止する前にブレークポイント。 このブレークポイントでは、システムの状態を確認し、Driver Verifier 呼び出さシステム クラッシュ前に、ドライバーをデバッグする機会を与えます。

 

 





