---
title: 作成および配置には、ユニバーサル センサー ドライバー
description: このトピックでは、記述して、ユーザー モード ドライバー フレームワーク (UMDF) バージョン 2 を使用して、ユニバーサル センサー ドライバーを展開する方法のガイダンスを提供します。
ms.assetid: FA888CB3-5B43-47CB-907D-76C6E6B6DE5D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d675023de031890dc24c4c638e0a0a344ed852a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553114"
---
# <a name="write-and-deploy-your-universal-sensor-driver"></a>作成および配置には、ユニバーサル センサー ドライバー


このトピックでは、記述して、ユーザー モード ドライバー フレームワーク (UMDF) バージョン 2 を使用して、ユニバーサル センサー ドライバーを展開する方法のガイダンスを提供します。

## <a name="write-a-generic-umdf-20-driver"></a>UMDF 2.0 の一般的なドライバーを記述します。


UMDF 2.0 の一般的なドライバーをビルドするを参照してください[ユニバーサル Windows ドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)、」の手順に従います[ユニバーサル Windows ドライバーをビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-universal-driver)ユニバーサル Windows を構築します。ドライバーを使用して、**ユーザー モード ドライバー (UMDF V2)** テンプレート。

## <a name="customize-the-generic-umdf-20-driver-fies"></a>ジェネリックの UMDF 2.0 ドライバーの修復をカスタマイズします。


開発および、この汎用 2.0 の UMDF ドライバーをビルドすると、次を含む、多くの定型的なファイルが作成されます。

-   ヘッダー ファイルを含む*Device.h*と*Driver.h*
-   ソース ファイルを含む*Device.cpp*と*Driver.cpp*

この汎用 2.0 の UMDF ドライバーをカスタマイズするときに目標は次の点に注意する必要があります。

-   [ドライバーの読み込み可能なこと](make-the-driver-loadable.md)
-   [ハードウェアへの接続します。](connect-to-hardware.md)
-   [ハードウェアからデータを読み取る](read-data-from-hardware.md)

これらの更新プログラムを作成する方法についての説明のコード スニペットは上記のトピックを参照してください。

センサー用にカスタマイズする汎用のファイルを更新した後は、次のトピックを参照してください。

-   [INX ファイルを確認してください。](review-and-revise-the-inf-file.md)
-   [センサー ドライバーをビルドします。](build-the-sensor-driver.md)
-   [センサー ドライバーをインストールします。](install-the-sensor-driver.md)

 

 




