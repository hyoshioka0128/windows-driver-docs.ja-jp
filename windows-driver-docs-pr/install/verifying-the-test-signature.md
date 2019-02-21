---
title: テスト署名の検証
description: テスト署名の検証
ms.assetid: 996ce3d4-76b5-4c78-9ea9-ca8a04cfef99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c846d78f2ae798c8122b605e0aff070794c1ade
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553482"
---
# <a name="verifying-the-test-signature"></a>テスト署名の検証


テスト証明書が、テスト コンピューターの信頼されたルート証明機関の証明書ストアにコピーされた後[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)以下を実行するために使用できます。

-   指定したファイルの署名を検証、[ドライバー パッケージの](driver-packages.md) [カタログ ファイル](catalog-files.md)します。

-   など、カーネル モード バイナリ ファイルの埋め込み署名の検証、*ブート開始ドライバー*します。

次の例は、ファイルの 1 つの署名を検証*toastpkg.inf*、Toastpkg サンプルの署名済みカタログ ファイルで*tstamd64.cat*します。 このカタログ ファイルの作成方法の詳細については、次を参照してください[カタログ ファイルを作成するのを使用して Inf2Cat](using-inf2cat-to-create-a-catalog-file.md):。

```cpp
Signtool verify /pa /v /c tstamd64.cat toastpkg.inf
```

各項目の意味は次のとおりです。

-   **確認**コマンドでは、指定したファイルを確認する SignTool を構成します。 t*oastpkg.inf*します。

-   **/Pa**オプションがデジタル署名を検証するときに、Authenticode 検証ポリシーの使用を指定します。

-   **/V**で SignTool の表示が正常に実行し、警告メッセージの詳細な操作を有効にします。

-   **/C**オプションは、カタログ ファイル名を指定します。

    **注**  埋め込まれた署名付きのカーネル モード バイナリのファイルの署名を検証するときに使用しないでください、 **/c**引数。

     

-   *toastpkg.inf*検証するファイルの名前を指定します。

次の例の署名を検証する、 *Toastpkg*サンプルの署名済みカタログ ファイルでは、 *Tstamd64.cat*:

```cpp
Signtool verify /pa /v tstamd64.cat
```

使用する方法の詳細についての[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)カタログ ファイルのデジタル署名を確認するを参照してください。 [Test-Signed カタログ ファイルの署名の検証](verifying-the-signature-of-a-test-signed-catalog-file.md)です。

 

 





