---
title: Windows Display Driver Model (WDDM) のためのロードマップ
description: Windows Display Driver Model (WDDM) 用ドライバーの開発のためのロードマップ
ms.assetid: 4f7ea2f4-ca2f-4b1d-97be-fb22e81c8080
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 6a408c2930d801f0d8565eb3f6b35f2878ae4d3a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553768"
---
# <a name="roadmap-for-the-windows-display-driver-model-wddm"></a>Windows Display Driver Model (WDDM) のためのロードマップ


![wddm を開発するためのロードマップを wdk のディスプレイ ドライバー](images/wdkroadmap-th.png)

Windows 表示 Driver Model (WDDM) では、グラフィックス ハードウェアの製造元が、ディスプレイ ドライバーのペアになっているユーザー モードおよびカーネル モードのディスプレイ ドライバーを指定する必要があります (または*ディスプレイ ミニポート ドライバー*)。

これらを作成するディスプレイ ドライバーで、次の手順に従います。

-   手順 1:Windows アーキテクチャとドライバーについて説明します。

    Windows オペレーティング システムでのドライバーのしくみの基礎を理解する必要があります。 基本事項を把握すると、適切な設計上の決定を行い、開発プロセスを効率化することは役立ちます。 参照してください[ドライバー開発者向けのすべての概念](https://msdn.microsoft.com/library/windows/hardware/ff554731)します。

-   手順 2:ディスプレイ ドライバーの WDDM の基礎について説明します。

    基礎を学習するを参照してください[Windows Display Driver Model (WDDM) への概要)](introduction-to-the-windows-vista-and-later-display-driver-model.md)、[ビデオ メモリ管理と GPU がスケジュール](video-memory-management-and-gpu-scheduling.md)、および[スレッド処理との同期モデル。表示のミニポート ドライバー](threading-and-synchronization-model-of-display-miniport-driver.md)します。

    最近の Windows リリースの主要な新機能の説明を参照してください。

    -   [Windows 8.1 のディスプレイ ドライバー (WDDM 1.3) の新機能については](what-s-new-for-windows-8-1-display-drivers--wddm-1-3-.md)
    -   [Windows 8 のディスプレイ ドライバー (WDDM 1.2) の新機能については](what-s-new-for-windows-8-display-drivers.md)
    -   [Windows Display Driver Model の強化 (WDDM 1.2)](https://go.microsoft.com/fwlink/p/?LinkId=226814)
-   手順 3:ユーザー モードのディスプレイ ドライバーについて説明し、問題からミニポート ドライバーの表示、[ユーザー モード ドライバーの表示](user-mode-display-drivers.md)と[複数のモニターとビデオの存在するネットワーク](multiple-monitors-and-video-present-networks.md)セクション。

-   手順 4:Windows ドライバーのビルド、テスト、およびデバッグ プロセスおよびツールについて説明します。

    ドライバーの構築は、ユーザー モード アプリケーションを構築することと同じではありません。 参照してください[開発、テスト、および展開ドライバー](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment) Windows ドライバーのビルド、デバッグ、およびテスト プロセス、ドライバーの署名、およびドライバーの検証について。 参照してください[ドライバー開発ツール](https://msdn.microsoft.com/library/windows/hardware/ff545440)については、検証、および、デバッグ ツールを構築、テストします。

-   手順 5:追加ディスプレイ ドライバーの設計に関する決定事項を作成します。

    設計上の決定を行う方法の詳細については、[実装のヒントと要件の Windows Display Driver Model (WDDM)](implementation-tips-and-requirements-for-the-windows-vista-display-dri.md)と[タスク Windows Display Driver Model (WDDM)](tasks-in-the-windows-vista-display-driver-model.md)を参照してください。

-   手順 6:アクセスして確認で WDK のディスプレイ ドライバー サンプル[表示サンプル](display-samples.md)します。

-   手順 7:開発、ビルド、テスト、および、ディスプレイ ドライバーをデバッグします。

    グラフィックス アダプターのディスプレイ ドライバーを開発する方法については、次を参照してください[初期化表示ミニポートとユーザー モード ドライバーの表示](initializing-display-miniport-and-user-mode-display-drivers.md)と[Windows 表示 Driver Model (WDDM) 操作フロー](windows-vista-and-later-display-driver-model-operation-flow.md). 参照してください[開発、テスト、および展開ドライバー](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)については反復的なビルド、テスト、およびデバッグします。 ディスプレイ ドライバー固有のヒントをデバッグするには、[Windows 表示 Driver Model (WDDM) のデバッグのヒント](debugging-tips-for-the-windows-vista-display-driver-model.md)を参照してください。 このプロセスに役立つ、動作するドライバーをビルドすることを確認します。

-   手順 8:ディスプレイ ドライバーのドライバー パッケージを作成します。

    詳細については、[ドライバー パッケージを配布する](https://msdn.microsoft.com/windows-drivers/develop/distributing_a_driver_package_win8)を参照してください。 グラフィックス アダプターのディスプレイ ドライバーをインストールする方法については、[ミニポートの表示と表示のユーザー モード ドライバーのインストール要件](installing-display-miniport-and-user-mode-display-drivers.md)を参照してください。

-   手順 9:サインインし、ディスプレイ ドライバーを配布します。

    最後の手順では、(省略可能) 署名し、ドライバーを配布します。 ドライバーがで定義されている品質基準を満たしているかどうか、 [Windows ハードウェア認定キット](https://go.microsoft.com/fwlink/p/?linkid=248337)以前の Windows Logo Kit (WLK)、Microsoft Windows 更新プログラムを通じて配布できます。 詳細については、[ドライバー パッケージを配布する](https://msdn.microsoft.com/windows-drivers/develop/distributing_a_driver_package_win8)を参照してください。

これらは、基本的な手順です。 追加の手順は、個々 のドライバーのニーズに基づいて、必要でにあります。

 

 





