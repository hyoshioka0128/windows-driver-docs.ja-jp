---
title: NDIS ミニポート ドライバーの開発のロードマップ
description: NDIS ミニポート ドライバーの開発のロードマップ
ms.assetid: 7cb56c08-3578-49d7-a0aa-a89dc6b139ca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3118cb4e151e255639a2aa28ea361925a407ad51
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386852"
---
# <a name="roadmap-for-developing-ndis-miniport-drivers"></a>NDIS ミニポート ドライバーの開発のロードマップ


Network Driver Interface Specification (NDIS) ミニポート ドライバー パッケージを作成するには、次の手順を実行します。

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

- 手順 5:ミニポート ドライバーの概要のトピックを参照してください。
  [種類の NDIS ミニポート ドライバー](types-of-ndis-miniport-drivers.md)
  [ネットワーク インターフェイス カードのサポート](network-interface-card-support.md)
  [ミニポート ドライバー コードの重要な機能](important-features-of-miniport-driver-code.md)
   [サンプル NDIS ミニポート ドライバー](sample-ndis-miniport-drivers.md)
- 手順 6:読み取り、[書き込みミニポート ドライバー セクション](writing-ndis-miniport-drivers.md)します。

  このセクションでは、ドライバー インターフェイス プライマリ ミニポートの概要を示します。 これらのインターフェイスには、ミニポート ドライバーが提供する機能が含まれている (*MiniportXxx*関数) と管理を開始する NDIS 呼び出し。 NDIS 提供**Ndis * Xxx*** NDIS 操作を実行するそのミニポート ドライバーの呼び出しに機能します。

- 手順 7:レビュー、 [NDIS ミニポート ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=617918)で、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります。

- 手順 8: (省略可能な読み取り) 追加の考慮事項、ミニポート ドライバー。

  追加の考慮事項が記載されているプライマリ インターフェイス上に展開されるトピックを含む、[書き込みミニポート ドライバー セクション](writing-ndis-miniport-drivers.md)します。

  [取得して、ミニポート ドライバーの情報と、WMI の NDIS サポートの設定](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)

  [NDIS MSI-X](ndis-msi-x.md)

  [NDIS スキャッター/ギャザー DMA](ndis-scatter-gather-dma.md)

  [NDIS 電源管理](ndis-power-management.md)

  [NDIS ミニポート ドライバーのプラグ アンド プレイ](plug-and-play-for-ndis-miniport-drivers.md)

  [リセット、停止、シャット ダウン関数](reset--halt--and-shutdown-functions.md)

  [WDM 低いインターフェイスを備えたミニポート ドライバー](https://docs.microsoft.com/windows-hardware/drivers/network/miniport-drivers-with-a-wdm-lower-interface)

  [WAN ミニポート ドライバー](wan-miniport-drivers.md)

  [スケーラブル ネットワーク](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

- 手順 9:開発 (またはポート)、ビルド、テスト、およびデバッグには、NDIS ドライバー。

  既存のドライバーを移植する場合、移植ガイドを参照してください。

  -   [NDIS 6.0 への移植の NDIS 5.x ドライバー](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)
  -   [NDIS 6.20 が動作する移植の NDIS 6.x ドライバー](porting-ndis-6-x-drivers-to-ndis-6-20.md)
  -   [NDIS 6.30 する NDIS 6.x ドライバーの移植](porting-ndis-6-x-drivers-to-ndis-6-30.md)

  反復的なビルド、テスト、およびデバッグの詳細については、次を参照してください。[概要のビルド、デバッグ、およびテスト プロセス](https://docs.microsoft.com/windows-hardware/drivers)します。 このプロセスに役立つ、動作するドライバーをビルドすることを確認します。

- 手順 10:ドライバーのドライバー パッケージを作成します。

  ドライバーをインストールする方法の詳細については、次を参照してください。[ドライバー パッケージを提供する](https://docs.microsoft.com/windows-hardware/drivers)します。 NDIS ドライバーをインストールする方法の詳細については、次を参照してください。[ネットワーク コンポーネントのアップグレードのインストールと](installing-and-upgrading-network-components.md)します。

- 手順 11:署名し、ドライバーを配布します。

  最後の手順では、(省略可能) 署名し、ドライバーを配布します。 ドライバーが定義されている品質基準を満たしているかどうか、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)、Microsoft Windows 更新プログラムを通じて配布できます。 ドライバーを配布する方法の詳細については、次を参照してください。[ドライバーを配布する](https://docs.microsoft.com/windows-hardware/drivers)します。

これらは、基本的な手順です。 追加の手順は、個々 のドライバーのニーズに基づいて、必要でにあります。

 

 





