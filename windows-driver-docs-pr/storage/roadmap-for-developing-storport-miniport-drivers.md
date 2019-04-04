---
title: Storport ミニポート ドライバーの開発のロードマップ
description: Storport ミニポート ドライバーの開発のロードマップ
ms.assetid: 43a8f1ee-b2d3-4f97-b7e5-d59790ca6754
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d84cab27320605a441ad26690264ba75178e3959
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570142"
---
# <a name="roadmap-for-developing-storport-miniport-drivers"></a>Storport ミニポート ドライバーの開発のロードマップ


![テキスト"wdk"を高速道路に重ね合わせて示すロードマップの図](images/wdkroadmap-th.png)Storport ミニポート ドライバーを作成するには、次の手順を実行します。

1.  **Windows アーキテクチャとドライバーについて説明します。**

    Windows でのドライバーのしくみの基礎を理解することが重要です。 基本事項を把握すると、適切な設計上の決定を行い、開発プロセスを効率化することは役立ちます。 参照してください[ドライバー開発者向けのすべての概念](https://msdn.microsoft.com/library/windows/hardware/ff554731)します。

2.  **Storport ミニポート ドライバーの基礎について説明します。**

    Storport ミニポート ドライバーの基礎については、次を参照してください[Windows ストレージ ドライバーのアーキテクチャ](storage-driver-architecture.md)、 [Storport によって提供される機能](capabilities-provided-by-storport.md)、および[Storport ミニポートに Storport のインターフェイス。ドライバー](storport-s-interface-with-storport-miniport-drivers.md)します。

3.  **追加 storport ミニポート ドライバーの設計に関する決定事項を確認します。**

    設計上の決定を行う方法については、次を参照してください。 [Storport によって提供される機能](capabilities-provided-by-storport.md)、 [Storport のインターフェイスは、記憶域クラス ドライバーを](storport-s-interface-with-the-storage-class-driver.md)、[ミニポート ドライバーの仮想記憶域。ときに、適切なでしょうか。](storage-virtual-miniport-drivers--when-are-they-appropriate-.md)、および[行う SCSI ポート ミニポート ドライバーが Storport を扱う](making-scsi-port-miniport-drivers-work-with-storport.md)します。

4.  **Windows Vista 以降のオペレーティング システムで storport ミニポート ドライバーについて説明します。**

    参照してください[Storport の履歴](history-of-storport.md)Windows Driver Kit (WDK) にします。

5.  **Windows ドライバーのビルド、テスト、およびデバッグ プロセスおよびツールについて説明します。**

    ドライバーの構築は、ユーザー モード アプリケーションを構築することと同じではありません。 参照してください[開発、テスト、および展開ドライバー](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment) Windows ドライバーのビルド、デバッグ、およびテスト プロセス、ドライバーの署名、および Windows のロゴ テストについてです。 参照してください[ドライバー開発ツール](https://msdn.microsoft.com/library/windows/hardware/ff545440)については、検証、および、デバッグ ツールを構築、テストします。

6.  **Storport ミニポート ドライバーのサンプルを確認します。**

    アクセスおよび storport ミニポート ドライバーのサンプルは、「レビュー、 [Windows Driver Kit (WDK) サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)します。

7.  **開発、ビルド、テスト、および storport ミニポート ドライバーをデバッグします。**

    参照してください[ドライバーをビルド](https://msdn.microsoft.com/windows-drivers/develop/building_a_driver)、[ドライバーのテスト](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver)と[ドライバーをデバッグ](https://msdn.microsoft.com/windows-drivers/develop/debugging_a_driver)については反復的なビルド、テスト、およびデバッグします。 このプロセスに役立つ、動作するドライバーをビルドすることを確認します。

8.  **Storport ミニポート ドライバーのドライバー パッケージを作成します。**

    詳細については、[ドライバー パッケージを作成する](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_package)を参照してください。

9.  **署名し、配布、storport ミニポート****ドライバー。**

    最後の手順では、(必要に応じて) にサインインし、ドライバーを配布します。 ドライバーが Windows ハードウェア認定に対して定義されている品質基準を満たしている場合は、Microsoft Windows 更新プログラムを介して配布できます。 詳細については、[ドライバー パッケージを配布する](https://msdn.microsoft.com/windows-drivers/develop/distributing_a_driver_package_win8)を参照してください。

これらは、基本的な手順です。 追加の手順は、個々 のドライバーのニーズに基づいて、必要でにあります。

 

 




