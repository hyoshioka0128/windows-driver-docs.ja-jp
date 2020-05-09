---
title: チェック ビルドを使用したときの副作用
description: チェック ビルドを使用したときの副作用
ms.assetid: 8c08d4f3-1221-4858-afd4-249d966c14a7
keywords:
- チェックされたビルド WDK、パフォーマンスへの影響
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 49c089d1928d37c2973fc3d147f441bd37bb116a
ms.sourcegitcommit: 076f9cd83313f6d8ab5688340f05bde7e8fbb8ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82999079"
---
# <a name="side-effects-of-using-the-checked-build"></a>チェック ビルドを使用したときの副作用

## <span id="ddk_side_effects_of_using_the_checked_build_tools"></span><span id="DDK_SIDE_EFFECTS_OF_USING_THE_CHECKED_BUILD_TOOLS"></span>

> [!NOTE]
> チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。
> Driver Verifier や GFlags などのツールを使用して、新しいバージョンの Windows でドライバーコードを確認します。

オペレーティングシステムのチェックされたコンポーネントには、それ以外の同じフリーコンポーネントよりも最適化やデバッグチェックが少なくなります。 したがって、チェックされたコンポーネントは、対応する無料のコンポーネントよりもかなり低速で動作します。

この実行速度が遅いと、コードパス間のタイミングの関係が変更される可能性があることに注意する必要があります。 そのため、チェックを行うビルドでは、無料のビルドで明らかになる可能性があるタイミングの問題 (競合状態やデッドロックなど) を隠すことができます。 そのため、リリース前に、無償のビルドとオペレーティングシステムのチェックされたビルドの両方で、すべてのドライバーをテストする必要があります。

 

 





