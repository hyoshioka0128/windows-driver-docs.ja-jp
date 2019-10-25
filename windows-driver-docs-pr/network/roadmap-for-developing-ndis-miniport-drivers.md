---
title: NDIS ミニポート ドライバーの開発のロードマップ
description: NDIS ミニポート ドライバーの開発のロードマップ
ms.assetid: 7cb56c08-3578-49d7-a0aa-a89dc6b139ca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4524f11bed854352543f2a69e6252404f18a8430
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842010"
---
# <a name="roadmap-for-developing-ndis-miniport-drivers"></a>NDIS ミニポート ドライバーの開発のロードマップ


Network Driver Interface Specification (NDIS) ミニポートドライバーパッケージを作成するには、次の手順を実行します。

- 手順 1: Windows のアーキテクチャとドライバーについて説明します。

  Windows オペレーティングシステムでのドライバーの動作の基礎を理解しておく必要があります。 基本を理解することで、適切な設計上の決定を行い、開発プロセスを効率化することができます。 ドライバーの基礎の詳細については、「[すべてのドライバー開発者向けの概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)」を参照してください。

- 手順 2: NDIS について説明します。

  NDIS および NDIS ドライバーに関する一般的な情報については、次のトピックを参照してください。

  [Windows ネットワークアーキテクチャと OSI モデル](windows-network-architecture-and-the-osi-model.md)

  [ネットワークドライバーのプログラミングに関する考慮事項](network-driver-programming-considerations.md)

  [ドライバースタックの管理](driver-stack-management.md)

  [NET\_のバッファーアーキテクチャ](net-buffer-architecture.md)

- 手順 3: その他の Windows ドライバーの設計上の決定を決定する。

  Windows の設計に関するその他の決定を行う方法の詳細については、「[信頼性の高いカーネルモードドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)」、「 [64 ビットドライバーのプログラミングに関する問題](https://docs.microsoft.com/windows-hardware/drivers/kernel/programming-issues-for-64-bit-drivers)」、および「[国際対応の INF ファイルの作成](https://docs.microsoft.com/windows-hardware/drivers/install/creating-international-inf-files)」を参照してください。

- 手順 4: Windows ドライバーのビルド、テスト、およびデバッグのプロセスとツールについて説明します。

  ドライバーのビルドは、ユーザーモードアプリケーションの作成とは異なります。 Windows ドライバーのビルド、デバッグ、テストプロセス、ドライバー署名、および[Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)テストの詳細については、「[ドライバーのビルド、デバッグ、およびテスト](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。 ツールのビルド、テスト、検証、およびデバッグの詳細については、「[ドライバー開発ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)」を参照してください。

- 手順 5: ミニポートドライバーの概要に関するトピックを参照してください。
  [Ndis ミニポートドライバーの種類](types-of-ndis-miniport-drivers.md)
  [ネットワークインターフェイスカードのサポート](network-interface-card-support.md)
  [ミニポートドライバーコードの重要な機能](important-features-of-miniport-driver-code.md)
  [サンプル ndis ミニポートドライバー](sample-ndis-miniport-drivers.md)
- 手順 6:[ミニポートドライバーの記述](writing-ndis-miniport-drivers.md)に関するセクションを参照してください。

  ここでは、プライマリミニポートドライバーインターフェイスの概要について説明します。 これらのインターフェイスには、ミニポートドライバーによって提供される関数 (*Miniportxxx*関数) と、操作を開始するための NDIS 呼び出しが含まれています。 Ndis には、ミニポートドライバーが NDIS 操作を実行するために呼び出す**ndis * Xxx*** 関数が用意されています。

- 手順 7: GitHub の[Windows ドライバーサンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)リポジトリで、 [NDIS ミニポートドライバーのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=617918)を確認します。

- 手順 8: (オプションの読み取り) ミニポートドライバーに関する追加の考慮事項。

  追加の考慮事項には、 [「ミニポートドライバーの記述」セクション](writing-ndis-miniport-drivers.md)で説明されている主要なインターフェイスを展開するトピックが含まれます。

  [ミニポートドライバー情報の取得と設定、および WMI の NDIS サポート](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)

  [NDIS MSI-X](ndis-msi-x.md)

  [NDIS スキャッター/ギャザー DMA](ndis-scatter-gather-dma.md)

  [NDIS 電源管理](ndis-power-management.md)

  [NDIS ミニポートドライバーのプラグアンドプレイ](plug-and-play-for-ndis-miniport-drivers.md)

  [Reset、Halt、および Shutdown 関数](reset--halt--and-shutdown-functions.md)

  [WDM インターフェイスがあるミニポートドライバー](https://docs.microsoft.com/windows-hardware/drivers/network/miniport-drivers-with-a-wdm-lower-interface)

  [WAN ミニポートドライバー](wan-miniport-drivers.md)

  [スケーラブル ネットワーク](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

- 手順 9: NDIS ドライバーの開発 (またはポート)、ビルド、テスト、およびデバッグを行います。

  既存のドライバーを移植する場合は、移植に関するガイドを参照してください。

  -   [Ndis 5.x ドライバーを NDIS 6.0 に移植する](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)
  -   [Ndis 6. x ドライバーを NDIS 6.20 に移植する](porting-ndis-6-x-drivers-to-ndis-6-20.md)
  -   [Ndis 6. x ドライバーを NDIS 6.30 に移植する](porting-ndis-6-x-drivers-to-ndis-6-30.md)

  反復的なビルド、テスト、およびデバッグの詳細については、「[ビルド、デバッグ、およびテストのプロセスの概要](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。 このプロセスを使用すると、動作するドライバーを確実にビルドできます。

- 手順 10: ドライバーのドライバーパッケージを作成します。

  ドライバーのインストール方法の詳細については、「[ドライバーパッケージの提供](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。 NDIS ドライバーをインストールする方法の詳細については、「[ネットワークコンポーネントのインストールとアップグレード](installing-and-upgrading-network-components.md)」を参照してください。

- 手順 11: ドライバーに署名して配布する。

  最後の手順は、署名 (オプション) し、ドライバーを配布することです。 ドライバーが、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)に定義されている品質基準を満たしている場合は、Microsoft Windows Update プログラムを通じて配布できます。 ドライバーを配布する方法の詳細については、「[ドライバーの配布](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。

基本的な手順は次のとおりです。 個々のドライバーのニーズに基づいて、追加の手順が必要になる場合があります。

 

 





