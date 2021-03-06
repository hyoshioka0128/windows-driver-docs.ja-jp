---
title: 静的および動的な検証ツール
description: 静的および動的な検証ツール
ms.assetid: 8bdf1f11-5deb-427b-b058-b9173e167f8d
keywords:
- WDK の動的検証ツール
- WDK の静的検証ツール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85ee71c08150862d32e1515782d38866b5cefad4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380011"
---
# <a name="static-and-dynamic-verification-tools"></a>静的および動的な検証ツール


2 つの基本的な種類の検証ツールがあります。

-   **静的検証ツール**ドライバーを実行しなくてもドライバーのコードを確認します。 これらのツールは、テスト コードを実行するには依存しない、徹底的な非常にすることがあります。 理論上は、静的検証ツールではすべての実習ではめったに実行するコード パスを含む、ドライバーのコードを調べることができます。 ただし、ドライバーが実際に実行されていないため、偽陽性の結果を生成するでした。 つまりが実際には発生しないコード パスでエラーをレポートする場合があります。

-   **動的検証ツール**ドライバーの実行中に、通常は一般的に使用する呼び出しをインターセプトすることで、ドライバーのコードを調べる[ドライバー サポート ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)と置き換えて、独自のエラー チェックのバージョンへの呼び出し同じルーチン。 動的なツールは、検証を行っているときに、ドライバーが実際に実行中、ため、偽陽性の結果はまれです。 ただし、動的なツールでは、ドライバーを監視している間に発生したアクションのみを検出、ために、ドライバーのテスト カバレッジが十分でない場合、ツールは特定のドライバー欠陥ミスことができます。 同時に、実行時に、利用可能な情報を使用して、については、ソース コードから静的に抽出するが困難動的検証ツールを検出できます特定のクラスの静的分析で検出するにくいドライバー エラーツールです。

静的および動的な検証ツールの組み合わせを使用することをお勧めします。 静的なツールを使用すると、動的なツールは、ドライバーで重大なエラーが発生しているを検索中に、実際には、実行しにくいコード パスを確認できます。

 

 





