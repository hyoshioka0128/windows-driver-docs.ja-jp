---
title: 例のグラフィックス メモリ レポート
description: 例のグラフィックス メモリ レポート
ms.assetid: 3dc0e7ae-db6f-4440-8c9c-7227f409f81f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7eadc4a6ffe397cd7b06a63c7568c8271795371
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539380"
---
# <a name="examples-of-graphics-memory-reporting"></a>例のグラフィックス メモリ レポート


次の例では、Windows XP と Windows Vista で異なるアダプターおよびメモリ構成を報告する数値を比較します。 例に示す、**表示**アプリケーションおよび使用可能なメモリの WinSAT アプレット レポートします。

### <a name="span-idexample1256mbdedicatedonboardgraphicsmemoryonadesktopspanspan-idexample1256mbdedicatedonboardgraphicsmemoryonadesktopspanexample-1-256-mb-dedicated-on-board-graphics-memory-on-a-desktop"></a><span id="example_1__256_mb_dedicated_on_board_graphics_memory_on_a_desktop"></span><span id="EXAMPLE_1__256_MB_DEDICATED_ON_BOARD_GRAPHICS_MEMORY_ON_A_DESKTOP"></span>例 1:256 MB 専用デスクトップで内蔵型のグラフィックス メモリ

次のスクリーン ショットでは、256 MB の専用の統合 (オンボード) グラフィックス メモリを備えた ATI 独立したグラフィックス アダプターを表示します。 ATI の独立したグラフィックス アダプターでは、グラフィックスのためのシステム メモリ (511 MB) も共有します。

次のスクリーン ショットで使用可能なメモリのレポートを示しています、**表示**Windows Vista のアプリケーション。

![windows vista のスクリーン ショットは、アプリケーションを表示します。](images/reportmem1.png)

次のスクリーン ショットは、Windows Vista で利用可能なメモリを割り当て、WinSAT アプレットのレポートを示します。

![windows vista のパフォーマンスの情報とツール アプリケーションのスクリーン ショット](images/reportmem2.png)

次のスクリーン ショットで使用可能なメモリのレポートを示しています、**表示**Windows XP でアプリケーション。

![windows xp のスクリーン ショットは、アプリケーションを表示します。](images/reportmemxp1.png)

**注**  前のスクリーン ショットは 1 つの「メモリ サイズ」数値が使用可能なグラフィックス メモリの合計サイズを正確に表したではない専用のオンボード グラフィックス メモリだけです。

 

### <a name="span-idexample232mbdedicatedonboardgraphicsmemoryonamobilecomputspanspan-idexample232mbdedicatedonboardgraphicsmemoryonamobilecomputspanexample-2-32-mb-dedicated-on-board-graphics-memory-on-a-mobile-computer"></a><span id="example_2__32_mb_dedicated_on_board_graphics_memory_on_a_mobile_comput"></span><span id="EXAMPLE_2__32_MB_DEDICATED_ON_BOARD_GRAPHICS_MEMORY_ON_A_MOBILE_COMPUT"></span>例 2:モバイル コンピューターで 32 MB 専用オンボード グラフィックス メモリ

次のスクリーン ショットでは、モバイル コンピューターに存在する NVIDIA TurboCache テクノロジの独立したアダプターを表示します。 このアダプターには専用のオンボード グラフィックス メモリの一部です。 ただし、アダプターは、グラフィックスのためのシステム メモリを共有するほとんどの場合。

次のスクリーン ショットで使用可能なメモリのレポートを示しています、**表示**Windows Vista のアプリケーション。

![windows vista のスクリーン ショットは、アプリケーションを表示します。](images/reportmemmob1.png)

次のスクリーン ショットは、Windows Vista で利用可能なメモリを割り当て、WinSAT アプレットのレポートを示します。

![windows vista のパフォーマンスの情報とツール アプリケーションのスクリーン ショット](images/reportmemmob2.png)

次のスクリーン ショットで使用可能なメモリのレポートを示しています、**表示**Windows XP でアプリケーション。

![windows xp のスクリーン ショットは、アプリケーションを表示します。](images/reportmemmobxp1.png)

**注**   TurboCache のコンピューターで上記のスクリーン ショット、1 つの「メモリ サイズ」番号の組み合わせが、合計でに示すような専用グラフィックス メモリと、システム メモリを共有します。 ここでも、使用可能なグラフィックス メモリの合計サイズを正確に表したではありません。

 

### <a name="span-idexample3256mbsharedgraphicsmemoryonamobilecomputerspanspan-idexample3256mbsharedgraphicsmemoryonamobilecomputerspanexample-3-256-mb-shared-graphics-memory-on-a-mobile-computer"></a><span id="example_3__256_mb_shared_graphics_memory_on_a_mobile_computer"></span><span id="EXAMPLE_3__256_MB_SHARED_GRAPHICS_MEMORY_ON_A_MOBILE_COMPUTER"></span>例 3:256 MB の共有モバイル コンピューターでのグラフィックス メモリ

次のスクリーン ショットでは、マザーボードの専用グラフィックス メモリを持たない Intel UMA (Unified メモリ アーキテクチャ) モバイル アダプターを表示します。 代わりに、アダプターは、すべてのグラフィックスのためのシステム メモリを共有します。

次のスクリーン ショットで使用可能なメモリのレポートを示しています、**表示**Windows Vista のアプリケーション。

![windows vista のスクリーン ショットは、アプリケーションを表示します。 ](images/reportmemmob3.png)

次のスクリーン ショットは、Windows Vista で利用可能なメモリを割り当て、WinSAT アプレットのレポートを示します。

![windows vista のパフォーマンスの情報とツール アプリケーションのスクリーン ショット](images/reportmemmob4.png)

次のスクリーン ショットで使用可能なメモリのレポートを示しています、**表示**Windows XP でアプリケーション。

![windows xp のスクリーン ショットは、アプリケーションを表示します。](images/reportmemmobxp2.png)

 

 





