---
title: NDIS プロトコル ドライバーの開発のロードマップ
description: NDIS プロトコル ドライバーの開発のロードマップ
ms.assetid: b9b8d790-7755-4c52-8a76-70257aa78212
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f042c515a5986514a85219d66d35c48d34adb82d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382174"
---
# <a name="roadmap-for-developing-ndis-protocol-drivers"></a>NDIS プロトコル ドライバーの開発のロードマップ


Network Driver Interface Specification (NDIS) プロトコルのドライバー パッケージを作成するには、次の手順を実行します。

- 手順 1:Windows アーキテクチャとドライバーについて説明します。

  Windows オペレーティング システムでのドライバーのしくみの基礎を理解する必要があります。 基礎を知ることに役立つ適切な設計上の決定を行い、開発プロセスを効率化することができます。 ドライバーの基礎の詳細については、次を参照してください。[ドライバー開発者向けのすべての概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)します。

- 手順 2:NDIS について説明します。

  概要については、NDIS および NDIS ドライバーは、次のトピックを参照してください。

  [Windows ネットワーク アーキテクチャと OSI モデル](windows-network-architecture-and-the-osi-model.md)

  [ネットワーク ドライバーのプログラミングの考慮事項](network-driver-programming-considerations.md)

  [ドライバー スタックの管理](driver-stack-management.md)

  [NET\_バッファーのアーキテクチャ](net-buffer-architecture.md)

- 手順 3:その他の Windows ドライバー設計の決定を確認します。

  その他の Windows を参照してください、設計上の決定を行う方法の詳細についての[信頼性の高いカーネル モード ドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)、 [64 ビット ドライバーのプログラミングの問題](https://docs.microsoft.com/windows-hardware/drivers/kernel/programming-issues-for-64-bit-drivers)、および[作成国際対応の INF ファイル](https://docs.microsoft.com/windows-hardware/drivers/install/creating-international-inf-files)します。

- 手順 4:Windows ドライバーのビルド、テスト、およびデバッグ プロセスおよびツールについて説明します。

  ドライバーの構築は、ユーザー モード アプリケーションの構築とは異なります。 Windows ドライバーのビルド、デバッグ、およびテスト プロセス、ドライバーの署名の詳細については、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)テストを参照してください[のビルド、デバッグ、およびドライバーのテスト](https://docs.microsoft.com/windows-hardware/drivers)します。 ビルドの詳細については、テスト、検証、およびデバッグ ツールを参照してください[ドライバー開発ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)します。

- 手順 5:プロトコル ドライバーの概要のトピックを参照してください。
  [NDIS プロトコル ドライバーの概要](introduction-to-ndis-protocol-drivers.md)
  [プロトコル ドライバー設計の概念](protocol-driver-design-concepts.md)
- 手順 6:読み取り、[書き込みプロトコル ドライバー セクション](writing-ndis-protocol-drivers.md)します。

  このセクションでは、ドライバー インターフェイスの主要なプロトコルの概要を示します。 これらのインターフェイスには、プロトコルのドライバーが提供する機能が含まれている (*ProtocolXxx*関数) と管理を開始する NDIS 呼び出し。 NDIS 提供**Ndis * Xxx*** プロトコルのドライバー呼び出し NDIS 操作を実行する関数。

- 手順 7:レビュー、 [NDIS プロトコル ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=617917)で、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります。

- 手順 8:開発 (またはポート)、ビルド、テスト、およびデバッグには、NDIS ドライバー。

  既存のドライバーを移植する場合、移植ガイドを参照してください。

  -   [NDIS 6.0 への移植の NDIS 5.x ドライバー](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)
  -   [NDIS 6.20 が動作する移植の NDIS 6.x ドライバー](porting-ndis-6-x-drivers-to-ndis-6-20.md)
  -   [NDIS 6.30 する NDIS 6.x ドライバーの移植](porting-ndis-6-x-drivers-to-ndis-6-30.md)

  反復的なビルド、テスト、およびデバッグの詳細については、次を参照してください。[概要のビルド、デバッグ、およびテスト プロセス](https://docs.microsoft.com/windows-hardware/drivers)します。 このプロセスに役立つ、動作するドライバーをビルドすることを確認します。

- 手順 9:ドライバーのドライバー パッケージを作成します。

  ドライバーをインストールする方法の詳細については、次を参照してください。[ドライバー パッケージを提供する](https://docs.microsoft.com/windows-hardware/drivers)します。 NDIS ドライバーをインストールする方法の詳細については、次を参照してください。[ネットワーク コンポーネントのアップグレードのインストールと](installing-and-upgrading-network-components.md)します。

- 手順 10:署名し、ドライバーを配布します。

  最後の手順では、(省略可能) 署名し、ドライバーを配布します。 ドライバーが定義されている品質基準を満たしているかどうか、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)、Microsoft Windows 更新プログラムを通じて配布できます。 ドライバーを配布する方法の詳細については、次を参照してください。[ドライバーを配布する](https://docs.microsoft.com/windows-hardware/drivers)します。

これらは、基本的な手順です。 追加の手順は、個々 のドライバーのニーズに基づいて、必要でにあります。

 

 





