---
title: ドライバー パッケージをリリース署名する方法
description: ドライバー パッケージをリリース署名する方法
ms.assetid: f02c0a50-01f1-456c-b432-c4d9e8cbc566
keywords:
- リリース署名ドライバー WDK
- ドライバー WDK、パッケージのリリース署名の署名
- ドライバー WDK、リリース署名パッケージへの署名
- デジタル署名 WDK、ドライバー パッケージのリリース署名
- WDK、ドライバー パッケージのリリース署名の署名
- リリース署名ドライバー WDK
- リリース署名ドライバー WDK、ドライバー パッケージ
- WDK のドライバー パッケージのリリース署名
- リリース署名ドライバー パッケージ、WDK テスト署名ドライバー パッケージについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 777ebffd59e2b14766050698aecff2995aca2b8b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386936"
---
# <a name="how-to-release-sign-a-driver-package"></a>ドライバー パッケージをリリース署名する方法


ときに従う必要のある基本的な手順を説明するリリース記号、[ドライバー パッケージ](driver-packages.md)します。 これには、次のデータが含まれます。

-   取得する、[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)商用証明機関 (CA) から。

-   準備、[ドライバー パッケージ](driver-packages.md)リリース署名します。 これは、作成が含まれています。、[カタログ ファイル](catalog-files.md)、ドライバー パッケージのデジタル署名が含まれています。

-   ドライバー パッケージのカタログ ファイルをリリース署名します。

-   埋め込みの署名でのドライバーをリリース署名します。 ドライバーの場合は、ドライバー内でのデジタル署名を埋め込む必要があります、*ブート開始ドライバー*します。

このセクションの各トピックでは、リリース署名中に、別の手順をについて説明し、手順について理解しておく必要のある一般的な情報を提供します。 さらに、各トピックを示す手順に関する詳細な情報を提供するその他のトピックです。

**注**  ここでは、ドライバー パッケージを手動でリリース署名するドライバーの発行者がある場合に必要な手順をについて説明します。 [ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)が[テスト カテゴリ](https://go.microsoft.com/fwlink/p/?linkid=189178)さまざまなデバイスの種類。 ドライバーの発行者を取得する必要があります、デバイスの種類のテスト カテゴリがこの一覧に含まれる場合、 [WHQL リリース署名](whql-release-signature.md)手動でリリース署名ドライバー パッケージではなく、ドライバー パッケージ用です。

 

このセクションを通じて、別々 のコンピューターは、ドライバーのリリースの署名に関連するさまざまな処理に使用されます。 これらのコンピューターは参照としては、次のように。

<a href="" id="--------signing-computer"></a> **コンピューターの署名**  
これは、リリースへのドライバーが Windows Vista および Windows の以降のバージョンのパッケージの署名を使用するコンピューターです。 このコンピューターでは、Windows XP SP2 または以降のバージョンの Windows が実行されている必要があります。 使用する、[ドライバーの署名ツール](https://msdn.microsoft.com/library/windows/hardware/ff552958)以降のバージョンの Windows Driver Kit (WDK) がインストールされている、このコンピューターは、Windows Vista をいる必要があります。

<a href="" id="test-computer"></a>**テスト コンピューター**  
これは、インストールし、リリースで署名されたドライバー パッケージをテストするために使用するコンピューターです。 このコンピューターでは、Windows Vista または Windows の以降のバージョンが実行されている必要があります。

リリース署名プロセスを説明しながら、このトピックは、セクションの使用、 *ToastPkg*サンプル ドライバー パッケージ。 WDK のインストール ディレクトリ内で、 *ToastPkg*ドライバー パッケージにありますが、 *src\\全般\\トースター\\toastpkg*ディレクトリ。

このセクションでは、次のトピックについて説明します。

[ソフトウェア発行元証明書 (SPC) を取得します。](obtaining-a-software-publisher-certificate--spc-.md)

[ドライバー パッケージのリリース署名カタログ ファイルを作成します。](creating-a-catalog-file-for-release-signing-a-driver-package.md)

[ドライバー パッケージのカタログ ファイルをリリース署名](release-signing-a-driver-package-s-catalog-file.md)

[埋め込みの署名でのドライバーをリリース署名](release-signing-a-driver-through-an-embedded-signature.md)

[リリース署名の検証](verifying-the-release-signature.md)

[リリース署名をサポートするコンピューターを構成します。](configuring-a-computer-to-support-release-signing.md)

[リリースで署名されたドライバー パッケージをインストールします。](installing-a-release-signed-driver-package.md)

 

 





