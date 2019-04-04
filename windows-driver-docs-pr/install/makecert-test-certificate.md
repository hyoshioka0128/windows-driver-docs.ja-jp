---
title: MakeCert テスト証明書
description: MakeCert テスト証明書
ms.assetid: 17f63c42-a563-4a57-a3be-ac3b2e97ee3b
keywords:
- テスト証明書の MakeCert WDK
- デジタル証明書 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46c8ca0484a7325b95cbfe5b5f0a77a0f64d4475
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529308"
---
# <a name="makecert-test-certificate"></a>MakeCert テスト証明書


MakeCert テスト証明書が、 [X.509 デジタル証明書](digital-certificates.md)を使用して作成され、 [ **MakeCert** ](https://msdn.microsoft.com/library/windows/hardware/ff548309)ツール。 MakeCert テスト証明書はテスト署名に使用できる、自己署名ルート証明書を[ドライバー パッケージの](driver-packages.md)[カタログ ファイル](catalog-files.md)またはテスト署名ドライバー ファイルの署名を埋め込むことで、ドライバー ファイル。

MakeCert テスト証明書の作成の詳細については、[**テスト証明書の作成**](creating-test-certificates.md)を参照してください。

## <a name="installing-a-makecert-test-certificate"></a>MakeCert テスト証明書をインストールします。

テスト署名、[カタログ ファイル](catalog-files.md)またはドライバー ファイルの署名を埋め込み、MakeCert テスト証明書が個人証明書ストア ("my"ストア)、またはサインインするローカル コンピューターの他のカスタム証明書ストアであることができます、ソフトウェア。 ただし、テスト署名を確認するに対応するテスト証明書インストール必要がありますが、[信頼されたルート証明機関証明書ストア](trusted-root-certification-authorities-certificate-store.md)署名の検証に使用するローカル コンピューターの。

使用して、 [ **CertMgr** ](../devtest/certmgr.md)ツール、次のように、ドライバーの署名に使用するローカル コンピューターの信頼されたルート証明機関の証明書ストアにテスト証明書をインストールします。

```cpp
CertMgr /add CertFileName.cer /s /r localMachine root
```

インストールする前に、[ドライバー パッケージ](driver-packages.md)MakeCert テスト証明書によって署名されている、信頼されたルート証明機関の証明書ストアにテスト証明書をインストールする必要があります、[信頼済み証明書ストアの発行元](trusted-publishers-certificate-store.md)のテスト コンピューター。 テスト コンピューターで MakeCert テスト証明書をインストールする方法については、[テスト コンピューターにテスト証明書をインストールする](installing-a-test-certificate-on-a-test-computer.md)を参照してください。

 

 





