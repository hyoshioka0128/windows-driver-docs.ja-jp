---
title: ドライバーを検証するためのツール
description: ドライバーを検証するためのツール
ms.assetid: 1d878be6-8730-4452-a35a-0635ebed9091
keywords:
- ツールを WDK、ドライバーの検証
- ドライバーの開発ツールを WDK、ドライバーの検証
- ドライバー WDK の確認
- WDK ドライバーの検証
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25afa7c27fc60ff7ddb7ac9aba00461c71213cb8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572224"
---
# <a name="tools-for-verifying-drivers"></a>ドライバーを検証するためのツール


Windows Driver Kit (WDK) には、検出し、開発プロセス中にドライバー コードのエラーを修正するのに役立つよう設計されているいくつかの非常に包括的なツールが含まれています。 これらのツールの多くは、開発プロセスのかなり初期に使用でき、非常に重要な役割を果たし、時間と労力を大幅に節約します。

これらの検証ツールを WDK ドキュメントで説明し、各ツールは、さまざまな方法でさまざまな種類のドライバーのエラーを検出するために、利用をお勧めします。 これらのツールは、手動のチェックよりもはるかに効率的です。 これらのツールは、標準のドライバー テストでは、通常は存在しないエラーを検出でき、経験豊かなドライバー開発者および Windows ドライバー インターフェイスの設計者の専門知識を具現化します。

最良の結果をすべてのドライバーを実行できるツールを使用します。 これらのツールを省略した場合は、ドライバーは深刻なバグを見逃す可能性が。

このセクションでは、コード検証ツールの特性と WDK と Windows、または Microsoft から入手できる付属のツールのアンケートの簡単な説明から始まります。

このセクションの内容:

[静的および動的な検証ツール](static-and-dynamic-verification-tools.md)

[検証ツールのアンケート](survey-of-verification-tools.md)

[DDI 準拠の規則](https://msdn.microsoft.com/library/windows/hardware/ff552840)

[Windows のチェック ビルド](checked-build-of-windows.md)

[アプリケーション検証ツール](application-verifier.md)

[ドライバーのコード分析](code-analysis-for-drivers.md)

[ドライバーの検証ツール](driver-verifier.md)

[静的ドライバー検証ツール](static-driver-verifier.md)

[WDF Verifier コントロール アプリケーション](wdf-verifier-control-application.md)

[WdfTester:WDF ドライバー テスト ツールセット](wdftester--wdf-driver-testing-toolset.md)

### <a name="span-idothertoolsspanspan-idothertoolsspanother-tools"></a><span id="other_tools"></span><span id="OTHER_TOOLS"></span>その他のツール

アクセスを他のコードまたはドライバーの検証ツールにある場合に (他のソース) から、私たちと WDK に含まれるツールだけでなく、それらを使用することお勧めします。 使用してください[Code Analysis for Drivers](code-analysis-for-drivers.md)、 [Static Driver Verifier](static-driver-verifier.md)、および[Driver Verifier](driver-verifier.md)により、特定の知識、Windows のドライバーがすべてのツールの検索さまざまな方法でコードを検索し、さまざまな種類の問題を修正する抑えことができます。

 

 





