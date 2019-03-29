---
title: テスト署名されたドライバー ファイルの署名の検証
description: テスト署名されたドライバー ファイルの署名の検証
ms.assetid: 21f4c42c-3d6e-453c-acff-f4b8acc3e20b
keywords:
- テスト署名ドライバー ファイル WDK
- テスト署名の検証
- テスト署名の確認
- 署名 WDK をテストします。
- テスト証明書検証 WDK
- ドライバーのファイル署名 WDK をテストします。
- テスト署名ドライバー パッケージにドライバー ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e923126bbf0a19944589be54d8bd86af3e44728
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570190"
---
# <a name="verifying-the-signature-of-a-test-signed-driver-file"></a>テスト署名されたドライバー ファイルの署名の検証


ドライバー ファイルに埋め込まれているテスト署名を確認するには、次を使用して[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)コマンド。

```cpp
SignTool verify /v /pa DriverFileName.sys
```

各項目の意味は次のとおりです。

-   **確認**コマンドでは、ドライバー ファイルに埋め込まれている署名を検証する SignTool を構成します。 *DriverFileName.sys します。*

-   **/V**オプションを実行し、警告メッセージを印刷する SignTool を構成します。

-   **/Pa**オプションを構成することを確認する SignTool に埋め込まれている署名*DriverFileName.sys* PnP デバイスのインストールの署名の要件に準拠します。

-   *DriverFileName.sys*ドライバー ファイルの名前を指定します。

注意してくださいを SignTool**確認**コマンドは、ドライバー ファイルの署名に使用されたテスト証明書を明示的に指定しません。 検証操作が成功するには、テスト証明書をインストールする必要があります最初、[信頼されたルート証明機関証明書ストア](trusted-root-certification-authorities-certificate-store.md)署名の検証に使用するローカル コンピューターの。 テスト証明書をローカル コンピューターの信頼されたルート証明機関の証明書ストアにインストールする方法の詳細については、次を参照してください。[テスト コンピューターにテスト証明書をインストールする](installing-a-test-certificate-on-a-test-computer.md)します。 インストール手順は、署名のコンピューターとテスト用のコンピューターの両方で同じです。

次のコマンドがで埋め込みの署名を検証するなど、 *Toaster.sys*では、 *amd64*コマンドが実行されるディレクトリのサブディレクトリ。

```cpp
SignTool verify /v /pa amd64\toaster.sys
```

 

 





