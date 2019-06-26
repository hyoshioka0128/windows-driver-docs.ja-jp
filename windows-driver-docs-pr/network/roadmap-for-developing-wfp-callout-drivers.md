---
title: WFP コールアウト ドライバーの開発のロードマップ
description: WFP コールアウト ドライバーの開発のロードマップ
ms.assetid: 98c857d9-e4a6-4a7f-8427-642763864f3e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 915b0a6ac24881aca03dbbe25a7b7a1aa236efb0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382171"
---
# <a name="roadmap-for-developing-wfp-callout-drivers"></a>WFP コールアウト ドライバーの開発のロードマップ


Windows フィルタ リング プラットフォーム (WFP) コールアウト ドライバーを作成するには、次の手順を実行します。

-   手順 1:WFP アーキテクチャについて説明します。

    WFP については、次を参照してください。 [Windows フィルタ リング プラットフォーム](https://docs.microsoft.com/windows/desktop/FWP/windows-filtering-platform-start-page)します。 WFP ユーザー モード アプリケーションを開発および WFP コールアウト ドライバーを記述しないようにできることがあります。

-   手順 2:Windows アーキテクチャとドライバーについて説明します。

    Windows オペレーティング システムでのドライバーのしくみの基礎を理解する必要があります。 基礎を知ることに役立つ適切な設計上の決定を行い、開発プロセスを効率化することができます。 ドライバーの基礎の詳細については、次を参照してください。[ドライバー開発者向けのすべての概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)します。

-   手順 3:WFP コールアウト ドライバーの Windows ドライバー モデルを決定します。

    使用するか、Windows Driver Model (WDM) またはカーネル モード ドライバー フレームワーク (KMDF)、WFP コールアウト ドライバーを記述できます。 ドライバー モデルを選択する方法の詳細については、次を参照してください。[ドライバー モデルを選択する](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)します。 WDM の詳細については、次を参照してください。 [Windows ドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-windows-drivers)と[書き込み WDM ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-wdm-drivers)します。 KMDF の詳細については、次を参照してください。 [WDF ドライバー開発ガイド](https://docs.microsoft.com/windows-hardware/drivers/wdf/design-guide)します。

-   手順 4:その他の Windows ドライバー設計の決定を確認します。

    その他の Windows を参照してください、設計上の決定を行う方法については[信頼性の高いカーネル モード ドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)、 [64 ビット ドライバーのプログラミング問題](https://docs.microsoft.com/windows-hardware/drivers/kernel/programming-issues-for-64-bit-drivers)、および[作成国際対応の INF ファイル](https://docs.microsoft.com/windows-hardware/drivers/install/creating-international-inf-files)します。

-   手順 5:Windows ドライバーのビルド、テスト、およびデバッグ プロセスおよびツールについて説明します。

    ドライバーの構築は、ユーザー モード アプリケーションの構築とは異なります。 については、Windows ドライバーのビルド、デバッグ、およびテスト プロセス、ドライバーの署名、および[Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)テストを参照してください[のビルド、デバッグ、およびドライバーのテスト](https://docs.microsoft.com/windows-hardware/drivers)します。 ビルドの詳細については、テスト、検証、およびデバッグ ツールを参照してください[ドライバー開発ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)します。

-   手順 6:レビュー、 [Windows フィルタ リング プラットフォーム (WFP) ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618680)で、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります。

-   手順 7:WFP コールアウト ドライバーに関する設計上の決定を行います。

    WFP コールアウト ドライバーの設計方法については、次を参照してください。[コールアウト ドライバーのプログラミングに関する考慮事項](callout-driver-programming-considerations.md)します。

-   手順 8:開発、ビルド、テスト、および WFP コールアウト ドライバーをデバッグします。

    WFP コールアウト ドライバーの詳細については、次を参照してください。[コールアウト ドライバー操作](callout-driver-operations.md)と[コールアウト ドライバーのインストール](callout-driver-installation.md)します。 関数、構造体、列挙型、または WFP に固有の定数については、次を参照してください。 [Windows フィルタ リング プラットフォーム コールアウト ドライバーの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。 反復的なビルド、テスト、およびデバッグについては、次を参照してください。[概要のビルド、デバッグ、およびテスト プロセス](https://docs.microsoft.com/windows-hardware/drivers)します。 このプロセスに役立つ、動作するドライバーをビルドすることを確認します。

-   手順 9:WFP コールアウト ドライバーのドライバー パッケージを作成します。

    詳細については、次を参照してください。[ドライバー パッケージを提供する](https://docs.microsoft.com/windows-hardware/drivers)と[コールアウト ドライバーのインストール](callout-driver-installation.md)します。

-   手順 10:署名および WFP コールアウト ドライバーを配布します。

    最後の手順では、(省略可能) 署名し、ドライバーを配布します。 ドライバーが定義されている品質基準を満たしているかどうか、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)、Microsoft Windows 更新プログラムを通じて配布できます。 ドライバーを配布する方法の詳細については、次を参照してください。[ドライバーを配布する](https://docs.microsoft.com/windows-hardware/drivers)します。

これらは、基本的な手順です。 追加の手順は、個々 のドライバーのニーズに基づいて、必要でにあります。

 

 





