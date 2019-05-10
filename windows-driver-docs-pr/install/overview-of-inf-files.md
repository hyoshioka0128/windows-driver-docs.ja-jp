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
ms.openlocfilehash: 98edaa065307af469b3cd35fd4b970c1761c41bd
ms.sourcegitcommit: 3a51ae8db61be0e25549a5527ea3143e3025e82f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65456361"
---
# <a name="overview-of-inf-files"></a>INF ファイルの概要

Windows では、セットアップ情報 (INF) ファイルを使用して、デバイスの次のコンポーネントをインストールします。

-   デバイスをサポートする 1 つまたは複数のドライバーです。

-   デバイス固有の構成またはデバイスをオンラインに設定します。

INF ファイルは、すべての情報を含むテキスト ファイルを[デバイス インストール コンポーネント](https://msdn.microsoft.com/library/windows/hardware/ff541277)ドライバーをインストールするために使用します。 Windows では、INF ファイルを使用してドライバーをインストールします。 この情報は次のとおりです。

-   ドライバーの名前と場所
-   ドライバーのバージョン情報
-   レジストリ情報

使用することができます、 *INX* INF ファイルを自動的に作成するファイル。 INX ファイルでは、バージョン情報を表す文字列変数を含む INF ファイルです。 ビルド ユーティリティと[Stampinf](https://msdn.microsoft.com/library/windows/hardware/ff552786)ツールは、特定のハードウェア アーキテクチャやフレームワークのバージョンを表すテキスト文字列で INX ファイル内の文字列変数を置き換えます。 INX ファイルの詳細については、次を参照してください。 [INX INF ファイルを作成するファイルを使用する](https://msdn.microsoft.com/library/windows/hardware/ff545473)します。


参照してください[INF ファイルのセクションとディレクティブ](inf-file-sections-and-directives.md)INF ファイル形式の詳細についてはします。
