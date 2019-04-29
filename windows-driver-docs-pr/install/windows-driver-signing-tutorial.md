---
title: Windows ドライバーの署名のチュートリアル
ms.assetid: B6F907DC-74DC-4BF3-A2F9-481AE706733C
description: ''
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c13a66fb8a69e2c464c12f3d59112d1462a2e40
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339263"
---
# <a name="windows-driver-signing-tutorial"></a>Windows ドライバーの署名のチュートリアル


このチュートリアルでは、概要し、統合された 1 つの場所で Windows のドライバー バイナリに署名する手順について詳しく説明します。 次のサブトピックでは、プロセスについて説明します。

[テスト署名](test-signing.md)
[リリース署名](release-signing.md)
[ドライバーのインストールの署名をトラブルシューティング](troubleshooting-driver-signing-installation.md)
[関連トピックと付録](related-topics-and-appendices.md)
## <a name="overview"></a>概要


Windows Vista 以降では、x64 ベース バージョンの Windows には、ドライバーに読み込まれるためにデジタル署名などのカーネル モードで実行されているすべてのソフトウェアが必要です。

マイクロソフトでは、ドライバーにデジタル署名を次の 2 つの方法を提供します。

1.  [Microsoft と、ドライバーの認定](https://msdn.microsoft.com/windows/hardware/gg463010.aspx)と Microsoft は、その署名を提供します。 ドライバー パッケージが認定テストに合格すると、Windows Hardware Quality Labs (WHQL) がこのドライバー パッケージに署名できるようになります。 ドライバー パッケージが WHQL によって署名されると、Windows Update プログラムや Microsoft がサポートする他の配布メカニズムによって配布することができます。
2.  ベンダーまたはドライバーの開発者は、Microsoft からのソフトウェア発行元証明書 (SPC) を取得できます証明機関 (CA) を承認し、単独でカーネル モードとユーザー モード バイナリの署名に使用します。

ブート開始の場合システムの中にドライバーを開始 (Windows Vista および Windows の以降のバージョン) のシステム ローダーによって読み込まれるドライバー、ベンダーが、ドライバーのバイナリ イメージ ファイルには埋め込むへの署名をソフトウェア発行元証明書 (SPC) の使用する必要があります。

**注**  必須のカーネル モード コード署名ポリシーは、Windows Vista 以降のバージョンの Windows で実行されている x64 ベースのシステムのカーネル モードのすべてのソフトウェアに適用されます。 ただし、発行元の 32 ビットのシステムおよびデバイス ドライバー (ユーザー モード ドライバーが含まれている) を含むすべてのカーネル モード ソフトウェアにデジタル署名をお勧めします。 Windows Vista および以降のバージョンの Windows では、32 ビット システムのカーネル モードの署名を確認します。 保護されたメディア コンテンツをサポートするソフトウェアは、32 ビットの場合でもデジタル署名する必要があります。

 

プリンター ドライバーなどのユーザー モード ドライバーはインストールし、x64 ベースのコンピューターで動作します。 ドライバーをインストールする承認を求めるインストール中に、ユーザーにダイアログが表示されます。 以降では、Windows 8 および Windows の以降のバージョンは、これらのドライバー パッケージが署名されていない場合もインストールは続行ではありません。

次のリソースは、ドライバーの署名を説明さらに詳しく説明します。

-   メイン[ドライバーの署名](driver-signing.md)トピック
-   サブトピック「方法にリリース記号、カーネル モジュール」で、[カーネル モード コード署名のチュートリアル](https://msdn.microsoft.com/library/windows/hardware/dn653569.aspx)カーネル モード コードの署名について知っておくべき内容について説明します。 ドキュメントの情報は、ユーザー モード ドライバーの署名にも適用されます。
-   Windows 7 の WDK で selfsign_readme.htm ファイルは、WDK のインストール ディレクトリにあります\\WinDDK\\7600.16385.1\\src\\全般\\ビルド\\driversigning します。 このディレクトリは、コマンド ファイルをドライバーの署名のコマンドを実行する編集可能な selfsign_example.cmd もあります。 Windows 8.1 の WDK で selfsign_readme.htm ファイルは c:\\Program Files (x86)\\Windows キット\\8.1\\bin\\selfsign、追加のドライバー署名情報へのリンクを提供します。

 

 





