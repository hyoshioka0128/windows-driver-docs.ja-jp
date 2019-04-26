---
title: 非 PnP ドライバー用のリリース署名されたカタログ ファイルのインストール
description: 非 PnP ドライバー用のリリース署名されたカタログ ファイルのインストール
ms.assetid: a67f3b71-b7a6-4712-a76f-b3b412a149c2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5893789273a46615f428b354d3eadbe63f56b36
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352056"
---
# <a name="installing-a-release-signed-catalog-file-for-a-non-pnp-driver"></a>非 PnP ドライバー用のリリース署名されたカタログ ファイルのインストール


準拠する、[カーネル モード コードの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)埋め込まれたリリース署名または署名されたリリースのいずれかの64ビットバージョンのWindowsVista以降のバージョンのWindows、以外のブート、非PnPのカーネルモードドライバーが必要[カタログ ファイル](catalog-files.md)システム コンポーネントおよびドライバー データベースにインストールされています。 さらに、リリース署名済みカタログ ファイルをユーザー モード ドライバーまたは 32 ビット非 PnP カーネル モード ドライバーの認証に使用する場合、Windows のコード署名ポリシーが必要です、システム コンポーネントおよびドライバー データベースでカタログ ファイルをインストールすること。 PnP デバイスのインストールは、ドライバー データベースでの PnP ドライバー カタログ ファイルを自動的にインストールされます。 ただし、非 PnP ドライバーでは、非 PnP ドライバーをインストールするインストール アプリケーション インストールする必要があります、カタログ ファイル ドライバー データベース。

パブリックに公開されている非 PnP ドライバーのカタログ ファイルをインストールする再頒布可能パッケージのインストール アプリケーションを使用する必要があります、 [CryptCATAdminAddCatalog](https://go.microsoft.com/fwlink/p/?linkid=104926) 」の説明に従って、暗号化関数[インストールします。CryptCATAdminAddCatalog を使用してファイルをカタログ](installing-a-catalog-file-by-using-cryptcatadminaddcatalog.md)します。

**注**  再頒布可能パッケージのインストール アプリケーションを一般に、使用することはできません、 [ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778) SignTool は再頒布可能パッケージ ツールではないため、カタログ ファイルをインストールするためのツール.

 

**ヒント:**   署名済みカタログ ファイルを使用して一般的により簡単かつよりも効率的には埋め込み署名を使用します。 詳細については、長所と短所の埋め込み署名を使用して、署名済みカタログ ファイルとは、次を参照してください。[テスト署名ドライバー](https://msdn.microsoft.com/windows-drivers/develop/signing_a_driver)します。

 

 

 





