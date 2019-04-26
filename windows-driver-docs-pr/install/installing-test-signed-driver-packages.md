---
title: テスト署名されたドライバー パッケージのインストール
description: テスト署名されたドライバー パッケージのインストール
ms.assetid: 6abbe51c-0fdf-465f-b1f2-d48e593a4f0e
keywords:
- テスト署名ドライバー WDK、テスト署名されたドライバー パッケージのインストール
- ドライバー WDK、ドライバー パッケージの署名
- ドライバー WDK、ドライバー パッケージの署名
- WDK、ドライバー パッケージのデジタル署名
- WDK、ドライバー パッケージの署名
- ドライバー パッケージのデジタル署名 WDK
- パッケージのデジタル署名 WDK
- テスト署名ドライバー WDK、ドライバー パッケージ
- WDK テスト署名されたドライバー パッケージのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec819f268b48609a7d1529d033da5857f1d06349
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360028"
---
# <a name="installing-test-signed-driver-packages"></a>テスト署名されたドライバー パッケージのインストール


テスト署名済み、Windows Vista と共に登場した[ドライバー パッケージ](driver-packages.md)インストールして、次の条件に該当する場合に、ユーザーの介入なし読み込む必要があります。

-   ドライバー パッケージは、Windows Vista の一般的な要件と以降のバージョンの Windows に準拠します。

-   ドライバー パッケージは署名され、署名は検証」の説明に従って[ドライバー パッケージのテスト署名](test-signing-driver-packages.md)します。

-   署名が後に、ドライバー パッケージは変更されません。

-   ドライバー パッケージの署名に使用されたテスト証明書が正しくインストールされて、テスト コンピューターでの説明に従って[テスト コンピューターにテスト証明書をインストールする](installing-a-test-certificate-on-a-test-computer.md)します。

-   非 PnP ドライバーが署名付き[カタログ ファイル](catalog-files.md)埋め込みの署名ではなく、ドライバーをインストールするインストール アプリケーションがカタログ ファイル システム カタログのルート ディレクトリでの説明に従ってインストール[非 PnP ドライバーのテスト署名済みカタログ ファイルをインストールする](installing-a-test-signed-catalog-file-for-a-non-pnp-driver.md)します。

-   テスト コンピューターで、テスト署名を有効になっています。 詳細については、次を参照してください。 [TESTSIGNING ブートの構成オプション](the-testsigning-boot-configuration-option.md)します。

テスト署名されたドライバー パッケージをインストールする方法の概要については、次を参照してください。 [Test-Signed ドライバー パッケージをテスト コンピューターにインストールする](installing-a-test-signed-driver-package-on-the-test-computer.md)します。

インストールに関する問題のトラブルシューティングを行う方法の詳細については、次を参照してください。[インストールのトラブルシューティングと負荷の問題のドライバー パッケージの署名に](troubleshooting-install-and-load-problems-with-signed-driver-packages.md)します。

 

 





