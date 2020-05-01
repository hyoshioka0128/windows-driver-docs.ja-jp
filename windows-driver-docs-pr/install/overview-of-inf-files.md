---
title: INF ファイルの概要
description: INF ファイルの概要
ms.assetid: 94682cba-1f68-416f-af74-99ede81eadc7
keywords:
- INF ファイル WDK デバイスのインストール
- INF ファイル WDK デバイスのインストール、作成
- デバイスのセットアップ WDK デバイスのインストール、INF ファイル
- デバイスのインストール WDK、INF ファイル
- デバイス WDK のインストール、INF ファイル
- INF ファイルを使用してドライバーをインストールする
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 78dfa6c2a5df5e01417f0bf53275fbe3a1c4a98d
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "72007586"
---
# <a name="overview-of-inf-files"></a>INF ファイルの概要

Windows では、セットアップ情報 (INF) ファイルを使用して、デバイスの次のコンポーネントをインストールします。

-   デバイスをサポートする 1 つまたは複数のドライバー。

-   デバイスをオンラインにするためのデバイス固有の構成または設定。

INF ファイルは、ドライバーのインストールの際に[デバイス インストール コンポーネント](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))で使用されたすべての情報が含まれるテキスト ファイルです。 Windows では、INF ファイルを使用してドライバーがインストールされます。 この情報には、次のものが含まれます。

-   ドライバー名と場所
-   ドライバーのバージョン情報
-   レジストリ情報

*INX* ファイルを使用して、INF ファイルを自動的に作成できます。 INX ファイルは、バージョン情報を表す文字列変数が含まれる INF ファイルです。 ビルド ユーティリティと [Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf) ツールを使用すると、INX ファイル内の文字列変数が、特定のハードウェア アーキテクチャまたはフレームワークのバージョンを表すテキスト文字列に置き換えられます。 INX ファイルの詳細については、「[INX ファイルを使用した INF ファイルの作成](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-inx-files-to-create-inf-files)」を参照してください。


INF ファイル形式に関する詳細な説明については、「[INF のファイルのセクションとディレクティブ](inf-file-sections-and-directives.md)」を参照してください。
