---
title: ドライバーを検証するためのツール
description: ドライバーを検証するためのツール
ms.assetid: 1d878be6-8730-4452-a35a-0635ebed9091
keywords:
- ツール WDK, ドライバーの検証
- ドライバー開発ツール WDK, ドライバーの検証
- ドライバーの WDK を検証する
- ドライバー検証 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1f541cd66d37cb0a582dacad75dd44ab061fcf6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839998"
---
# <a name="tools-for-verifying-drivers"></a>ドライバーを検証するためのツール

Windows Driver Kit (WDK) には、開発プロセス中にドライバーコードのエラーを検出して修正できるように設計された、非常に包括的なツールがいくつか含まれています。 これらのツールの多くは、開発プロセスのかなり初期に使用でき、非常に重要な役割を果たし、時間と労力を大幅に節約します。

これらの検証ツールは、各ツールがさまざまな種類のドライバーエラーを検出するため、WDK のドキュメントで説明されており、使用することをお勧めします。 これらのツールは、手動チェックよりもはるかに効率的です。 これらのツールは、標準のドライバーテストでは通常は見つからないエラーを検出でき、熟練したドライバー開発者および Windows driver interface designer の専門知識を具体化します。

最適な結果を得るには、ドライバーで実行可能なすべてのツールを使用します。 これらのツールのいずれかを省略すると、ドライバーに重大なバグが発生する可能性があります。

このセクションでは、まず、コード検証ツールの特性、および WDK および Windows に含まれるツールと Microsoft から提供されるツールについて簡単に説明します。

このセクションの内容:

[静的および動的な検証ツール](static-and-dynamic-verification-tools.md)

[検証ツールの調査](survey-of-verification-tools.md)

[DDI コンプライアンス規則](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[Windows のチェックされたビルド](checked-build-of-windows.md)

[アプリケーション検証ツール](application-verifier.md)

[ドライバーのコード分析](code-analysis-for-drivers.md)

[ドライバー検証ツール](driver-verifier.md)

[静的ドライバー検証ツール](static-driver-verifier.md)

[WDF 検証コントロールアプリケーション](wdf-verifier-control-application.md)

[WdfTester: WDF Driver テストツールセット](wdftester--wdf-driver-testing-toolset.md)

### <a name="span-idother_toolsspanspan-idother_toolsspanother-tools"></a><span id="other_tools"></span><span id="OTHER_TOOLS"></span>その他のツール

他のコードまたはドライバー検証ツール (他のソースから) にアクセスできる場合は、WDK のツールに加えて使用することをお勧めします。 ドライバー、[静的ドライバー検証](static-driver-verifier.md)ツール、および[ドライバーの検証](driver-verifier.md)ツールは Windows ドライバーに固有の知識があるため、必ず[コード分析](code-analysis-for-drivers.md)を使用してください。ただし、すべてのツールがコードをさまざまな方法で確認するため、検出と修正に役立ちます。さまざまな種類の問題。
