---
title: テスト ドライバー パッケージを署名する方法
description: テスト ドライバー パッケージを署名する方法
ms.assetid: 992f0974-0b0e-4c96-ad16-c5894067896c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b93c83d44aa25ac15fef1a4beaa4264aaa80891a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532326"
---
# <a name="how-to-test-sign-a-driver-package"></a>テスト ドライバー パッケージを署名する方法


このセクションでは、ときに従うことがあるという基本的な手順に関する情報を提供するテスト署名、[ドライバー パッケージ](driver-packages.md)します。 

参照のプレリリース版をサインインするとき、テスト証明書を使用するテスト署名、[ドライバー パッケージ](driver-packages.md)テスト コンピューターで使用します。 具体的には、これにより、開発者などの自己署名証明書を使用してカーネル モード バイナリに署名する、 [ **MakeCert** ](https://msdn.microsoft.com/library/windows/hardware/ff548309)ツールが生成されます。 この機能により、開発者とドライバー署名の検証が有効になっている Windows のカーネル モード バイナリをテストします。

Windows では、開発およびテスト目的のみのテスト署名されたドライバーをサポートしています。 テスト署名されたドライバーを運用環境では使用せず、顧客にリリースする必要があります。

このセクションには、次の手順について説明し、次の例を紹介するトピックが含まれています。

-   ドライバー パッケージの署名に使用されるテスト証明書を作成します。 このセクションで手順は、作成してという名前のテスト用の自己署名証明書を使用する説明*Contoso.com(Test)* します。 この証明書は、このセクションで説明されている多くの例で使用されます。

-   準備、[ドライバー パッケージ](driver-packages.md)テスト署名のためです。 これは、作成、[カタログ ファイル](catalog-files.md)デジタル署名を格納しています。

-   使用して、ドライバー パッケージのカタログ ファイルのテスト署名、 *Contoso.com(Test)* 証明書。

-   使用して、ドライバーは、埋め込み署名のテスト署名、 *Contoso.com(Test)* 証明書。

    **注**  ドライバーがある場合は、ドライバー内でのデジタル署名を埋め込む必要があります、*ブート開始ドライバー*します。

     

このセクションの各トピックでは、テスト署名中に、別の手順をについて説明し、手順を理解する必要がある一般的な情報を提供します。 さらに、各トピックを示す手順に関する詳細な情報を提供するその他のトピックです。

このセクションでは、別々 のコンピューターは、テスト署名ドライバーに関連するさまざまな処理に使用されます。 これらのコンピューターは参照としては、次のように。

<a href="" id="signing-computer"></a>**コンピューターの署名**  
これは、テスト署名ドライバーが Windows Vista および Windows の以降のバージョンのパッケージ化するために使用するコンピューターです。 このコンピューターでは、Windows XP SP2 または以降のバージョンの Windows が実行されている必要があります。 使用するには、[ドライバーの署名ツール](https://msdn.microsoft.com/library/windows/hardware/ff552958)以降のバージョンの Windows Driver Kit (WDK) がインストールされている、このコンピューターは、Windows Vista をいる必要があります。

<a href="" id="test-computer"></a>**テスト コンピューター**  
これは、インストールし、テスト署名されたドライバー パッケージをテストするために使用するコンピューターです。 このコンピューターでは、Windows Vista または Windows の以降のバージョンが実行されている必要があります。

このトピックのセクションの使用、 *ToastPkg*テスト署名プロセスを導入するドライバー パッケージのサンプルです。 WDK のインストール ディレクトリ内で、 *ToastPkg*ドライバー パッケージにありますが、 *src\\全般\\トースター\\toastpkg*ディレクトリ。

**注**  、WDK には正しくテスト署名するための手順を示すサンプル コマンド スクリプトが含まれています、 *ToastPkg*サンプル[ドライバー パッケージ](driver-packages.md)します。 ドライバー パッケージに署名をテストするには、このスクリプトを変更できます。 例では、WDK のインストール ディレクトリ内にある*src\\全般\\ビルド\\driversigning\\selfsign_example.cmd*します。 テスト署名に関する詳しい説明については「 *src\\全般\\ビルド\\driversigning\\selfsign_readme.htm*します。

 

ここでは、次のトピックについて説明します。

[テスト証明書の作成](creating-test-certificates.md)

[テスト証明書の表示](viewing-test-certificates.md)

[ドライバー パッケージのテスト署名カタログ ファイルを作成します。](creating-a-catalog-file-for-test-signing-a-driver-package.md)

[テスト署名ドライバー パッケージのカタログ ファイル](test-signing-a-driver-package-s-catalog-file.md)

[テスト署名ドライバーは、埋め込みの署名](test-signing-a-driver-through-an-embedded-signature.md)

[テスト署名をサポートするために、テスト コンピューターを構成します。](configuring-the-test-computer-to-support-test-signing.md)

[テスト証明書のインストール](installing-test-certificates.md)

[テスト署名の検証](verifying-the-test-signature.md)

[テスト コンピューターにテスト署名されたドライバー パッケージをインストールします。](installing-a-test-signed-driver-package-on-the-test-computer.md)

 

 





