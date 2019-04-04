---
title: NDIS ドライバーの開発のロードマップ
description: NDIS ドライバーの開発のロードマップ
ms.assetid: 4adc5438-d2ea-4b05-bbf3-e86cc5f3105a
keywords:
- NDIS WDK、ドライバー
- NDIS WDK、ドライバーの開発
- NDIS ドライバー WDK の開発
- Network Driver Interface Specification (NDIS) WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54cfb8cfd1e270816293b1d1db7a4a8a7132985a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570064"
---
# <a name="roadmap-for-developing-ndis-drivers"></a>NDIS ドライバーの開発のロードマップ


Network Driver Interface Specification (NDIS) ドライバー パッケージを作成するには、次の手順を実行します。

-   手順 1:Windows アーキテクチャとドライバーについて説明します。

    Windows オペレーティング システムでのドライバーのしくみの基礎を理解する必要があります。 基礎を知ることに役立つ適切な設計上の決定を行い、開発プロセスを効率化することができます。 ドライバーの基礎の詳細については、[ドライバー開発者向けのすべての概念](https://msdn.microsoft.com/library/windows/hardware/ff554731)を参照してください。

-   手順 2:NDIS について説明します。

    概要については、NDIS および NDIS ドライバーは、次のトピックを参照してください。

    [Windows ネットワーク アーキテクチャと OSI モデル](windows-network-architecture-and-the-osi-model.md)

    [ネットワーク ドライバーのプログラミングの考慮事項](network-driver-programming-considerations.md)

    [ドライバー スタックの管理](driver-stack-management.md)

    [NET\_バッファーのアーキテクチャ](net-buffer-architecture.md)

-   手順 3:その他の Windows ドライバー設計の決定を確認します。

    その他の Windows を参照してください、設計上の決定を行う方法の詳細についての[信頼性の高いカーネル モード ドライバーの作成](https://msdn.microsoft.com/library/windows/hardware/ff542904)、 [64 ビット ドライバーのプログラミングの問題](https://msdn.microsoft.com/library/windows/hardware/ff559923)、および[作成国際対応の INF ファイル](https://msdn.microsoft.com/library/windows/hardware/ff540208)します。

-   手順 4:Windows ドライバーのビルド、テスト、およびデバッグ プロセスおよびツールについて説明します。

    ドライバーの構築は、ユーザー モード アプリケーションの構築とは異なります。 Windows ドライバーのビルド、デバッグ、およびテスト プロセス、ドライバーの署名の詳細については、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)テストを参照してください[のビルド、デバッグ、およびドライバーのテスト](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)します。 ビルドの詳細については、テスト、検証、およびデバッグ ツールを参照してください[ドライバー開発ツール](https://msdn.microsoft.com/library/windows/hardware/ff545440)します。

-   手順 5:実装する NDIS ドライバーの種類を選択します。

    NDIS ドライバーの種類の詳細については、[ネットワーク ドライバー設計のガイドを使用して](using-the-network-driver-design-guide.md)を参照してください。

    ドライバーの種類のロードマップに従ってください。

    [NDIS ミニポート ドライバーの開発のためのロードマップ](roadmap-for-developing-ndis-miniport-drivers.md)

    [NDIS プロトコル ドライバーの開発のためのロードマップ](roadmap-for-developing-ndis-protocol-drivers.md)

    [NDIS フィルター ドライバーを開発するためのロードマップ](roadmap-for-developing-ndis-filter-drivers.md)

    [NDIS 中間ドライバを開発するためのロードマップ](roadmap-for-developing-ndis-intermediate-drivers.md)

    [モバイル ブロード バンドのミニポート ドライバーを開発するためのロードマップ](roadmap-to-develop-mb-miniport-drivers.md)

    [Windows プラットフォームのコールアウト ドライバーをフィルター処理を開発するためのロードマップ](roadmap-for-developing-wfp-callout-drivers.md)

-   手順 6:レビュー、[ネットワーク ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616034)で、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります。

-   手順 7:開発 (またはポート)、ビルド、テスト、およびデバッグには、NDIS ドライバー。

    既存のドライバーを移植する場合、移植ガイドを参照してください。

    -   [NDIS 6.40 する NDIS 6.x ドライバーの移植](porting-ndis-6-x-drivers-to-ndis-6-40.md)
    -   [NDIS 6.30 する NDIS 6.x ドライバーの移植](porting-ndis-6-x-drivers-to-ndis-6-30.md)
    -   [NDIS 6.20 が動作する移植の NDIS 6.x ドライバー](porting-ndis-6-x-drivers-to-ndis-6-20.md)
    -   [NDIS 6.0 への移植の NDIS 5.x ドライバー](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)

    反復的なビルド、テスト、およびデバッグの詳細については、[概要のビルド、デバッグ、およびテスト プロセス](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)を参照してください。 このプロセスに役立つ、動作するドライバーをビルドすることを確認します。

-   手順 8:ドライバーのドライバー パッケージを作成します。

    ドライバーをインストールする方法の詳細については、[ドライバー パッケージを提供する](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_package)を参照してください。 NDIS ドライバーをインストールする方法の詳細については、[ネットワーク コンポーネントのアップグレードのインストールと](installing-and-upgrading-network-components.md)を参照してください。

-   手順 9:署名し、ドライバーを配布します。

    最後の手順では、署名し、ドライバーを配布します。 ドライバーが定義されている品質基準を満たしているかどうか、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)、Microsoft Windows 更新プログラムを通じて配布できます。 ドライバーを配布する方法の詳細については、[ドライバーを配布する](https://msdn.microsoft.com/windows-drivers/develop/distributing_a_driver_package_win8)を参照してください。

これらは、基本的な手順です。 追加の手順は、個々 のドライバーのニーズに基づいて、必要でにあります。

 

 





