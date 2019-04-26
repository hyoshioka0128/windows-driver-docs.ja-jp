---
title: テスト コンピューターへのテスト証明書のインストール
description: テスト コンピューターへのテスト証明書のインストール
ms.assetid: b28bd334-cd75-4ea1-8f1b-d9cd5b417b53
keywords:
- 証明書 WDK をテストします。
- インストールを実行するテスト証明書 WDK
- ドライバー パッケージを署名テスト証明書のインストール、WDK のテストします。
- 証明書ストアの WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa56bc6cf92ae4106d28cd3bfc61ea50a581a46a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352060"
---
# <a name="installing-a-test-certificate-on-a-test-computer"></a>テスト コンピューターへのテスト証明書のインストール


[テスト証明書](test-certificates.md)ドライバー ファイルの署名を埋め込むと、署名に使用される、[ドライバー パッケージの](driver-packages.md) [カタログ ファイル](catalog-files.md)に追加する必要があります、[信頼済みルート証明機関証明書ストア](trusted-root-certification-authorities-certificate-store.md)と[信頼された発行元証明書ストア](trusted-publishers-certificate-store.md)します。 使用して、テスト証明書をこれらの証明書ストアに手動で追加することができます、 [ **CertMgr** ](https://msdn.microsoft.com/library/windows/hardware/ff543411)ツール」の説明に従って[テスト証明書のインストールをテスト コンピューターでを使用してCertMgr](using-certmgr-to-install-test-certificates-on-a-test-computer.md).

ドメイン内のコンピューターにテスト証明書を自動的に展開する既定のドメイン ポリシーを構成することも[既定のドメイン ポリシーを使用してテスト証明書を展開](deploying-a-test-certificate-by-using-the-default-domain-policy.md)します。

 

 





