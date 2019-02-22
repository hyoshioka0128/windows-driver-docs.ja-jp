---
title: Winsock カーネルとネットワーク ドライバーを開発するためのロードマップ
description: Winsock カーネルとネットワーク ドライバーを開発するためのロードマップ
ms.assetid: f94952c3-02b1-4bd2-bd73-e6d6d42a06fb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e4c42e9936fb4f948af432bf9d5803f9b7e5cc6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538178"
---
# <a name="roadmap-for-developing-network-drivers-with-winsock-kernel"></a>Winsock カーネルとネットワーク ドライバーを開発するためのロードマップ


プログラミング機能は、Winsock カーネル (WSK) のカーネル モード ソケットを使用するネットワークのドライバー パッケージを作成するには、次の手順を実行します。

-   **手順 1:** Windows アーキテクチャとドライバーについて説明します。

    Windows オペレーティング システムでのドライバーのしくみの基礎を理解する必要があります。 基礎を知ることに役立つ適切な設計上の決定を行い、開発プロセスを効率化することができます。 ドライバーの基礎の詳細については、次を参照してください。[ドライバー開発者向けのすべての概念](https://msdn.microsoft.com/library/windows/hardware/ff554731)します。

-   **手順 2:** Network Driver Interface Specification (NDIS) について説明します。

    ドライバー パッケージは、Network Driver Interface Specification (NDIS) インターフェイスを使用して通常します。 NDIS および NDIS の詳細については、ミニポート ドライバーは、次のトピックを参照してください。

    [Windows ネットワーク アーキテクチャと OSI モデル](windows-network-architecture-and-the-osi-model.md)

    [NDIS ミニポート ドライバー](ndis-miniport-drivers.md)

    [書き込みの NDIS ミニポート ドライバー](writing-ndis-miniport-drivers.md)

    [ネットワーク ドライバーのプログラミングの考慮事項](network-driver-programming-considerations.md)

-   **手順 3:** ドライバーを使用する追加のネットワーク コンポーネントを決定します。

    NDIS の主要な機能だけでなく、ハードウェア構成によっては、カーネル モード ドライバーで次の追加の Windows ネットワーク コンポーネントを使用できます。

    [IP ヘルパー](ip-helper.md)

    [Windows フィルタ リング プラットフォーム コールアウト ドライバー](introduction-to-windows-filtering-platform-callout-drivers.md)

    [ネイティブの 802.11 ワイヤレス LAN](https://msdn.microsoft.com/library/windows/hardware/ff560689)

    [モバイル ブロード バンド ネットワーク インターフェイス](mb-interface-overview.md)

-   **手順 4:** Winsock Kernel の基礎について説明します。

    Winsock カーネルは、Windows Vista および Windows の以降のバージョンでサポートされます。 Winsock カーネルを使用する方法については、次を参照してください。 [Winsock Kernel 概要](introduction-to-winsock-kernel.md)します。

    ネットワークのドライバーで使用できる、単純化しより汎用的なネットワーク プログラミング インターフェイスが[ネットワーク モジュールのレジストラー](network-module-registrar2.md)します。

-   **手順 5:** その他の Windows ドライバー設計の決定を確認します。

    その他の Windows を参照してください、設計上の決定を行う方法については[信頼性の高いカーネル モード ドライバーの作成](https://msdn.microsoft.com/library/windows/hardware/ff542904)、 [64 ビット ドライバーのプログラミング問題](https://msdn.microsoft.com/library/windows/hardware/ff559923)、および[作成国際対応の INF ファイル](https://msdn.microsoft.com/library/windows/hardware/ff540208)します。

-   **手順 6:** Windows ドライバーのビルド、テスト、およびデバッグ プロセスおよびツールについて説明します。

    ドライバーの構築は、ユーザー モード アプリケーションの構築とは異なります。 については、Windows ドライバーのビルド、デバッグ、およびテスト プロセス、ドライバーの署名、および[Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)テストを参照してください[のビルド、デバッグ、およびドライバーのテスト](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)します。 ビルドするためのツールについては、テスト、検証、およびデバッグするを参照してください[ドライバー開発ツール](https://msdn.microsoft.com/library/windows/hardware/ff545440)します。

-   **手順 7:** レビュー、 [Winsock カーネル (WSK TCP エコー サーバー) ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=617935)で、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります。

-   **手順 8:** 開発、ビルド、テスト、およびドライバーをデバッグします。

    反復的なビルド、テスト、およびデバッグについては、次を参照してください。[概要のビルド、デバッグ、およびテスト プロセス](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)します。 このプロセスにより、動作するドライバーを作成することを確認します。

-   **手順 9:** ドライバーのドライバー パッケージを作成します。

    ドライバーをインストールする方法については、次を参照してください。[ドライバー パッケージを提供する](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_package)します。

-   **手順 10:** 署名し、ドライバーを配布します。

    最後の手順では、(省略可能) 署名し、ドライバーを配布します。 ドライバーが定義されている品質基準を満たしているかどうか、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)、Microsoft Windows 更新プログラムを通じて配布できます。 ドライバーを配布する方法の詳細については、次を参照してください。[ドライバーを配布する](https://msdn.microsoft.com/windows-drivers/develop/distributing_a_driver_package_win8)します。

これらは、基本的な手順です。 追加の手順は、個々 のドライバーのニーズに基づいて、必要でにあります。

 

 





