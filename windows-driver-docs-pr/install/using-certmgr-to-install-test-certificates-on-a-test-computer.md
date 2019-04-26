---
title: テスト コンピューターへの CertMgr を使用したテスト証明書のインストール
description: テスト コンピューターへの CertMgr を使用したテスト証明書のインストール
ms.assetid: 5928c810-65e8-412e-9723-7b371574006c
keywords:
- Certmgr ツール
- 証明書マネージャー ツールを WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccda7273b3b8173f0382a0e3e928fc6cb7a16193
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339455"
---
# <a name="using-certmgr-to-install-test-certificates-on-a-test-computer"></a>テスト コンピューターへの CertMgr を使用したテスト証明書のインストール


使用して、テスト コンピューターにテスト証明書をインストールする[ **CertMgr**](https://msdn.microsoft.com/library/windows/hardware/ff543411)、これらの手順に従います。

1.  証明書のコピー (*.cer*) に使用したファイルは、[テスト署名](test-signing-driver-packages.md)ドライバーは、テスト コンピューターにします。 証明書ファイルは、テスト コンピューター上の任意のディレクトリにコピーできます。

2.  使用[ **CertMgr** ](https://msdn.microsoft.com/library/windows/hardware/ff543411)証明書を追加するコマンド、[信頼されたルート証明機関証明書ストア](trusted-root-certification-authorities-certificate-store.md)、[信頼された発行元証明書ストア](trusted-publishers-certificate-store.md)します。

次の CertMgr コマンドでは、証明書のファイル、証明書を追加します。 *CertificateFileName.cer*テスト コンピューター上のストアの証明書には、信頼されたルート証明機関。

```cpp
CertMgr.exe /add CertificateFileName.cer /s /r localMachine root /all
```

次の CertMgr コマンドでは、証明書のファイル、証明書を追加します。 *CertificateFileName.cer*テスト コンピューター上のストアの証明書には、信頼された発行元。

```cpp
CertMgr.exe /add CertificateFileName.cer /s /r localMachine trustedpublisher
```

 

 





