---
title: NDIS 中間ドライバーの開発のロードマップ
description: NDIS 中間ドライバーの開発のロードマップ
ms.assetid: d3bd26ff-846f-4bd2-929c-1c15dd61a122
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96e3d077a5d883e0209b5fdf78643b99f8117ebc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382176"
---
# <a name="roadmap-for-developing-ndis-intermediate-drivers"></a>NDIS 中間ドライバーの開発のロードマップ


Network Driver Interface Specification (NDIS) 中間のドライバー パッケージを作成するには、次の手順を実行します。

-   手順 1:Windows アーキテクチャとドライバーについて説明します。

    Windows オペレーティング システムでのドライバーのしくみの基礎を理解する必要があります。 基礎を知ることに役立つ適切な設計上の決定を行い、開発プロセスを効率化することができます。 ドライバーの基礎の詳細については、次を参照してください。[ドライバー開発者向けのすべての概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)します。

-   手順 2:NDIS について説明します。

    概要については、NDIS および NDIS ドライバーは、次のトピックを参照してください。

    [Windows ネットワーク アーキテクチャと OSI モデル](windows-network-architecture-and-the-osi-model.md)

    [ネットワーク ドライバーのプログラミングの考慮事項](network-driver-programming-considerations.md)

    [ドライバー スタックの管理](driver-stack-management.md)

    [NET\_バッファーのアーキテクチャ](net-buffer-architecture.md)

-   手順 3:その他の Windows ドライバー設計の決定を確認します。

    その他の Windows を参照してください、設計上の決定を行う方法の詳細についての[信頼性の高いカーネル モード ドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)、 [64 ビット ドライバーのプログラミングの問題](https://docs.microsoft.com/windows-hardware/drivers/kernel/programming-issues-for-64-bit-drivers)、および[作成国際対応の INF ファイル](https://docs.microsoft.com/windows-hardware/drivers/install/creating-international-inf-files)します。

-   手順 4:Windows ドライバーのビルド、テスト、およびデバッグ プロセスおよびツールについて説明します。

    ドライバーの構築は、ユーザー モード アプリケーションの構築とは異なります。 Windows ドライバーのビルド、デバッグ、およびテスト プロセス、ドライバーの署名の詳細については、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)テストを参照してください[のビルド、デバッグ、およびドライバーのテスト](https://docs.microsoft.com/windows-hardware/drivers)します。 ビルドの詳細については、テスト、検証、およびデバッグ ツールを参照してください[ドライバー開発ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)します。

-   手順 5:中間ドライバー、ミニポート ドライバー、およびプロトコル ドライバーの概要のトピックを参照します。
    [NDIS 中間ドライバの概要](introduction-to-ndis-intermediate-drivers.md)
    [NDIS ミニポート ドライバーの概要](introduction-to-ndis-miniport-drivers.md)
    [NDIS ドライバーのプロトコル](ndis-protocol-drivers.md)
-   手順 6:読み取り、[書き込み中間ドライバー セクション](writing-ndis-intermediate-drivers.md)します。

    中間ドライバーでは、いくつかの中間ドライバー固有のインターフェイスに加えてプロトコル ドライバーおよびミニポート ドライバー インターフェイスの組み合わせを使用します。 オプションとして、またミニポート ドライバーを読み取るし、プロトコルのドライバーの設計ガイドできます。

-   手順 7:レビュー、 [NDIS 中間ドライバ サンプル](https://go.microsoft.com/fwlink/p/?LinkId=617916)で、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります。

-   手順 8:開発 (またはポート)、ビルド、テスト、およびデバッグには、NDIS ドライバー。

    既存のドライバーを移植する場合、移植ガイドを参照してください。

    -   [NDIS 6.0 への移植の NDIS 5.x ドライバー](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)
    -   [NDIS 6.20 が動作する移植の NDIS 6.x ドライバー](porting-ndis-6-x-drivers-to-ndis-6-20.md)
    -   [NDIS 6.30 する NDIS 6.x ドライバーの移植](porting-ndis-6-x-drivers-to-ndis-6-30.md)

    反復的なビルド、テスト、およびデバッグの詳細については、次を参照してください。[概要のビルド、デバッグ、およびテスト プロセス](https://docs.microsoft.com/windows-hardware/drivers)します。 このプロセスに役立つ、動作するドライバーをビルドすることを確認します。

-   手順 9:ドライバーのドライバー パッケージを作成します。

    ドライバーをインストールする方法の詳細については、次を参照してください。[ドライバー パッケージを提供する](https://docs.microsoft.com/windows-hardware/drivers)します。 NDIS ドライバーをインストールする方法の詳細については、次を参照してください。[ネットワーク コンポーネントのアップグレードのインストールと](installing-and-upgrading-network-components.md)します。

-   手順 10:署名し、ドライバーを配布します。

    最後の手順では、(省略可能) 署名し、ドライバーを配布します。 ドライバーが定義されている品質基準を満たしているかどうか、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)、Microsoft Windows 更新プログラムを通じて配布できます。 ドライバーを配布する方法の詳細については、次を参照してください。[ドライバーを配布する](https://docs.microsoft.com/windows-hardware/drivers)します。

これらは、基本的な手順です。 追加の手順は、個々 のドライバーのニーズに基づいて、必要でにあります。

 

 





