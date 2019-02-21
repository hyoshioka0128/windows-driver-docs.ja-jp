---
title: ドライバー パッケージをプレインストールします。
description: ドライバー パッケージをプレインストールします。
ms.assetid: aba794ac-ab24-486a-9f5a-7e8435056bb7
keywords:
- インストール アプリケーション WDK、プレインストールのドライバー パッケージ
- デバイスのインストール アプリケーション WDK、プレインストールのドライバー パッケージ
- プレインストールされているドライバー WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bab22ad61f4e685d8ed73d7fe3fc6ef6380add9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549208"
---
# <a name="preinstalling-driver-packages"></a>ドライバー パッケージをプレインストールします。





ドライバーのファイルをプレインストールする、*デバイス インストール アプリケーション*次の手順に従う必要があります。

1.  ターゲット システムで、ドライバー ファイルのディレクトリを作成します。 デバイスのインストール アプリケーションでは、アプリケーションをインストールする場合、ドライバー ファイルをアプリケーション ディレクトリのサブディレクトリに格納する必要があります。

2.  すべてのファイルをコピー、[ドライバー パッケージ](driver-packages.md)(1) の手順で作成されるディレクトリに、配布メディアから。 ドライバー パッケージには、ドライバーまたはドライバー、INF ファイル、カタログ ファイル、およびその他のインストール ファイルが含まれています。

3.  呼び出す[SetupCopyOEMInf](https://go.microsoft.com/fwlink/p/?linkid=98735) (1) の手順で作成されたディレクトリの INF ファイルを指定します。 指定の SPOST_PATH、 *OEMSourceMediaType*パラメーター指定と**NULL**の*OEMSourceMediaLocation*パラメーター。 [SetupCopyOEMInf](https://go.microsoft.com/fwlink/p/?linkid=194252)にパッケージをドライバーの INF ファイルをコピー、 *%systemroot%\\Inf*ディレクトリ、ターゲット システムに Windows の一覧に含めず、INF ファイルのソースの場所を格納するように指示と前処理済みの INF ファイル。 [SetupCopyOEMInf](https://go.microsoft.com/fwlink/p/?linkid=194252)も PnP マネージャー ドライバー インストールは、次回、INF ファイルに記載されているデバイスを認識しているため、カタログ ファイルを処理します。

PnP マネージャーが、デバイスの認識、によってコピー INF ファイルを検索、デバイス、ユーザーが接続されるときに[SetupCopyOEMInf](https://go.microsoft.com/fwlink/p/?linkid=194252)ドライバーの (2) の手順でコピーしてインストールします。 (INF ファイルをコピーする方法の詳細については、次を参照してください[コピー Inf](copying-inf-files.md)。)。

 

 





