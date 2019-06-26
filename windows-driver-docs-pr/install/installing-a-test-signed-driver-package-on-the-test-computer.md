---
title: テスト コンピューターへのテスト署名されたドライバー パッケージのインストール
description: テスト コンピューターへのテスト署名されたドライバー パッケージのインストール
ms.assetid: d825acb6-d1de-4fc5-bde2-ea27bd706f61
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2692e4e6078731430dba343d441fb6401f9a4999
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383740"
---
# <a name="installing-a-test-signed-driver-package-on-the-test-computer"></a>テスト コンピューターへのテスト署名されたドライバー パッケージのインストール


テスト署名されたをインストールする[ドライバー パッケージ](driver-packages.md)テスト コンピューターを 1 回。

-   テスト コンピューターは、テスト署名されたドライバーやドライバー パッケージをインストールする準備ができた。 詳細については、次を参照してください。[サポートのテスト署名をテスト コンピューターを構成する](configuring-the-test-computer-to-support-test-signing.md)します。

-   テスト証明書は、テスト コンピューターで信頼されたルート証明機関の証明書ストアにコピーされます。 詳細については、次を参照してください。[テスト証明書のインストール](installing-test-certificates.md)します。

テスト署名されたをインストールする[ドライバー パッケージ](driver-packages.md)によりコンピューターに。

-   [DevCon](https://docs.microsoft.com/windows-hardware/drivers/devtest/devcon)ツールで、ドライバーをインストールするための WDK コマンド ライン ツールです。

このトピックでは、ドライバー パッケージのテスト署名のプロセスをまず確認し、テスト コンピューターでドライバー パッケージをインストールする方法を説明します。 このトピックでは、 *ToastPkg*サンプル ドライバー パッケージ。 WDK のインストール ディレクトリ内で、パッケージのソース ファイル内にある、 *src\\全般\\トースター\\toastpkg*ディレクトリ。

この手順をビルドおよびテスト署名、 *ToastPkg*サンプル ドライバー パッケージ。

1.  署名のコンピューターでは、ビルド、 *ToastPkg*ドライバー パッケージのカーネル モード バイナリのサンプルです。 ドライバーを構築する方法の詳細については、次を参照してください。[ドライバーをビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)します。

2.  署名のコンピューターでは、作成、 *Contoso.com(Test)* 」の説明に従って証明書[テスト証明書を作成する](creating-test-certificates.md)します。

3.  署名のコンピューターでは、作成、[カタログ ファイル](catalog-files.md)の*ToastPkg*サンプル ドライバー パッケージの説明に従って[ドライバー パッケージのテスト署名カタログ ファイルを作成する](creating-a-catalog-file-for-test-signing-a-driver-package.md)します。

4.  テスト署名、署名のコンピューターで、 *ToastPkg* 」の説明に従って、ドライバー パッケージのカタログ ファイルをサンプル[テスト署名ドライバー パッケージのカタログ ファイル](test-signing-a-driver-package-s-catalog-file.md)します。 ドライバー パッケージを署名するときに使用して、 *Contoso.com (テスト)* から証明書、 *PrivateCertStor*e はテスト署名します。

5.  テスト署名をサポートするために、テスト コンピューターを準備する」の説明に従って[サポートをテスト署名をテスト コンピューターを構成する](configuring-the-test-computer-to-support-test-signing.md)します。

6.  コピー、 *Contoso.com(Test)* 」の説明に従って、テスト コンピューターの信頼されたルート証明機関の証明書ストアに証明書の[テスト証明書のインストール](installing-test-certificates.md)します。

次のトピックについて説明しますが、どのように*ToastPkg*サンプル ドライバー パッケージをテスト コンピューターにインストールできます。

-   [DevCon ツールを使用して、ドライバー パッケージをインストールするには](using-the-devcon-tool-to-install-a-driver-package.md)

1 回、[ドライバー パッケージ](driver-packages.md)がインストールされている場合、問題のトラブルシューティング テスト署名されたドライバーの読み込みで説明したメソッドを介して[インストールのトラブルシューティングとドライバー パッケージの署名を使用した負荷の問題](troubleshooting-install-and-load-problems-with-signed-driver-packages.md).

テスト署名されたドライバー パッケージをインストールする方法の詳細については、次を参照してください。 [Installing Test-Signed ドライバー パッケージ](installing-test-signed-driver-packages.md)します。

 

 





