---
title: 非 PnP ドライバー用のテスト署名されたカタログ ファイルのインストール
description: 非 PnP ドライバー用のテスト署名されたカタログ ファイルのインストール
ms.assetid: 8586bacc-86c5-4402-84fa-6f1efe967f5d
keywords:
- テスト署名ドライバー パッケージ WDK、カタログ ファイル
- CAT ファイル
- .cat ファイル
- 非 PnP ドライバー カタログ ファイル WDK ドライバー署名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d18dc1a027f69224aeed0c3456200685b7133d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383743"
---
# <a name="installing-a-test-signed-catalog-file-for-a-non-pnp-driver"></a>非 PnP ドライバー用のテスト署名されたカタログ ファイルのインストール


準拠する、[カーネル モード コードの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)埋め込みの署名または符号付き 64 ビット バージョンの Windows Vista と Windows、以外のブートでの以降のバージョンの非 PnP ドライバーが必要[のカタログファイル](catalog-files.md)システム コンポーネントおよびドライバー データベースにインストールされています。 PnP デバイスのインストールは、ドライバー データベースでの PnP ドライバー カタログ ファイルを自動的にインストールされます。 ただし、非 PnP ドライバーでは、非 PnP ドライバーをインストールするインストール アプリケーション インストールする必要があります、カタログ ファイル ドライバー データベース。

ドライバーのインストール アプリケーションを使用して、システム コンポーネントおよびドライバー データベースでカタログ ファイルをプログラムでインストールできます、 [CryptCATAdminAddCatalog](https://go.microsoft.com/fwlink/p/?linkid=104926)暗号関数です。 アプリケーションは、再頒布可能パッケージには、このアプローチを使用して、カタログ ファイルをインストールする必要があります。 この方法の詳細については、次を参照してください。 [CryptCATAdminAddCatalog を使用して、カタログ ファイルをインストールする](installing-a-catalog-file-by-using-cryptcatadminaddcatalog.md)します。

また、使用することができます、 [ **SignTool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)をインストールするためのツール、[カタログ ファイル](catalog-files.md)システム コンポーネントおよびドライバー データベースでします。 ただし、SignTool は再頒布可能パッケージ ツールではありません。 そのため、インストール アプリケーション使用できます SignTool コンピューターで、ツールが、ツールのマイクロソフト ソフトウェア ライセンス条項に準拠している方法でコンピューターに既にインストールされている場合にのみ。 この方法の詳細については、次を参照してください。 [SignTool を使用して、カタログ ファイルをインストールする](installing-a-catalog-file-by-using-signtool.md)します。

**ヒント:**   署名済みカタログ ファイルを使用して一般的により簡単かつよりも効率的には埋め込み署名を使用します。 詳細については、長所と短所の埋め込み署名を使用して、署名済みカタログ ファイルとは、次を参照してください。[テスト署名ドライバー](https://docs.microsoft.com/windows-hardware/drivers)します。

 

 

 





