---
title: Storport ミニポート ドライバーの開発のロードマップ
description: Storport ミニポート ドライバーの開発のロードマップ
ms.assetid: 43a8f1ee-b2d3-4f97-b7e5-d59790ca6754
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d671327880d03c3c9c5c119dbc49428fa4515659
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387172"
---
# <a name="roadmap-for-developing-storport-miniport-drivers"></a>Storport ミニポート ドライバーの開発のロードマップ


![テキスト"wdk"を高速道路に重ね合わせて示すロードマップの図](images/wdkroadmap-th.png)Storport ミニポート ドライバーを作成するには、次の手順を実行します。

1.  **Windows アーキテクチャとドライバーについて説明します。**

    Windows でのドライバーのしくみの基礎を理解することが重要です。 基本事項を把握すると、適切な設計上の決定を行い、開発プロセスを効率化することは役立ちます。 参照してください[ドライバー開発者向けのすべての概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)します。

2.  **Storport ミニポート ドライバーの基礎について説明します。**

    Storport ミニポート ドライバーの基礎については、次を参照してください[Windows ストレージ ドライバーのアーキテクチャ](storage-driver-architecture.md)、 [Storport によって提供される機能](capabilities-provided-by-storport.md)、および[Storport ミニポートに Storport のインターフェイス。ドライバー](storport-s-interface-with-storport-miniport-drivers.md)します。

3.  **追加 storport ミニポート ドライバーの設計に関する決定事項を確認します。**

    設計上の決定を行う方法については、次を参照してください。 [Storport によって提供される機能](capabilities-provided-by-storport.md)、 [Storport のインターフェイスは、記憶域クラス ドライバーを](storport-s-interface-with-the-storage-class-driver.md)、[ミニポート ドライバーの仮想記憶域。ときに、適切なでしょうか。](storage-virtual-miniport-drivers--when-are-they-appropriate-.md)、および[行う SCSI ポート ミニポート ドライバーが Storport を扱う](making-scsi-port-miniport-drivers-work-with-storport.md)します。

4.  **Windows Vista 以降のオペレーティング システムで storport ミニポート ドライバーについて説明します。**

    参照してください[Storport の履歴](history-of-storport.md)Windows Driver Kit (WDK) にします。

5.  **Windows ドライバーのビルド、テスト、およびデバッグ プロセスおよびツールについて説明します。**

    ドライバーの構築は、ユーザー モード アプリケーションを構築することと同じではありません。 参照してください[開発、テスト、および展開ドライバー](https://docs.microsoft.com/windows-hardware/drivers) Windows ドライバーのビルド、デバッグ、およびテスト プロセス、ドライバーの署名、および Windows のロゴ テストについてです。 参照してください[ドライバー開発ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)については、検証、および、デバッグ ツールを構築、テストします。

6.  **Storport ミニポート ドライバーのサンプルを確認します。**

    アクセスおよび storport ミニポート ドライバーのサンプルは、「レビュー、 [Windows Driver Kit (WDK) サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)します。

7.  **開発、ビルド、テスト、および storport ミニポート ドライバーをデバッグします。**

    参照してください[ドライバーをビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)、[ドライバーのテスト](https://docs.microsoft.com/windows-hardware/drivers)と[ドライバーをデバッグ](https://docs.microsoft.com/windows-hardware/drivers)については反復的なビルド、テスト、およびデバッグします。 このプロセスに役立つ、動作するドライバーをビルドすることを確認します。

8.  **Storport ミニポート ドライバーのドライバー パッケージを作成します。**

    詳細については、次を参照してください。[ドライバー パッケージを作成する](https://docs.microsoft.com/windows-hardware/drivers)します。

9.  **署名し、配布、storport ミニポート** **ドライバー。**

    最後の手順では、(必要に応じて) にサインインし、ドライバーを配布します。 ドライバーが Windows ハードウェア認定に対して定義されている品質基準を満たしている場合は、Microsoft Windows 更新プログラムを介して配布できます。 詳細については、次を参照してください。[ドライバー パッケージを配布する](https://docs.microsoft.com/windows-hardware/drivers)します。

これらは、基本的な手順です。 追加の手順は、個々 のドライバーのニーズに基づいて、必要でにあります。

 

 




