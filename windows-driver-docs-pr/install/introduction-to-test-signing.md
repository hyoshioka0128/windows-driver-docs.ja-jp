---
title: テスト署名の概要
description: テスト署名の概要
ms.assetid: 63d4627d-b92c-489d-accf-16cfb5ac1410
keywords:
- テスト署名ドライバー パッケージ、WDK テスト署名ドライバー パッケージについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2426a79f688a0df2ad5f4794a006b07a7a2c05f6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364302"
---
# <a name="introduction-to-test-signing"></a>テスト署名の概要


ドライバーは、使用してテスト署名する必要があります、[デジタル署名](digital-signatures.md)開発やテストは、次の理由。

-   容易にし、インストールを自動化します。

    ドライバーが署名されていない場合、[プラグ アンド プレイ (PnP) ドライバーのインストール ポリシー](digital-signatures-and-pnp-device-installation--windows-vista-and-late.md) Windows Vista 以降のバージョンの Windows がシステム管理者は、未署名のドライバのインストールを手動で承認を必要と追加します。インストール プロセスに余分な手順です。 この余分な手順は、開発者およびテスト担当者の生産性を低下します。 この要件をオーバーライドすることはできません。

-   64 ビット バージョンの Windows Vista と以降のバージョンの Windows カーネル モード ドライバーをロードできます。

    既定で、[カーネル モード コードの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)の 64 ビット バージョンの Windows Vista と Windows の以降のバージョンは、カーネル モード ドライバーが読み込まれるドライバーの順序で署名する必要があります。 この要件は、開発やドライバーのデバッグを容易に一時的にオーバーライドできます。

-   特定の種類の次世代のプレミアム コンテンツを再生するには、Windows Vista および Windows の以降のバージョンですべてのカーネル モード コンポーネントに署名する必要があります。 さらに、すべてのユーザー モードとカーネル モード コンポーネント Protected Media Path (PMP) では、PMP の署名ポリシーに準拠する必要があります。 PMP については、ポリシーの署名のホワイト ペーパーを参照[Windows Vista のメディアの保護されているコンポーネントのコード署名](https://go.microsoft.com/fwlink/p/?linkid=69258)します。

これらの理由から、Windows Vista および Windows の以降のバージョン用のドライバーは、Microsoft Authenticode を使用して作成されるデジタル証明書でテスト署名する必要があります。 このようなデジタル証明書と呼びます、*テスト証明書*テスト証明書を使用して生成された署名と呼ばれますと、*テスト署名*します。

**注**  Windows Vista および Windows の以降のバージョンは、開発およびテスト目的に対してのみテスト署名されたドライバーをサポートします。 テスト署名を運用環境では使用せず、顧客にリリースする必要があります。

 

開発/テスト チームが参加できる、 [WHQL テスト署名プログラム](whql-test-signature-program.md)、Windows Hardware Quality Labs (WHQL) を PnP サインイン[ドライバー パッケージ](driver-packages.md)テスト目的で。 開発/テスト チームがまたは、独自の社内署名プロセスを管理しの次の種類を使用して、[テスト証明書](test-certificates.md)テスト署名ドライバーに。

-   [テスト証明書の MakeCert](makecert-test-certificate.md)、デジタル証明書がによってこれを作成、 [ **MakeCert** ](https://msdn.microsoft.com/library/windows/hardware/ff548309)ツール。

-   [市販のテスト証明書](commercial-test-certificate.md)、これは、Microsoft ルート証明書プログラムのメンバーである CA によって発行されるデジタル証明書。

-   [テスト証明書をエンタープライズ CA](enterprise-ca-test-certificate.md)、これは、エンタープライズ CA によって展開されているデジタル証明書。

チームの作成、取得、またはテスト証明書を提供した後にテスト チームが、ドライバー パッケージに署名する方法については、次を参照してください。[ドライバー パッケージのテスト署名](test-signing-driver-packages.md)します。

テスト署名されたドライバー パッケージをインストールする方法については、次を参照してください。 [Installing Test-Signed ドライバー パッケージ](installing-test-signed-driver-packages.md)します。

初期のドライバーの開発とデバッグを容易に、カーネル モード コードを読み込むしを未署名のカーネル モード ドライバーをテストするための要件を署名を一時的に無効にできます。 ただし、未署名のドライバのインストールを承認するためにシステム管理者を必要とする PnP ドライバーのインストール ポリシーを無効にすることはできません。 未署名のドライバをインストールする方法の詳細については、次を参照してください。[開発およびテスト中に、署名されていないドライバーをインストールする](installing-an-unsigned-driver-during-development-and-test.md)します。

テスト署名ドライバー パッケージに使用する最適なツールについては、次を参照してください。[ドライバーの署名ツール](https://msdn.microsoft.com/library/windows/hardware/ff552958)します。

**注**  テスト署名ドライバー パッケージに関連する手順の理解を深めるためには、次を参照してください。[テスト署名ドライバー パッケージ方法](how-to-test-sign-a-driver-package.md)します。 このトピックでは、テスト署名プロセスの概要を提供し、テスト署名の例の多くを使用してステップ実行、 *ToastPkg*サンプル[ドライバー パッケージ](driver-packages.md)Windows Driver Kit (WDK) 内で。

 

 

 





