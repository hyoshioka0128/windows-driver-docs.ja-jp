---
title: NDIS フィルター ドライバーの開発のロードマップ
description: NDIS フィルター ドライバーの開発のロードマップ
ms.assetid: 346dae93-4cb7-4cb5-a2cf-41be9809fec2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0abc1e52ab5c874ec4a552446718e5ad6e39e231
ms.sourcegitcommit: b7971067b64ffa9162bfedc263ce4de53dcbe9b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74832873"
---
# <a name="roadmap-for-developing-ndis-filter-drivers"></a>NDIS フィルター ドライバーの開発のロードマップ


Network Driver Interface Specification (NDIS) フィルタードライバーパッケージを作成するには、次の手順を実行します。

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

  ドライバーのビルドは、ユーザーモードアプリケーションの作成とは異なります。 Windows ドライバーのビルド、デバッグ、およびテストプロセス、ドライバー署名、および[Windows ハードウェア互換性](https://docs.microsoft.com/windows-hardware/design/compatibility/)テストの詳細については、「[ドライバーのビルド、デバッグ、およびテスト](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。 ツールのビルド、テスト、検証、およびデバッグの詳細については、「[ドライバー開発ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)」を参照してください。

- 手順 5:[フィルタードライバーの概要に関するトピック](introduction-to-ndis-filter-drivers.md)を参照してください。

- 手順 6:[プロトコルドライバーの記述](writing-ndis-miniport-drivers.md)に関するセクションを参照してください。

  ここでは、プライマリプロトコルドライバーインターフェイスの概要について説明します。 これらのインターフェイスには、プロトコルドライバーによって提供される関数 (*Protocolxxx*関数) と、操作を開始するための NDIS 呼び出しが含まれています。 Ndis は、プロトコルドライバーが ndis 操作を実行するために呼び出す**ndis * Xxx*** 関数を提供します。

- 手順 7: GitHub の[Windows ドライバーサンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)リポジトリで、 [NDIS フィルタードライバーのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=617915)を確認します。

- 手順 8: NDIS ドライバーの開発 (またはポート)、ビルド、テスト、およびデバッグを行います。

  既存のドライバーを移植する場合は、移植に関するガイドを参照してください。

  -   [Ndis 5.x ドライバーを NDIS 6.0 に移植する](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)
  -   [Ndis 6. x ドライバーを NDIS 6.20 に移植する](porting-ndis-6-x-drivers-to-ndis-6-20.md)
  -   [Ndis 6. x ドライバーを NDIS 6.30 に移植する](porting-ndis-6-x-drivers-to-ndis-6-30.md)

  反復的なビルド、テスト、およびデバッグの詳細については、「[ビルド、デバッグ、およびテストのプロセスの概要](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。 このプロセスを使用すると、動作するドライバーを確実にビルドできます。

- 手順 9: ドライバーのドライバーパッケージを作成する

  ドライバーのインストール方法の詳細については、「[ドライバーパッケージの提供](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。 NDIS ドライバーをインストールする方法の詳細については、「[ネットワークコンポーネントのインストールとアップグレード](installing-and-upgrading-network-components.md)」を参照してください。

- 手順 10: ドライバーに署名して配布します。

  最後の手順は、署名 (オプション) し、ドライバーを配布することです。 ドライバーが[Windows Hardware 互換性プログラム](https://docs.microsoft.com/windows-hardware/design/compatibility/)に対して定義されている品質基準を満たしている場合は、Microsoft Windows Update プログラムを通じて配布できます。 ドライバーを配布する方法の詳細については、「[ドライバーの配布](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。

基本的な手順は次のとおりです。 個々のドライバーのニーズに基づいて、追加の手順が必要になる場合があります。

 

 





