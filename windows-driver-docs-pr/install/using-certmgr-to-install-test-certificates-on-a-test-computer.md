---
title: テスト コンピューターへの CertMgr を使用したテスト証明書のインストール
description: テスト コンピューターへの CertMgr を使用したテスト証明書のインストール
ms.assetid: 5928c810-65e8-412e-9723-7b371574006c
keywords:
- Certmgr ツール
- 証明書マネージャー ツールを WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b542250b705fdb4faaf1ac70e31d46b05089e7b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384771"
---
# <a name="using-certmgr-to-install-test-certificates-on-a-test-computer"></a>テスト コンピューターへの CertMgr を使用したテスト証明書のインストール


使用して、テスト コンピューターにテスト証明書をインストールする[ **CertMgr**](https://docs.microsoft.com/windows-hardware/drivers/devtest/certmgr)、これらの手順に従います。

1.  証明書のコピー ( *.cer*) に使用したファイルは、[テスト署名](test-signing-driver-packages.md)ドライバーは、テスト コンピューターにします。 証明書ファイルは、テスト コンピューター上の任意のディレクトリにコピーできます。

2.  使用[ **CertMgr** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/certmgr)証明書を追加するコマンド、[信頼されたルート証明機関証明書ストア](trusted-root-certification-authorities-certificate-store.md)、[信頼された発行元証明書ストア](trusted-publishers-certificate-store.md)します。

次の CertMgr コマンドでは、証明書のファイル、証明書を追加します。 *CertificateFileName.cer*テスト コンピューター上のストアの証明書には、信頼されたルート証明機関。

```cpp
CertMgr.exe /add CertificateFileName.cer /s /r localMachine root /all
```

次の CertMgr コマンドでは、証明書のファイル、証明書を追加します。 *CertificateFileName.cer*テスト コンピューター上のストアの証明書には、信頼された発行元。

```cpp
CertMgr.exe /add CertificateFileName.cer /s /r localMachine trustedpublisher
```

 

 





