---
title: インストール コンポーネントの概要
description: インストール コンポーネントの概要
ms.assetid: 29d14a3a-e89a-47ef-bd36-ee3cdcde2cd7
keywords:
- ドライバー パッケージ WDK をインストールするコンポーネント
- WDK をインストールするコンポーネントのパッケージ
- ドライバーのインストールに必要な情報、WDK
- オペレーティング システムの WDK、ドライバーのインストール情報
- ドライバー WDK、必要な情報をインストールします。
- インストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d72b0060c69fa6b7bd3df118b51699e727c31bcb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574327"
---
# <a name="installation-component-overview"></a>インストール コンポーネントの概要





[デバイス インストールの概要](overview-of-device-and-driver-installation.md)セクションでは、Microsoft Windows オペレーティング システムの検出し、デバイスとドライバーのインストールでは、このようなインストールに関連するコンポーネントで、詳細を示します。

デバイスまたはドライバーをインストールするには、オペレーティング システムには、少なくとも次の情報が必要です。

-   デバイスまたはドライバーがサポートされている各オペレーティング システムの名前とバージョン番号

-   デバイスのセットアップ クラス GUID とセットアップ クラス

-   ドライバーのバージョン情報

-   元とコピー先の場所と共に、ドライバー ファイルの名前

-   デバイスに固有の情報を含む[ハードウェア ID](hardware-ids.md)と[互換性 Id](compatible-ids.md)

-   名前、[カタログ (.cat) ファイル](catalog-files.md)

-   方法についての情報と使用すると、各ドライバー (Windows 2000 および Windows の以降のバージョン) によって提供されるサービスを読み込む

デバイスの INF ファイルでは、すべての情報を指定できます。 ほとんどのデバイスとドライバーの組み合わせに対して、INF ファイルは、必要なのみのインストール コンポーネントです。 すべてのデバイスとドライバー、INF ファイルを必要とします。 詳細については、次を参照してください。 [、INF ファイルを指定して](supplying-an-inf-file.md)します。

システムのブート時に、デバイスが関係している場合は、インストールの要件が異なります。 参照してください[ブート ドライバーをインストールする](installing-a-boot-start-driver.md)します。

 

 





