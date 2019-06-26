---
title: MB ミニポート ドライバーの開発のロードマップ
description: MB ミニポート ドライバーの開発のロードマップ
ms.assetid: 3ef6e899-22dc-4293-80cc-d786b03c6b29
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93f444c121fa0680e2feaf3539b3acd1fd48750c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382163"
---
# <a name="roadmap-to-develop-mb-miniport-drivers"></a>MB ミニポート ドライバーの開発のロードマップ


MB のミニポート ドライバーを作成するには、次の手順を実行します。

-   **手順 1**:Windows アーキテクチャとミニポート ドライバーについて説明します。

    Windows オペレーティング システムでのドライバーのしくみの基礎を理解する必要があります。 基礎を知ることに役立つ適切な設計上の決定を行い、開発プロセスを効率化することができます。 ドライバーの基礎の詳細については、次を参照してください。[ドライバー開発者向けのすべての概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)します。

-   **手順 2**:MB のミニポート ドライバーの基礎について説明します。

    MB のミニポート ドライバーが Windows 7 および Windows の以降のバージョンではサポートされているし、に準拠している、 *NDIS 6.20 が動作仕様*します。 行う必要があります、ミニポート ドライバー設計の決定については、次を参照してください。 [NDIS 6.20 が動作の概要](introduction-to-ndis-6-20.md)します。

-   **手順 3**:その他の Windows ドライバー設計の決定を確認します。

    その他の Windows を参照してください、設計上の決定を行う方法については[信頼性の高いカーネル モード ドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)、 [64 ビット ドライバーのプログラミング問題](https://docs.microsoft.com/windows-hardware/drivers/kernel/programming-issues-for-64-bit-drivers)、および[作成国際対応の INF ファイル](https://docs.microsoft.com/windows-hardware/drivers/install/creating-international-inf-files)します。

-   **手順 4**:Windows ドライバーのビルド、テスト、およびデバッグ プロセスおよびツールについて説明します。

    ドライバーの構築は、ユーザー モード アプリケーションの構築とは異なります。 については、Windows ドライバーのビルド、デバッグ、およびテスト プロセス、ドライバーの署名、および[Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)テストを参照してください[のビルド、デバッグ、およびドライバーのテスト](https://docs.microsoft.com/windows-hardware/drivers)します。 ビルドの詳細については、テスト、検証、およびデバッグ ツールを参照してください[ドライバー開発ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)します。

-   **手順 5**:MB ミニポート ドライバーに関する設計上の決定を行います。

    詳細については、次を参照してください。 [MB インターフェイスの概要](mb-interface-overview.md)します。 説明を確認して、モバイル ブロード バンドのミニポート ドライバーを開発する方法についても、[モバイル ブロード バンド ドライバー開発](https://go.microsoft.com/fwlink/p/?linkid=144416)ホワイト ペーパー。

-   **手順 6**:開発、ビルド、テスト、および MB ミニポート ドライバーをデバッグします。

    反復的なビルド、テスト、およびデバッグについては、次を参照してください。[概要のビルド、デバッグ、およびテスト プロセス](https://docs.microsoft.com/windows-hardware/drivers)します。 このプロセスに役立つ、動作するミニポート ドライバーをビルドすることを確認します。

-   **手順 7**:MB ミニポート ドライバーのドライバー パッケージを作成します。

    詳細については、次を参照してください。[ドライバー パッケージを提供する](https://docs.microsoft.com/windows-hardware/drivers)します。

-   **手順 8**:サインインし、MB、ミニポート ドライバーを配布します。

    最後の手順では、(省略可能) 署名し、ミニポート ドライバーを配布します。 ミニポート ドライバーが定義されている品質基準を満たしているかどうか、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)、Microsoft Windows 更新プログラムを通じて配布できます。 ドライバーを配布する方法の詳細については、次を参照してください。[ドライバーを配布する](https://docs.microsoft.com/windows-hardware/drivers)します。

これらは、基本的な手順です。 追加の手順は、個々 のミニポート ドライバーのニーズに基づいて、必要でにあります。

 

 





