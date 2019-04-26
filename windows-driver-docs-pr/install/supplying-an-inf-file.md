---
title: INF ファイルの提供
description: INF ファイルの提供
ms.assetid: 208726d9-6f62-46a4-84a1-6fab3895bbe3
keywords:
- WDK のドライバー パッケージ、INF ファイル
- WDK のパッケージでは、INF ファイル
- INF ファイルの詳細については、INF ファイル、WDK
- WDK の情報ファイル
- .inf ファイル
- デバイスのインストール WDK、INF ファイル
- インストールを実行するデバイス WDK、INF ファイル
- デバイスのインストール WDK、INF ファイル
- INF ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 222e73663b9d19edac1e57e92a76eaf3eeaf0eac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339645"
---
# <a name="supplying-an-inf-file"></a>INF ファイルの提供





すべてのドライバー パッケージは、INF を含める必要がありますファイルを[デバイス インストール コンポーネント](https://msdn.microsoft.com/library/windows/hardware/ff541277)デバイスのインストール時の読み取り。 INF ファイルは、インストール スクリプトではありません。 これが ASCII または Unicode テキスト ファイル ドライバー ファイル、レジストリ エントリ、デバイスの Id など、デバイスとドライバーの情報を提供する[カタログ ファイル](catalog-files.md)、およびデバイスまたはドライバーをインストールするために必要なバージョン情報。 だけでなく、デバイスまたはドライバーのインストール時にまずもドライバー、ユーザーの要求を通じてデバイス マネージャーを更新するときに、INF が使用されます。

正確な内容と INF ファイルの形式に依存して、[デバイス セットアップ クラス](device-setup-classes.md)します。 [INF セクションの概要](summary-of-inf-sections.md)INF の種類ごとに必要な情報について説明します。 一般に、製造元ごとの情報にある、 [ **INF*モデル*セクション**](inf-models-section.md)します。 内のエントリ、**モデル**セクションを参照してください[ **INF *DDInstall*セクション**](inf-ddinstall-section.md)モデルに固有の詳細が含まれます。

[InfVerif](https://docs.microsoft.com/en-us/windows-hardware/drivers/devtest/infverif)で提供されており、ツール、 *\\ツール*ディレクトリ Microsoft Windows Driver Kit (WDK) の構文とすべてのクロス クラス INF セクションと、ディレクティブの構造を確認します。と共にプリンターを除くすべてのセットアップ クラスのクラスに固有の拡張機能。

Windows 2000 以降、すべてのバージョンの Windows オペレーティング システムにインストールするための 1 つの INF ファイルを使用できます。 詳細については、次を参照してください。 [INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)します。 デバイスは、国際市場で販売が場合は、[国際 INF ファイルを作成する](creating-international-inf-files.md)します。 関係のローカリティによっては、国際対応の INF ファイルを ASCII ではなく Unicode ファイルである必要があります。

ドライバーの INF ファイルを作成する優れた方法では、変更、WDK を提供するサンプルの 1 つです。 大部分の WDK サンプル ドライバーでは、ドライバーのサンプルと同じディレクトリの INF ファイルを含めます。

INF ファイルの詳細については、次を参照してください[INF ファイルを作成する](overview-of-inf-files.md)、ドキュメントを[InfVerif](https://docs.microsoft.com/en-us/windows-hardware/drivers/devtest/infverif)、デバイス固有のドキュメントで、WDK とサンプル ドライバーに付属している INF ファイル。自分とよく似たデバイス。

 

 





