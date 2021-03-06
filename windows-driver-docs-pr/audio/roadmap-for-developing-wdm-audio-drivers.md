---
title: WDM オーディオ ドライバーの開発のロードマップ
description: WDM オーディオ ドライバーの開発のロードマップ
ms.assetid: fa75ff65-32fe-4002-89fd-bf345502a9ac
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 418557c8a8fda820cbcb872787d3697c8d220761
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355277"
---
# <a name="roadmap-for-developing-wdm-audio-drivers"></a>WDM オーディオ ドライバーの開発のロードマップ


![テキスト"wdk"を高速道路に重ね合わせて示すロードマップの図](images/wdkroadmap-th.png)オーディオ ドライバーは、Windows driver model (WDM) に基づいています。

WDM オーディオ ドライバーを作成するには、次の手順を実行します。

1.  **Windows アーキテクチャとドライバーについて説明します。**

    Windows オペレーティング システムでのドライバーのしくみの基礎を理解する必要があります。 基本事項を把握すると、適切な設計上の決定を行い、開発プロセスを効率化することは役立ちます。 参照してください[ドライバー開発者向けのすべての概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)します。

2.  **WDM オーディオ ドライバーの基礎について説明します。**

    Windows XP から Windows Vista への Windows オペレーティング システムのバージョンでのオーディオ ドライバーでは、WDM に準拠しており、カーネルのストリーミングのコンポーネントを使用します。 必要なドライバーの設計に関する決定については、次を参照してください。[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/kernel-streaming)、 [WDM オーディオ ドライバーの概要](getting-started-with-wdm-audio-drivers.md)と[WDM オーディオ ドライバーの概要](introduction-to-wdm-audio-drivers.md)します。

3.  **追加 WDM オーディオ ドライバーの設計上の決定を確認します。**

    設計上の決定を行う方法については、次を参照してください。[カスタム オーディオ ドライバー](custom-audio-drivers.md)、[オーディオ データ形式とデータ範囲](audio-data-formats-and-data-ranges.md)します。 ヘルプの詳細を参照してください、オーディオ ドライバーの種類を決定する必要がある場合[カスタム オーディオ ドライバーの種類のデシジョン ツリー](custom-audio-driver-type-decision-tree.md)します。

4.  **オーディオ処理オブジェクトについて説明します。**

    オーディオ処理オブジェクト (APOs) は、Windows オーディオ ストリームのカスタマイズ可能なソフトウェア ベースのデジタル信号処理を提供します。 詳細についてを参照してください。 [Windows オーディオ処理オブジェクト](windows-audio-processing-objects.md)します。

5.  **Windows ドライバーのビルド、テスト、およびデバッグ プロセスおよびツールについて説明します。**

    ドライバーの構築は、ユーザー モード アプリケーションを構築することと同じではありません。 参照してください[開発、テスト、および展開ドライバー](https://docs.microsoft.com/windows-hardware/drivers) Windows ドライバーのビルド、デバッグ、およびテスト プロセス、およびドライバーの署名についてはします。 参照してください[ドライバー開発ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)については、検証、および、デバッグ ツールを構築、テストします。

6.  **オーディオ ドライバー WDK サンプルを確認します。**

    アクセスして、WDK のオーディオ ドライバーのサンプルを確認して、次を参照してください。[サンプル オーディオ ドライバー](sample-audio-drivers.md)します。

7.  **WDM、オーディオ ドライバーに関する設計上の決定を行います。**

    参照してください[オーディオ ミニポート ドライバー](audio-miniport-drivers.md)と[カーネルで COM](com-in-the-kernel.md)します。

8.  **開発、ビルド、テスト、および WDM、オーディオ ドライバーをデバッグします。**

    特定のオーディオ アダプターのオーディオ ドライバーを開発する方法については、次を参照してください。[アダプター ドライバー構築](adapter-driver-construction.md)します。 参照してください[開発、テスト、および展開ドライバー](https://docs.microsoft.com/windows-hardware/drivers)については反復的なビルド、テスト、およびデバッグします。 このプロセスに役立つ、動作するドライバーをビルドすることを確認します。

9.  **WDM、オーディオ ドライバーのドライバー パッケージを作成します。**

    詳細については、次を参照してください。[ドライバー パッケージを作成する](https://docs.microsoft.com/windows-hardware/drivers)します。 オーディオのアダプターをインストールする方法については、次を参照してください。[ポート クラス オーディオ アダプターをインストールする](installing-a-port-class-audio-adapter.md)します。

10. **署名し、WDM、オーディオ ドライバーを配布します。**

    最後の手順では、(省略可能) 署名し、ドライバーを配布します。 ドライバーが Windows 認定プログラムに対して定義されている品質基準を満たしている場合は、Microsoft Windows 更新プログラムを介して配布できます。 詳細については、次を参照してください。[ドライバー パッケージを配布する](https://docs.microsoft.com/windows-hardware/drivers)します。

これらは、基本的な手順です。 追加の手順は、個々 のドライバーのニーズに基づいて、必要でにあります。

 

 




