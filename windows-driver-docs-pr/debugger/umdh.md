---
title: ユーザー モード ダンプ ヒープ (UMDH) ツール
description: ユーザー モード ダンプ ヒープ (UMDH) ツール、Umdh.exe、分析、特定のプロセスを Microsoft Windows ヒープ メモリの割り当て
ms.assetid: 112795a9-57c0-43a4-9f21-2a8655b65d1b
keywords: UMDH、ユーザー モード ダンプ ヒープ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52d54bcb0358effd3bcc743a4102f988d60008d4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380772"
---
# <a name="umdh"></a>UMDH


## <span id="ddk_umdh_dtools"></span><span id="DDK_UMDH_DTOOLS"></span>


ユーザー モード ダンプ ヒープ (UMDH) ツール、Umdh.exe は、特定のプロセスを Microsoft Windows ヒープ メモリの割り当てを分析します。 UMDH は、次のモードがあります。

-   **実行中のプロセスを分析**(「モード 1」)。 UMDH のキャプチャおよびプロセスのヒープ メモリの割り当てを分析します。 それぞれの割り当てに UMDH は、割り当てと割り当ての履歴を割り当てのサイズは、オーバーヘッドのサイズ、ポインターを表示します。 プロセスは、1 つ以上のアクティブなメモリ ヒープ、UMDH はすべてのヒープをキャプチャします。 この分析をリアルタイムで表示またはログ ファイルに保存できます。

-   **UMDH ログ ファイルを分析する**(「モード 2」)。 UMDH が以前に作成したログ ファイルを分析します。 UMDH が同じを異なるタイミングで処理し、呼び出しを表示用に作成された 2 つのログを比較できる割り当てサイズを増やす最もでします。 メモリ リークを見つけるには、この手法を使用できます。

このセクションの内容:

[UMDH を使用する準備](preparing-to-use-umdh.md)

[UMDH コマンド](umdh-commands.md)

[UMDH ログの解釈](interpreting-a-umdh-log.md)

[ログの比較を解釈します。](interpreting-a-log-comparison.md)

 

 





