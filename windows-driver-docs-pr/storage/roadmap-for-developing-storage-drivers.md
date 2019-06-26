---
title: Windows ストレージ ドライバーの開発のロードマップ
description: Windows ストレージ ドライバーの開発のロードマップ
ms.assetid: 67627ff9-588c-492f-861f-c592f7f92b51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80b2c4a3cffcd6707ccbdd029bd87622e961f5e4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387173"
---
# <a name="roadmap-for-developing-windows-storage-drivers"></a>Windows ストレージ ドライバーの開発のロードマップ


![テキスト"wdk"を高速道路に重ね合わせて示すロードマップの図](images/wdkroadmap-th.png)記憶装置ドライバーを作成するには、次の手順を実行します。

1.  **Windows アーキテクチャとドライバーについて説明します。**

    Windows オペレーティング システムでのドライバーのしくみの基礎を理解する必要があります。 基本事項を把握すると、適切な設計上の決定を行い、開発プロセスを効率化することは役立ちます。 参照してください[ドライバー開発者向けのすべての概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)します。

2.  **記憶装置ドライバーの基礎について説明します。**

    ストレージ ドライバーの基礎については、次を参照してください。 [Windows ストレージ ドライバーのアーキテクチャ](storage-driver-architecture.md)します。

3.  **追加のストレージ ドライバーの設計に関する決定事項を確認します。**

    設計上の決定を行う方法については、次を参照してください。 [Storport によって提供される機能](capabilities-provided-by-storport.md)、[ミニポート ドライバーの仮想記憶域。ときに、適切なでしょうか。](storage-virtual-miniport-drivers--when-are-they-appropriate-.md)、および[行う SCSI ポート ミニポート ドライバーが Storport を扱う](making-scsi-port-miniport-drivers-work-with-storport.md)します。

4.  **Windows オペレーティング システムのストレージについて説明します。**

    参照してください[Storport の履歴](history-of-storport.md)Windows Driver Kit (WDK) にします。

5.  **Windows ドライバーのビルド、テスト、およびデバッグ プロセスおよびツールについて説明します。**

    ドライバーの構築は、ユーザー モード アプリケーションを構築することと同じではありません。 参照してください[開発、テスト、および展開ドライバー](https://docs.microsoft.com/windows-hardware/drivers) Windows ドライバーのビルド、デバッグ、およびテスト プロセス、ドライバーの署名、および Windows のロゴ テストについてです。 参照してください[ドライバー開発ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)については、検証、および、デバッグ ツールを構築、テストします。

6.  **ストレージ ドライバーのサンプルを確認します。**

    アクセスおよび storport ミニポート ドライバーのサンプルは、「レビュー、 [Windows Driver Kit (WDK) サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)します。

7.  **開発、ビルド、テスト、および記憶域ドライバーをデバッグします。**

    参照してください[ドライバーをビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)、[ドライバーのテスト](https://docs.microsoft.com/windows-hardware/drivers)と[ドライバーをデバッグ](https://docs.microsoft.com/windows-hardware/drivers)については反復的なビルド、テスト、およびデバッグします。 このプロセスに役立つ、動作するドライバーをビルドすることを確認します。

8.  **ストレージ ドライバーのドライバー パッケージを作成します。**

    詳細については、次を参照してください。[ドライバー パッケージを作成する](https://docs.microsoft.com/windows-hardware/drivers)します。

9.  **署名し、配布、ストレージ** **ドライバー。**

    最後の手順では、(省略可能) 署名し、ドライバーを配布します。 ドライバーが Windows ハードウェア認定に対して定義されている品質基準を満たしている場合は、Microsoft Windows 更新プログラムを介して配布できます。 詳細については、次を参照してください。[ドライバー パッケージを配布する](https://docs.microsoft.com/windows-hardware/drivers)します。

これらは、基本的な手順です。 追加の手順は、個々 のドライバーのニーズに基づいて、必要でにあります。

 

 




