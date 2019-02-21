---
title: ソース コード ウィンドウで色の設定
description: ソース コード ウィンドウで色の設定
ms.assetid: 1bc3635b-31ed-4453-aaef-cd5aac637df2
keywords:
- WDK Static Driver Verifier の色分け
- Static Driver Verifier レポート WDK、ソース コード ウィンドウ
- ソース コード ウィンドウ WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54cf997c4d9268f5a1619f41233faa93630bdbd6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537682"
---
# <a name="color-coding-in-the-source-code-pane"></a>ソース コード ウィンドウで色の設定


SDV は、コードのソースをすばやく把握に役立つコーディングの色を使用します。

-   *背景色*を表示しているファイルの種類を決定するのに役立ちます。

-   *テキストの色*ファイル内のコードに関する情報を提供します。

-   A*青の強調表示*で選択されている要素に関連付けられているソース コードの行を示します、**トレース ツリー**ウィンドウ。 要素が選択した場合にのみ表示される、**トレース ツリー**ウィンドウ。

### <a name="span-idbackgroundcolorsspanspan-idbackgroundcolorsspanbackground-colors"></a><span id="background_colors"></span><span id="BACKGROUND_COLORS"></span>背景色

**ソース コード ウィンドウ**2 つの背景色、黄と白が含まれています。

-   **黄色**:C ファイル、ヘッダー ファイル、およびライブラリ ファイルなど、ドライバーからソース コードを示します。

-   **ホワイト**:SDV からソース コードを示します。 これが含まれています[ルール ファイル (.slic)](static-driver-verifier-rule.md)とオペレーティング システムのモデル ファイル、Sdv harness.c します。

### <a name="span-idtextcolorsspanspan-idtextcolorsspantext-colors"></a><span id="text_colors"></span><span id="TEXT_COLORS"></span>テキストの色

次のテキストの色を使用、**ソース コード**ウィンドウ。

-   **緑:**[コメント]: 

-   **赤:** 規則違反へのパスで実行されるコード。

-   **黒:** コード規則違反へのパスでは実行されません。

-   **青。**(規則のソース ファイル (\*.slic) のみ)。規則違反へのパスで実行されないコードを示します。

 

 





