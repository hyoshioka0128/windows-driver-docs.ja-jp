---
title: WFP コールアウト ドライバーの開発のロードマップ
description: WFP コールアウト ドライバーの開発のロードマップ
ms.assetid: 98c857d9-e4a6-4a7f-8427-642763864f3e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8a32ae092cee3034371070c5f0b91d719689d72
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842009"
---
# <a name="roadmap-for-developing-wfp-callout-drivers"></a>WFP コールアウト ドライバーの開発のロードマップ


Windows Filtering Platform (WFP) コールアウトドライバーを作成するには、次の手順を実行します。

-   手順 1: WFP アーキテクチャについて説明します。

    WFP の詳細については、「 [Windows Filtering Platform](https://docs.microsoft.com/windows/desktop/FWP/windows-filtering-platform-start-page)」を参照してください。 WFP ユーザーモードアプリケーションを開発して、WFP コールアウトドライバーを記述しないようにすることができます。

-   手順 2: Windows のアーキテクチャとドライバーについて説明します。

    Windows オペレーティングシステムでのドライバーの動作の基礎を理解しておく必要があります。 基本を理解することで、適切な設計上の決定を行い、開発プロセスを効率化することができます。 ドライバーの基礎の詳細については、「[すべてのドライバー開発者向けの概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)」を参照してください。

-   手順 3: WFP コールアウトドライバーの Windows ドライバーモデルを決定します。

    WFP コールアウトドライバーは、Windows Driver Model (WDM) またはカーネルモードドライバーフレームワーク (KMDF) を使用して書き込むことができます。 ドライバーモデルを選択する方法の詳細については、「[ドライバーモデルの](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)選択」を参照してください。 WDM の詳細については、「 [Windows ドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-windows-drivers)」および「 [Wdm ドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-wdm-drivers)」を参照してください。 KMDF の詳細については、「 [WDF Driver Development Guide](https://docs.microsoft.com/windows-hardware/drivers/wdf/design-guide)」を参照してください。

-   手順 4: Windows ドライバーの設計に関するその他の決定を決定する

    Windows の設計に関するその他の決定を行う方法については、「[信頼性の高いカーネルモードドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)」、「 [64 ビットドライバーのプログラミングに関する問題](https://docs.microsoft.com/windows-hardware/drivers/kernel/programming-issues-for-64-bit-drivers)」、および「[国際対応の INF ファイルの作成](https://docs.microsoft.com/windows-hardware/drivers/install/creating-international-inf-files)」を参照してください。

-   手順 5: Windows ドライバーのビルド、テスト、およびデバッグのプロセスとツールについて説明します。

    ドライバーのビルドは、ユーザーモードアプリケーションの作成とは異なります。 Windows ドライバーのビルド、デバッグ、テストプロセス、ドライバー署名、および[Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)テストの詳細については、「[ドライバーのビルド、デバッグ、およびテスト](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。 ツールのビルド、テスト、検証、およびデバッグの詳細については、「[ドライバー開発ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)」を参照してください。

-   手順 6: GitHub の[windows ドライバーサンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)リポジトリで、 [windows FILTERING Platform (WFP) ドライバーのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=618680)を確認します。

-   手順 7: WFP コールアウトドライバーについて設計上の決定を行います。

    WFP コールアウトドライバーを設計する方法の詳細については、「[コールアウトドライバーのプログラミングに関する考慮事項](callout-driver-programming-considerations.md)」を参照してください。

-   手順 8: WFP コールアウトドライバーを開発、ビルド、テスト、およびデバッグします。

    WFP コールアウトドライバーの詳細については、「[コールアウト](callout-driver-operations.md)ドライバーの操作」および「[コールアウトドライバーのインストール](callout-driver-installation.md)」を参照してください。 WFP に固有の関数、構造体、列挙型、または定数の詳細については、「 [Windows フィルタリングプラットフォームのコールアウトドライバーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。 反復的なビルド、テスト、およびデバッグの詳細については、「[ビルド、デバッグ、およびテストのプロセスの概要](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。 このプロセスを使用すると、動作するドライバーを確実にビルドできます。

-   手順 9: WFP コールアウトドライバーのドライバーパッケージを作成する

    詳細については、「ドライバーパッケージと[コールアウトドライバーのインストール](callout-driver-installation.md)[を指定する](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。

-   手順 10: WFP コールアウトドライバーに署名して配布します。

    最後の手順は、署名 (オプション) し、ドライバーを配布することです。 ドライバーが、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)に定義されている品質基準を満たしている場合は、Microsoft Windows Update プログラムを通じて配布できます。 ドライバーを配布する方法の詳細については、「[ドライバーの配布](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。

基本的な手順は次のとおりです。 個々のドライバーのニーズに基づいて、追加の手順が必要になる場合があります。

 

 





