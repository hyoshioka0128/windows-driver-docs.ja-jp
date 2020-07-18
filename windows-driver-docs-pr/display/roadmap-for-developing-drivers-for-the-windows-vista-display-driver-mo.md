---
title: Windows Display Driver Model (WDDM) のためのロードマップ
description: Windows Display Driver Model (WDDM) 用ドライバーを開発するためのロードマップ
ms.assetid: 4f7ea2f4-ca2f-4b1d-97be-fb22e81c8080
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: c6ebef19ed83695b36c4d1dddf184daea88028e9
ms.sourcegitcommit: 0d89fc46058efb2ebc6ed9bd8f638c3f8cc1a678
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2020
ms.locfileid: "86459248"
---
# <a name="road-map-for-the-windows-display-driver-model-wddm"></a>Windows Display Driver Model (WDDM) のためのロードマップ

![wddm ディスプレイドライバーを開発するための wdk ロードマップ](images/wdkroadmap-th.png)

Windows Display Driver Model (WDDM) では、グラフィックスハードウェアベンダーが、ユーザーモードのディスプレイドライバーとカーネルモードのディスプレイドライバー (または、*ミニポートドライバーを表示*) をペアリングする必要があります。

これらの表示ドライバーを作成するには、次の手順を実行します。

- 手順 1: Windows のアーキテクチャとドライバーについて説明します。

  Windows オペレーティングシステムでのドライバーの動作の基礎を理解しておく必要があります。 基本を理解することで、適切な設計上の決定を行い、開発プロセスを効率化することができます。 [すべてのドライバー開発者向けの概念を](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)ご覧ください。

- 手順 2: WDDM ディスプレイドライバーの基礎について説明します。

  基本については、「 [Windows Display Driver Model (WDDM) の概要](introduction-to-the-windows-vista-and-later-display-driver-model.md)」を参照してください)、[ビデオメモリ管理と GPU スケジューリング](video-memory-management-and-gpu-scheduling.md)、および[ディスプレイミニポートドライバーのスレッドと同期モデル](threading-and-synchronization-model-of-display-miniport-driver.md)を参照してください。

    最新の Windows リリースの新機能の詳細については、「 [windows 10 のディスプレイドライバーとグラフィックスドライバーの新](https://docs.microsoft.com/windows-hardware/drivers/display/what-s-new-for-windows-10-display-and-graphics-drivers)機能」を参照してください。

- 手順 3: ユーザーモード表示ドライバーと問題について説明します。これには、[ユーザーモードの [ディスプレイドライバー](user-mode-display-drivers.md) ] と [[複数のモニター] および [ビデオの現在のネットワーク](multiple-monitors-and-video-present-networks.md)] セクションからのミニポートドライバーが表示されます。

- 手順 4: Windows ドライバーのビルド、テスト、およびデバッグのプロセスとツールについて説明します。

  ドライバーのビルドは、ユーザーモードアプリケーションのビルドと同じではありません。 Windows ドライバーのビルド、デバッグ、およびテストプロセス、ドライバーの署名、およびドライバーの検証に関する情報については、「[ドライバーの開発、テスト、および展開](https://docs.microsoft.com/windows-hardware/drivers/develop/)」を参照してください。 ツールのビルド、テスト、検証、およびデバッグについては、「[ドライバー開発ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)」を参照してください。

- 手順 5: ディスプレイドライバーの設計に関するその他の決定を行います。

  設計に関する決定事項については、「windows display driver [model (wddm) の実装に関するヒントと要件](implementation-tips-and-requirements-for-the-windows-vista-display-dri.md)」および「 [Windows display DRIVER model (wddm)」](tasks-in-the-windows-vista-display-driver-model.md)を参照してください。

- 手順 6:[ディスプレイドライバーのサンプル](display-samples.md)にアクセスして確認します。

- 手順 7: ディスプレイドライバーを開発、ビルド、テスト、およびデバッグします。

  グラフィックスアダプターの表示ドライバーを開発する方法の詳細については、「[ディスプレイミニポートの初期化」および「ユーザーモードの表示ドライバー](initializing-display-miniport-and-user-mode-display-drivers.md) 」および「 [Windows display DRIVER Model (WDDM) の操作フロー](windows-vista-and-later-display-driver-model-operation-flow.md)」を参照してください。 反復的なビルド、テスト、およびデバッグについては、「[ドライバーの開発、テスト、および配置](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。 ディスプレイドライバーに固有のデバッグのヒントについては、「 [WDDM ドライバーのデバッグのヒント](debugging-tips-for-wddm-drivers.md)」を参照してください。 このプロセスを使用すると、動作するドライバーを確実にビルドできます。

- 手順 8: ディスプレイドライバーのドライバーパッケージを作成します。

  詳細については、「[ドライバーパッケージの配布](https://docs.microsoft.com/windows-hardware/drivers/develop/distributing-a-driver-package-win8)」を参照してください。 グラフィックスアダプターの表示ドライバーをインストールする方法の詳細については、「[表示ミニポートのインストール要件」および「ユーザーモードの表示ドライバー](installing-display-miniport-and-user-mode-display-drivers.md)」を参照してください。

- 手順 9: 表示ドライバーに署名して配布します。

  最後の手順は、署名 (オプション) し、ドライバーを配布することです。 ドライバーが[Windows ハードウェアラボキット](https://docs.microsoft.com/windows-hardware/test/hlk/)(以前の Windows ロゴキットまたは WLK) で定義されている品質基準を満たしている場合は、Microsoft Windows Update プログラムを通じて配布できます。 詳細については、「[ドライバーパッケージの配布](https://docs.microsoft.com/windows-hardware/drivers/develop/distributing-a-driver-package-win8)」を参照してください。

基本的な手順は次のとおりです。 個々のドライバーのニーズに基づいて、追加の手順が必要になる場合があります。
