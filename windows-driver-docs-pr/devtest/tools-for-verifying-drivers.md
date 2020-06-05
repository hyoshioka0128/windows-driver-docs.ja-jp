---
title: ドライバーを検証するためのツール
description: ドライバーを検証するためのツール
ms.assetid: 1d878be6-8730-4452-a35a-0635ebed9091
keywords:
- ツール WDK, ドライバーの検証
- ドライバー開発ツール WDK, ドライバーの検証
- ドライバーの WDK を検証する
- ドライバー検証 WDK
ms.date: 06/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: 9f5f340babca67386cd3193e37e61b15046a7add
ms.sourcegitcommit: 0a0b75d93130b6c5854279607cd0aac099f65fd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428319"
---
# <a name="tools-for-verifying-drivers"></a>ドライバーを確認するためのツール

Windows Driver Kit (WDK) には、開発プロセス中にドライバーコードのエラーを検出して修正できるように設計された、非常に包括的なツールがいくつか含まれています。 これらのツールの多くは、開発プロセスのかなり初期に使用でき、非常に重要な役割を果たし、時間と労力を大幅に節約します。

これらの検証ツールは、各ツールがさまざまな種類のドライバーエラーを検出するため、WDK のドキュメントで説明されており、使用することをお勧めします。 これらのツールは、手動チェックよりもはるかに効率的です。 これらのツールは、標準のドライバーテストでは通常は見つからないエラーを検出でき、熟練したドライバー開発者および Windows driver interface designer の専門知識を具体化します。

最適な結果を得るには、ドライバーで実行可能なすべてのツールを使用します。 これらのツールのいずれかを省略すると、ドライバーに重大なバグが発生する可能性があります。

> [!NOTE]
> チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。
> Driver Verifier や GFlags などのツールを使用して、新しいバージョンの Windows でドライバーコードを確認します。

このセクションでは、まず、コード検証ツールの特性、および WDK および Windows に含まれるツールと Microsoft から提供されるツールについて簡単に説明します。

ここでは、以下の内容について説明します。

[静的および動的な検証ツール](static-and-dynamic-verification-tools.md)

[検証ツールの調査](survey-of-verification-tools.md)

[DDI コンプライアンス規則](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[Windows のチェック ビルド](checked-build-of-windows.md)

[アプリケーション検証ツール](application-verifier.md)

[ドライバーのコード分析](code-analysis-for-drivers.md)

[ドライバーの検証ツール](driver-verifier.md)

[静的ドライバー検証ツール](static-driver-verifier.md)

[WDF 検証ツール制御アプリケーション](wdf-verifier-control-application.md)

[WdfTester: WDF Driver テストツールセット](wdftester--wdf-driver-testing-toolset.md)

## <a name="other-tools"></a>その他のツール

他のコードまたはドライバー検証ツール (他のソースから) にアクセスできる場合は、WDK のツールに加えて使用することをお勧めします。 [ドライバーのコード分析](code-analysis-for-drivers.md)、[静的ドライバーの検証](static-driver-verifier.md)ツール、およびドライバーの[検証](driver-verifier.md)ツールは、Windows ドライバーに固有の情報があるため、コードをさまざまな方法で確認するため、さまざまな種類の問題を見つけて修正するのに役立ちます。
