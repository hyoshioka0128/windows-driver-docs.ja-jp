---
title: 署名のスコア
description: 署名のスコア
ms.assetid: 5e8dbbf8-6282-4299-80d9-5f886d01b1bf
keywords:
- 署名スコア WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e322655aab6d6b4b84cbe8dd3653a80a1932902
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538900"
---
# <a name="signature-score"></a>署名のスコア

このページには、Windows ドライバーの署名のスコアがについて説明します。 署名のスコアは、ドライバーのランクで構成される 3 つのスコアのいずれかです。 このページの情報は、Windows Vista およびそれ以降のバージョンのオペレーティング システムにのみ適用されます。

ドライバーのランクは 0 x として書式設定*SSGGTHHH*ここで、0 x の値*SS*000000 は 0x00 の値である署名スコア*GG*0000 は、[スコアの機能](feature-score--windows-vista-and-later-.md)、し、値 0x0000*THHH*は、[識別子スコア](identifier-score--windows-vista-and-later-.md)します。

署名スコアには、どのドライバーが署名されて、次の手順に従って、ドライバーが順位付けされます。

-   Windows が最適な署名スコアを割り当てます (署名スコアの最小値) に信頼された署名が含まれるドライバー。 これには、次のデータが含まれます。

    -   Premium WHQL 署名と標準 WHQL 署名します。
    -   受信トレイのドライバーの署名。
    -   Windows Sustained Engineering (Windows SE) の署名。
    -   Authenticode テクノロジを使用してサード パーティの署名。  有効なサード パーティの署名の種類を以下に示します。
        -   ドライバーの署名証明書、エンタープライズ証明機関 (CA) からコードを使用して署名します。
        -   ドライバーの署名証明書クラス 3 の CA によって発行されたコードを使用して署名します。
        -   署名証明書によって作成されたコードを使用して署名されたドライバー、 [ **MakeCert ツール**](https://msdn.microsoft.com/library/windows/hardware/ff548309)します。
-   Windows は、2 番目に適したシグネチャ スコアを割り当てます[ドライバー パッケージ](driver-packages.md)有効な署名する必要はありませんが、によってドライバーがインストールされている、 [ **INF *DDInstall*セクション**](inf-ddinstall-section.md)を持つ、 **.nt**プラットフォーム拡張機能。

    詳細については、 **.nt**拡張機能を参照してください[INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)します。

-   Windows では、有効な署名がないドライバー パッケージに第 3 の署名のスコアが割り当てられ、INF によってドライバーがインストールされていない*DDInstall*セクションを持つ、 **.nt**プラットフォーム拡張機能。

-   Windows には、4 番目と最悪の署名のスコアが割り当てられます (署名スコアの最高値) にドライバーが署名されていないか、署名の状態は不明です。

ドライバーのランク付けの詳細については、次を参照してください。[ランク ドライバーをどのように Windows](how-setup-ranks-drivers--windows-vista-and-later-.md)します。

 

 





