---
title: 一般的な設計および実装の戦略
description: 一般的な設計および実装の戦略
ms.assetid: c631062c-87ec-4bad-9de2-1844d0c81661
keywords:
- ディスプレイ ドライバー モデル WDK Windows 2000 では、戦略
- Windows 2000 のディスプレイ ドライバー モデル WDK、戦略
- ビデオのミニポート ドライバー WDK Windows 2000 では、戦略
- ディスプレイ ドライバー WDK Windows 2000 では、戦略
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0589881083b5c32dbc2ecca9cd5e0e01ec20e6d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377975"
---
# <a name="general-design-and-implementation-strategies"></a>一般的な設計および実装の戦略


## <span id="ddk_general_design_and_implementation_strategies_gg"></span><span id="DDK_GENERAL_DESIGN_AND_IMPLEMENTATION_STRATEGIES_GG"></span>


を、有効な Windows 2000 を設計およびドライバーとビデオのミニポート ドライバーを後で表示するには、次の方法を検討してください。

-   ドライバー設計の時間を短縮するグラフィックス アダプターのような種類のように設計された既存の Windows Driver Kit (WDK) サンプル ドライバーを変更します。

-   C を使用して、ハードウェアによってもサポートされていないタイム クリティカルな操作に必要な場合にのみ、アセンブリ言語を使用して、移植性を最大限にできるだけ多くドライバーの記述。 アセンブリ内のコーディングには、最適化の可能性を向上しますが、時間と移植性の問題は、その利点を上回る。

-   ビデオのミニポート ドライバーを使用して、リソースの管理、物理デバイスのメモリ マッピングを実行、出力が近接、発生するか、割り込みに応答に登録することを確認する操作。 ミニポート ドライバーは、主に、ハードウェア ファミリ内のバリエーションを処理するため、ディスプレイ ドライバーのハードウェアの種類の依存関係を最小限に抑えるために使用します。

ドライバーの作成者を表示する目的の詳細については、次を参照してください。[ドライバーの表示のグラフィックス DDI 関数](graphics-ddi-functions-for-display-drivers.md)します。 このトピックとサブトピックをそれに続く グラフィックスは、必要な条件付きで必要なディスプレイ ドライバーの省略可能な DDI 関数について説明します。 [Windows 2000 Display Driver Model でのビデオのミニポート ドライバー](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)サブトピックがビデオのミニポート ドライバーの作成者を目的とした同様の情報を含めることができます。

次の点も考慮する必要があります。

-   ディスプレイ ドライバーとビデオのミニポート ドライバーは、NT エグゼクティブの残りの部分と同じ特権のカーネル モード アドレス空間で動作します。 いずれかのドライバーでエラーをエラーに、システムの残りの部分となります。

-   ディスプレイ ドライバーやビデオのミニポート ドライバーは、いつでも割り込まれることができます。

-   ディスプレイ ドライバーのコードとデータのセクションでは、ページング可能な完全の両方です。

-   エクスポートされた関数は、標準の NT ベースのオペレーティング システムを実行する必要があります*プロローグ*エントリで、*エピローグ*終了時にします。 詳細については、Microsoft Windows SDK のドキュメントを参照してください。

ディスプレイ ドライバーに固有の情報については、次を参照してください。[ドライバーの表示のグラフィックス DDI 関数](graphics-ddi-functions-for-display-drivers.md)します。 そのセクションには、必要な条件付きで必要ですが、および必要に応じて必要なグラフィック DDI 関数に関する情報が含まれています。

 

 





