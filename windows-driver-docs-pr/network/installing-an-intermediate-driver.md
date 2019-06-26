---
title: 中間ドライバーのインストール
description: 中間ドライバーのインストール
ms.assetid: 75e299d0-b708-411d-9d37-609c8bf621f8
keywords:
- 中間ドライバー WDK ネットワー キングのインストール
- NDIS 中間ドライバー WDK をインストール
- インストールを実行する NDIS 中間ドライバー WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 514232160158532356fecd69164da2af2e52d4fa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382207"
---
# <a name="installing-an-intermediate-driver"></a>中間ドライバーのインストール





中間ドライバーでは、2 つの INF ファイルが必要です。 INF ファイルの 1 つは、プロトコルの下端のインストール パラメーターを定義します。 その他の INF ファイルでは、仮想ミニポートの上端のインストール パラメーターを定義します。

プロトコルの INF ファイルは、プライマリの INF ファイルです。 プロトコルの下端がインストールされた後、プロトコルの INF ファイルで定義されているミニポート ドライバーの INF ファイルへの参照に基づく仮想ミニポート上端がインストールされます。

Windows vista では、システムの INF ディレクトリに、ミニポート ドライバーの INF ファイルをコピーするのにには、通知オブジェクトまたはカスタム セットアップ アプリケーションを使用できます。 Windows Vista およびそれ以降のオペレーティング システム バージョンでは、使用する必要があります、 [ **INF CopyINF ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyinf-directive)ミニポート ドライバーの INF ファイルをコピーするプロトコル INF ファイル。 通知オブジェクトと INF ファイルのコピーの詳細については、次を参照してください。[中間ドライバーに通知オブジェクト](intermediate-driver-notify-object.md)します。

下端は、プロトコルのシステム提供のデバイス セットアップ クラス**NetService**中級レベルのドライバーのフィルターと**NetTrans** MUX 中間ドライバー。 仮想ミニポートのドライバーのクラスは常に**Net**します。

INF ファイルに加えて MUX 中間ドライバーを使用した通知オブジェクトを指定することも必要があります。 通知オブジェクトは、中間のフィルター ドライバーでは省略可能です。

使用して仮想ミニポート デバイスが削除、ユーザー インターフェイスから常に、 **ExcludeFromSelect**ディレクティブ。 そのため、ユーザーはのみプロトコルを認識し、プロトコルの INF ファイルからプロトコルをインストールします。

**注**  、 **ExcludeFromSelect**ディレクティブでは、仮想デバイスからは削除されません、**接続** ダイアログ ボックス。 ただし、NCF\_ミニポート ドライバーの INF ファイルの非表示フラグ*DDInstall*セクションの**特性**エントリから、ユーザーの任意の部分に表示されている仮想ミニポートを防止します。インターフェイスを含む、**接続** ダイアログ ボックス。

 

このセクションでは、中間の INF ファイルに関する情報を提供し、オブジェクトに通知します。 この情報は、次のトピックについて説明します。

[中間ドライバー UpperRange や LowerRange INF ファイルのエントリ](intermediate-driver-upperrange-and-lowerrange-inf-file-entries.md)

[MUX 中間ドライバーのインストール](mux-intermediate-driver-installation.md)

[中間ドライバー オブジェクトを通知します。](intermediate-driver-notify-object.md)

 

 





