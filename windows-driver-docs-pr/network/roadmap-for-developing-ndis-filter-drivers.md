---
title: NDIS フィルター ドライバーの開発のロードマップ
description: NDIS フィルター ドライバーの開発のロードマップ
ms.assetid: 346dae93-4cb7-4cb5-a2cf-41be9809fec2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71a208e56b4e873c441d523350d15d01414967af
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377524"
---
# <a name="roadmap-for-developing-ndis-filter-drivers"></a>NDIS フィルター ドライバーの開発のロードマップ


Network Driver Interface Specification (NDIS) フィルター ドライバー パッケージを作成するには、次の手順を実行します。

- 手順 1:Windows アーキテクチャとドライバーについて説明します。

  Windows オペレーティング システムでのドライバーのしくみの基礎を理解する必要があります。 基礎を知ることに役立つ適切な設計上の決定を行い、開発プロセスを効率化することができます。 ドライバーの基礎の詳細については、次を参照してください。[ドライバー開発者向けのすべての概念](https://msdn.microsoft.com/library/windows/hardware/ff554731)します。

- 手順 2:NDIS について説明します。

  概要については、NDIS および NDIS ドライバーは、次のトピックを参照してください。

  [Windows ネットワーク アーキテクチャと OSI モデル](windows-network-architecture-and-the-osi-model.md)

  [ネットワーク ドライバーのプログラミングの考慮事項](network-driver-programming-considerations.md)

  [ドライバー スタックの管理](driver-stack-management.md)

  [NET\_バッファーのアーキテクチャ](net-buffer-architecture.md)

- 手順 3:その他の Windows ドライバー設計の決定を確認します。

  その他の Windows を参照してください、設計上の決定を行う方法の詳細についての[信頼性の高いカーネル モード ドライバーの作成](https://msdn.microsoft.com/library/windows/hardware/ff542904)、 [64 ビット ドライバーのプログラミングの問題](https://msdn.microsoft.com/library/windows/hardware/ff559923)、および[作成国際対応の INF ファイル](https://msdn.microsoft.com/library/windows/hardware/ff540208)します。

- 手順 4:Windows ドライバーのビルド、テスト、およびデバッグ プロセスおよびツールについて説明します。

  ドライバーの構築は、ユーザー モード アプリケーションの構築とは異なります。 Windows ドライバーのビルド、デバッグ、およびテスト プロセス、ドライバーの署名の詳細については、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)テストを参照してください[のビルド、デバッグ、およびドライバーのテスト](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)します。 ビルドの詳細については、テスト、検証、およびデバッグ ツールを参照してください[ドライバー開発ツール](https://msdn.microsoft.com/library/windows/hardware/ff545440)します。

- 手順 5:読み取り、[フィルター ドライバーの概要トピック](introduction-to-ndis-filter-drivers.md)します。

- 手順 6:読み取り、[書き込みプロトコル ドライバー セクション](writing-ndis-miniport-drivers.md)します。

  このセクションでは、ドライバー インターフェイスの主要なプロトコルの概要を示します。 これらのインターフェイスには、プロトコルのドライバーが提供する機能が含まれている (*ProtocolXxx*関数) と管理を開始する NDIS 呼び出し。 NDIS 提供**Ndis * Xxx*** プロトコルのドライバー呼び出し NDIS 操作を実行する関数。

- 手順 7:レビュー、 [NDIS フィルター ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=617915)で、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります.

- 手順 8:開発 (またはポート)、ビルド、テスト、およびデバッグには、NDIS ドライバー。

  既存のドライバーを移植する場合、移植ガイドを参照してください。

  -   [NDIS 6.0 への移植の NDIS 5.x ドライバー](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)
  -   [NDIS 6.20 が動作する移植の NDIS 6.x ドライバー](porting-ndis-6-x-drivers-to-ndis-6-20.md)
  -   [NDIS 6.30 する NDIS 6.x ドライバーの移植](porting-ndis-6-x-drivers-to-ndis-6-30.md)

  反復的なビルド、テスト、およびデバッグの詳細については、次を参照してください。[概要のビルド、デバッグ、およびテスト プロセス](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)します。 このプロセスに役立つ、動作するドライバーをビルドすることを確認します。

- 手順 9:ドライバーのドライバー パッケージを作成します。

  ドライバーをインストールする方法の詳細については、次を参照してください。[ドライバー パッケージを提供する](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_package)します。 NDIS ドライバーをインストールする方法の詳細については、次を参照してください。[ネットワーク コンポーネントのアップグレードのインストールと](installing-and-upgrading-network-components.md)します。

- 手順 10:署名し、ドライバーを配布します。

  最後の手順では、(省略可能) 署名し、ドライバーを配布します。 ドライバーが定義されている品質基準を満たしているかどうか、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)、Microsoft Windows 更新プログラムを通じて配布できます。 ドライバーを配布する方法の詳細については、次を参照してください。[ドライバーを配布する](https://msdn.microsoft.com/windows-drivers/develop/distributing_a_driver_package_win8)します。

これらは、基本的な手順です。 追加の手順は、個々 のドライバーのニーズに基づいて、必要でにあります。

 

 





