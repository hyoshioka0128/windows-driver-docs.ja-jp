---
title: INF ファイルの概要
description: INF ファイルの概要
ms.assetid: 94682cba-1f68-416f-af74-99ede81eadc7
keywords:
- INF ファイル WDK デバイスのインストール
- INF ファイル WDK デバイスのインストール、作成
- デバイスセットアップ WDK デバイスのインストール、INF ファイル
- デバイスのインストール WDK、INF ファイル
- デバイスのインストール WDK, INF ファイル
- INF ファイルを使用してドライバーをインストールする
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 78dfa6c2a5df5e01417f0bf53275fbe3a1c4a98d
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007586"
---
# <a name="overview-of-inf-files"></a>INF ファイルの概要

Windows では、セットアップ情報 (INF) ファイルを使用して、デバイスの次のコンポーネントをインストールします。

-   デバイスをサポートする1つまたは複数のドライバー。

-   デバイスをオンラインにするためのデバイス固有の構成または設定。

INF ファイルは、ドライバーのインストールに使用される[デバイスインストールコンポーネント](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))に関するすべての情報を含むテキストファイルです。 Windows は INF ファイルを使用してドライバーをインストールします。 この情報には、次のものが含まれます。

-   ドライバーの名前と場所
-   ドライバーのバージョン情報
-   レジストリ情報

*INX*ファイルを使用して、INF ファイルを自動的に作成することができます。 INX ファイルは、バージョン情報を表す文字列変数を含む INF ファイルです。 ビルドユーティリティと[Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf)ツールは、INX ファイル内の文字列変数を、特定のハードウェアアーキテクチャまたはフレームワークのバージョンを表すテキスト文字列に置き換えます。 INX ファイルの詳細については、「 [USING INX files To CREATE INF files](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-inx-files-to-create-inf-files)」を参照してください。


INF ファイル形式の詳細については、「 [Inf ファイルのセクションとディレクティブ](inf-file-sections-and-directives.md)」を参照してください。
