---
title: INF ファイルの概要
description: INF ファイルの概要
ms.assetid: 94682cba-1f68-416f-af74-99ede81eadc7
keywords:
- INF ファイル WDK デバイスのインストール
- INF ファイル WDK デバイスのインストールを作成します。
- デバイス セットアップ WDK デバイスのインストール、INF ファイル
- デバイスのインストール WDK、INF ファイル
- インストールを実行するデバイス WDK、INF ファイル
- INF ファイルを使用してドライバーをインストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7baa663e05c87ee19208eef04bf788944be02cb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374981"
---
# <a name="overview-of-inf-files"></a>INF ファイルの概要

Windows では、セットアップ情報 (INF) ファイルを使用して、デバイスの次のコンポーネントをインストールします。

-   デバイスをサポートする 1 つまたは複数のドライバーです。

-   デバイス固有の構成またはデバイスをオンラインに設定します。

INF ファイルは、すべての情報を含むテキスト ファイルを[デバイス インストール コンポーネント](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))ドライバーをインストールするために使用します。 Windows では、INF ファイルを使用してドライバーをインストールします。 この情報は次のとおりです。

-   ドライバーの名前と場所
-   ドライバーのバージョン情報
-   レジストリ情報

使用することができます、 *INX* INF ファイルを自動的に作成するファイル。 INX ファイルでは、バージョン情報を表す文字列変数を含む INF ファイルです。 ビルド ユーティリティと[Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf)ツールは、特定のハードウェア アーキテクチャやフレームワークのバージョンを表すテキスト文字列で INX ファイル内の文字列変数を置き換えます。 INX ファイルの詳細については、次を参照してください。 [INX INF ファイルを作成するファイルを使用する](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-inx-files-to-create-inf-files)します。


参照してください[INF ファイルのセクションとディレクティブ](inf-file-sections-and-directives.md)INF ファイル形式の詳細についてはします。
